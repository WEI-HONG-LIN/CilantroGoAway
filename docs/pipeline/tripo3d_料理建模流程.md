# Tripo3D 料理建模流程

**用途：** 新增一道「可互動料理」時，從拆件、生成、清理到放進 Godot 的標準流程。每道料理都照這份流程走一次。
**配套文件：** [`tripo3d_prompt範本.md`](tripo3d_prompt範本.md)（所有 prompt）、企劃書 v1.1 第 4、7 章、`docs/roles/04_3D美術.md`。

> **資料來源（2026-10-21 核對）：** 參數、模型版本、點數價格與 API 授權條款都已對照 [Tripo 開發者文件](https://developers.tripo3d.ai/en/docs/introduction) 與 [API 定價頁](https://developers.tripo3d.ai/en/pricing)。Tripo Studio（網頁版）的訂閱方案條款在 `www.tripo3d.ai`，目前無法從這個環境讀取，仍需自行確認。Tripo 更新頻繁，正式生產時請**固定模型版本**，並定期重新核對。
>
> **參數命名：** 本文件使用 REST API v3 的名稱（`model`、`input`、`inputs`）。如果用 Python SDK（`tripo3d`），對應的名稱是 `model_version`、`image`、`images`，其他參數名稱相同。

---

## 0. 核心原則

1. **一個可互動物件 = 一次生成 = 一個 `.glb`。** 不要一次生成整盤料理。整盤生成的模型是「一整塊」，食物底下和互相接觸的面都是空的，無法拆成能各自落下、翻面的剛體。
2. **容器另外生成，而且是空的。** 碗、盤、醬碟單獨生成；湯是 Godot 的 shader（企劃書 7.5），不要讓 Tripo 生成「裝著湯的碗」。
3. **小而薄的東西不用 Tripo。** 香菜、蔥花、碎葉這類又小又薄的葉片，AI 生成常常破面或太厚。這些用 Blender 手工做低面數模型，品質和辨識度比較好控制（見 3.6）。
4. **一律先產生參考圖，再用圖片生成 3D。** 不用文字直接生成正式資產。文字生 3D 其實會在內部自動產生一張你看不到、也不能挑的圖，每次的風格都不一樣；先產生參考圖，可以在花 3D 點數之前用便宜的 2D 圖試錯，並把造型、顏色、風格先確定下來。
5. **每道料理先做一個風格基準物件。** 第一個物件的參考圖做到滿意，就是這道料理（以及之後所有料理）的風格基準；其他物件產生參考圖時，都要上傳基準圖當風格參考（見 3.2）。
6. **所有參數與 seed 都要記錄。** 每個資產都寫進資產紀錄（第 9 節），之後才能重現或微調。

## 1. 流程總覽

```text
① 拆件規劃 ──▶ ② 參考圖 ──▶ ③ 圖片生成 3D ──▶ ④ Tripo 後處理 ──▶ ⑤ Blender 清理
   (拆件表)    (基準圖→其他物件)  (P1 / H3.1)      (低面數/轉檔)      (比例/原點/碰撞/掛點)
                                                                         │
⑧ 登錄資產 ◀── ⑦ 驗收 ◀── ⑥ Godot 匯入與組裝 ◀──────────────────────────┘
 (資產紀錄)    (清單)      (FoodItem 場景)
```

| 步驟 | 負責角色 | 產出 | 預估時間（每個物件） |
|---|---|---|---|
| ① 拆件規劃 | 02 企劃 + 03 關卡 + 04 美術 | 料理拆件表 | 每道料理 1–2 小時 |
| ② 參考圖 | 04 美術 | 風格基準圖；每個物件 1 張通過檢查的正面圖（必要時 4 視角） | 10–20 分鐘 |
| ③ 生成 | 04 美術 | 原始模型（2–4 個候選） | 5–15 分鐘 |
| ④ 後處理 | 04 美術 | 低面數 `.glb` | 5 分鐘 |
| ⑤ Blender 清理 | 04 美術 | 遊戲用 `.glb` | 30–60 分鐘 |
| ⑥ Godot 組裝 | 06 程式（或 04 美術） | `food_<名稱>.tscn` | 15–30 分鐘 |
| ⑦ 驗收 | 08 QA + 04 美術 | 驗收清單打勾 | 15 分鐘 |

## 2. 步驟 ① 拆件規劃

用下面的表格把料理拆成物件。**這張表決定了要生成哪些模型**，填完要給企劃和關卡設計確認。

```markdown
## 料理拆件表：<料理名稱>（<dish_id>）

| # | 物件 ID | 中文名 | 類型 | 數量 | 實際尺寸（cm, 長×寬×高） | 生成方式 | 碰撞形狀 | 密度 | 會進湯 | 香菜掛點面 |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | bowl_noodle | 麵碗 | 容器（固定） | 1 | 18×18×8 | Tripo 圖生 | 凹面（三角網格） | — | — | — |
| 2 | food_beef_chunk | 牛肉塊 | 可互動食物 | 3 | 4×3×2.5 | Tripo 圖生 | 凸包 ×1 | 1.1 | 是 | Top/Side/Bottom |
| … | | | | | | | | | | |

- 誘餌：<蔥花、青菜碎葉…（手工）>
- 香菜：<使用共用香菜模型，不新增>
- 湯：<湯色預設、混濁度、液面高度>
- 共用資產：<可以直接重用的既有模型>
- 變體需求：<例如牛肉塊要 2 種形狀，避免重複感>
```

**類型與生成方式的判斷：**

| 物件特性 | 生成方式 |
|---|---|
| 有體積、外形圓潤的食物（肉塊、蛋、水餃、麵條團） | Tripo 圖生 3D |
| 容器（碗、盤） | Tripo 圖生 3D，或在 Blender 用旋轉成形（更乾淨、更快） |
| 又薄又小的葉片（香菜、蔥花、碎葉、海苔） | Blender 手工 |
| 餐具（筷子、鑷子、湯匙） | Blender 手工，或 Tripo 圖生 3D 後大幅簡化 |
| 液體（湯、醬汁） | 不建模，用 Godot shader |

**重用原則：** 先查 `art/models/` 有沒有可重用的物件（青菜、碗、盤子）。同一種食材做 2 個造型變體，就能在關卡中重複出現而不顯得單調。

## 3. 步驟 ② 參考圖（必做）

### 3.1 要求

| 項目 | 要求 |
|---|---|
| 格式（官方規格） | PNG／JPEG／WebP，≤ 20 MB，至少 256×256 px；主體清楚、背景乾淨、遮擋少 |
| 比例 | 1:1 |
| 構圖 | **單一物件**，置中，佔畫面 70–80%，完整不裁切 |
| 視角 | 3/4 俯視（約 30°），能看到物件的主要輪廓 |
| 背景 | 純白，無陰影、無桌面、無盤子 |
| 光線 | 均勻柔光，不要強烈的高光和投影（否則會被烘進貼圖） |
| 風格 | 套用 [prompt 範本](tripo3d_prompt範本.md) 的 `STYLE`；基準物件以外的物件要上傳風格基準圖 |
| 解析度 | 1024×1024 以上 |

### 3.2 風格基準物件

1. 每道料理選一個**造型最單純**的物件當基準（例如牛肉麵選牛肉塊）。專案的第一道料理做出的基準圖，就是**整個遊戲**的風格基準。
2. 基準圖要一直改到滿意為止：Q 版程度、顏色飽和度、霧面質感、細節多寡都在這一步定案。建議請企劃一起看過再往下做。
3. 基準圖存到 `art/source/style_anchor/<dish_id>_<物件>.png`，並寫進資產紀錄。試做中、還沒選定的參考圖和 Tripo 原始下載檔，放在 `art/_local/`（不會上傳到 GitHub）。
4. 之後每個物件產生參考圖時：
   - 上傳基準圖當參考；
   - prompt 最前面加上 [prompt 範本](tripo3d_prompt範本.md) 2.3 節 的風格參考段落；
   - 用和基準圖**相同的圖像模型**。
5. 新的料理沿用專案的基準圖；只有在企劃決定改風格時才換基準圖，並記錄在 `docs/decisions.md`。

### 3.3 產生方式

**主要：Tripo 網頁版 Image 分頁**（介面依 2026-10-23 的截圖整理，完整對照見第 12 節）

| 設定 | 建議 |
|---|---|
| Prompt | 照 [prompt 範本](tripo3d_prompt範本.md) 第 2 節組合；**這個分頁沒有負面描述欄位**，不要貼 Negative 段落 |
| Generation Model | 整個專案固定用同一個模型（目前可用 Nano Banana；GPT Image 2.5 需升級方案） |
| Aspect Ratio | 1:1 |
| Number of Images | 4（想省點數可選 2） |
| 4K Resolution | 關 |
| 參考圖 | 基準物件以外，上傳風格基準圖（輸入框左下角的圖片按鈕，待確認） |

**其他方式：**
- **Tripo API**：`POST /v3/generation/text-to-image`（`seedream_v4`，5 點；`banana_pro` 品質較高，15 點）；之後把該任務的 `task_id` 直接當成圖生 3D 的 `input`。
- **其他圖像生成工具或手繪**：可以，但同一道料理的所有物件要用同一個工具。

### 3.4 進入 3D 前的檢查（每張參考圖都要通過）

- [ ] 畫面中只有這一個物件：沒有盤子、筷子、桌面或其他食物。
- [ ] 物件完整在畫面內，背景是乾淨的白色。
- [ ] 沒有明顯的投影或強烈高光。
- [ ] 一眼看得出是什麼食物，而且是 Q 版玩具感，不寫實、不油亮。
- [ ] 和風格基準圖放在一起，看起來是同一個遊戲。
- [ ] 平放的物件底部是平的。
- [ ] 綠色物件和香菜在輪廓上明顯不同。

沒通過就改 prompt 重新產生，**不要拿不合格的圖去生成 3D**。2D 圖便宜很多，在這一步多試幾次比較省。

### 3.5 什麼時候需要多視角

正面看不出背面形狀的物件（例如水餃的摺邊、肉塊的不規則背面），改用 **multiview-to-model**：

- 最多 4 張（front／left／back／right），**正面必填，至少 2 張**；所有圖片的物件、光線必須一致。
- 最省事的做法：用 `POST /v3/generation/image-to-multiview`（10 點）從正面圖自動產生四個視角，再把它的 `task_id` 以 `inputs: [{"task_id": "…"}]` 傳給 multiview-to-model。
- 自動產生的視角不對時，可以用 Edit Multiview（每張 5 點）修正單一視角。

### 3.6 手工物件（香菜、誘餌）

香菜只做一次，全遊戲共用（企劃書 4.2：完整葉、小葉、碎葉 × 2 色，加上浸濕變體）。做法：在 Blender 用低面數平面做葉片，稍微加厚（0.5–1 mm）並加上葉柄，三角面 ≤ 300。蔥花用短圓環，青菜碎葉用不規則的薄片。重點是和香菜在**輪廓上**明顯不同（企劃書 4.1）。

## 4. 步驟 ③ 圖片生成 3D

### 4.1 選擇模型

| 模型（`model`） | 特性（官方文件） | 每次圖生 3D 的點數（含標準貼圖） | 本專案用途 |
|---|---|---|---|
| `P1-20260311` | P 系列穩定版，官方推薦用於遊戲與行動裝置的低面數資產；拓撲乾淨、面數控制精準（50–20,000） | 50 | **首選**：食物與容器 |
| `v3.1-20260211`（H3.1） | 預設的高精度模型；可加 `smart_low_poly`（+10 點，面數 500–20,000） | 30（+10 低面數 = 40） | **備案**：P1 造型不理想時改用；比 P1 便宜，但低面數模式遇到複雜造型可能失敗 |
| `P2-20260801` | P 系列下一代，原生四邊面；**目前是 Preview** | 110 | 暫不使用：Preview 版本可能變動，而且較貴 |

> 官方建議正式生產時固定模型版本，避免模型更新造成風格不一致。整個專案請統一用同一個版本，換版本要記錄在 `docs/decisions.md`。
>
> **P1 不支援** `smart_low_poly`、`quad`、`generate_parts`、`geometry_quality`，送了也沒有作用；P1 的面數直接由 `face_limit` 控制。

### 4.2 建議參數

| 參數 | P1 建議值 | H3.1 建議值 | 說明 |
|---|---|---|---|
| `input`／`inputs` | 參考圖的 `task_id`、`file_token` 或 URL | 同左 | 一次只能用一種來源 |
| `face_limit` | 食物 3000；容器 5000 | 同左 | 官方建議簡單模型至少 150、複雜模型至少 250，太低會變形 |
| `smart_low_poly` | 不支援 | `true` | 複雜造型可能失敗，失敗不扣點，關掉重試即可 |
| `texture` | `true` | `true` | |
| `pbr` | `false` | `false` | 預設是 `true`；我們用 Q 版材質，只需要顏色貼圖。開了 `pbr` 會強制開 `texture` |
| `texture_quality` | `standard` | `standard` | `detailed` +10 點、`extreme`（8K）+20 點，小物件用不到 |
| `texture_version` | `v3.5-20260815` | `v3.5-20260815` | 最新的貼圖模型，搭配 `delight` 使用 |
| `delight` | `true` | `true` | 去除參考圖中烘進去的光影，正好符合「平塗、無陰影」的貼圖需求；只有 v3.5 貼圖模型有效 |
| `texture_alignment` | `original_image` | `original_image` | 顏色以參考圖為準 |
| `orientation` | `default` | `default` | |
| `auto_size` | `false` | `false` | 開啟會以公尺為單位縮放；我們統一在 Blender 依拆件表縮放 |
| `export_orientation` | **不要設定** | **不要設定** | 官方說明：設定後再做後處理，方向可能會錯但不會報錯；方向在最後的 convert 才處理 |
| `quad` | 不支援 | `false` | 開啟會強制輸出 FBX |
| `generate_parts` | 不支援 | `false` | 和貼圖、低面數都衝突 |
| `model_seed`、`texture_seed` | 記錄下來 | 記錄下來 | 同樣的輸入加上同樣的 seed 會得到相同結果；只想換貼圖時，固定 `model_seed`、改 `texture_seed` |

### 4.3 生成策略

1. 每個物件先用 P1 生成 2–3 個候選（換 `model_seed`），選造型最好的一個。
2. P1 的造型不理想時，用同一張參考圖改跑 H3.1 + `smart_low_poly` 比較。
3. 只有貼圖不滿意時，用 `POST /v3/models/texture` 重新上貼圖（10 點，可以加文字或圖片提示），不要整個重新生成。
4. **同一個物件生成 3 次還不滿意，就回到步驟 ② 改參考圖**，不要一直重抽浪費點數。常見原因：視角太斜、物件被切到、背面形狀看不出來（改用多視角）。
5. 失敗或取消的任務不扣點；P 系列同時最多 5 個任務並行。

### 4.4 替代方案：整盤生成再切割

如果想要「整盤料理」的構圖感，可以先生成整盤，再用 `mesh_segmentation`（`segmentation_granularity`：`simple`／`balanced`／`detailed`）切成零件，然後用 `mesh_completion`（`ai_completion`）補上被遮住的面。這條路線結果較不穩定，**只建議用來做非互動的裝飾性料理**，可互動的食物還是照 4.1 一件一件生成。

## 5. 步驟 ④ Tripo 後處理

| 工具（REST 端點／SDK 方法） | 何時使用 | 建議參數 | 點數 |
|---|---|---|---|
| Convert Format：`POST /v3/models/convert`（SDK `convert_model`） | **每個物件都要** | `format: "GLTF"`、`texture_size: 512`（食物）／`1024`（容器）、`pivot_to_center_bottom: true`、`flatten_bottom: true`（只用在應該平放的物件，例如水餃、碗、盤）；方向需要調整時在這一步設定 `export_orientation` | 5；有任何非預設參數（例如上面這些）就是 10 |
| Retopology：`POST /v3/mesh/decimate`（SDK `smart_lowpoly`） | 面數還太高，或拓撲太亂 | `model: "v3.0"`、`face_limit: 3000`、`smart_uv: true` | 35（v3.0 三角面） |
| Smart UV：`POST /v3/mesh/uv`（SDK `mesh_uv`） | UV 破碎、之後要重畫貼圖時 | 輸入不能超過 80,000 個三角面 | 20 |
| Texture：`POST /v3/models/texture`（SDK `texture_model`） | 只想換貼圖 | 同 4.2 的貼圖參數，可加文字或圖片提示 | 10（標準） |

`pivot_to_center_bottom` 會把原點放在底部中心，符合 04 美術的原點規範；香菜原點例外（葉柄根部），但香菜是手工做的，不受影響。

## 6. 步驟 ⑤ Blender 清理

照順序做，每一步都要做：

1. **匯入與比例**：匯入 `.glb`，依拆件表的實際尺寸縮放（例如牛肉塊 4 cm 長）。專案比例尺是 **1 Godot 單位 = 10 cm**（04 美術規範），所以 4 cm = 0.4 單位。套用縮放與旋轉（`Ctrl+A`）。
2. **檢查網格**：合併重複頂點、重新計算法線、刪除浮空的碎片；確認三角面數在預算內，超出就用 Decimate 減面。
3. **造型修正**：AI 生成常見的問題，例如底部不平、細節糊掉、左右不對稱；平放的物件底部要平，圓的物件不要有凸點，以免物理上停不穩或亂滾。
4. **貼圖**：檢查顏色是否符合 Q 版色調、有沒有烘進陰影或高光；需要時在 Blender 或繪圖軟體修色。貼圖尺寸：食物 512²、容器 1024²。
5. **物理碰撞**：建立 1–4 個凸包（可以用 Blender 內建的 Convex Hull，或 V-HACD 等凸包分解外掛），**物件名稱加上 `-convcolonly` 後綴**，例如 `food_beef_chunk_a-convcolonly`；Godot 匯入時會自動變成碰撞形狀，而且不會被渲染。容器的凹面內側用 `-colonly`（三角網格碰撞，只能用在固定物件）。
6. **重心**：如果重心需要偏移（例如水餃要平底朝下），加一個名為 `CenterOfMass` 的空物件，程式會讀取它的位置設定剛體的 `center_of_mass`。
7. **香菜掛點**：依拆件表和關卡設計的需求，在表面加空物件（Empty），命名 `Anchor_<食物>_<面>_<序號>`，例如 `Anchor_BeefChunk_Bottom_01`；Z 軸（或 Y 軸，和程式約定）朝外，貼齊表面。
8. **浮力取樣點**：會進湯的物件，在體積內平均放 4–8 個空物件 `Buoyancy_01`…`Buoyancy_08`。
9. **命名與匯出**：根物件命名 `food_<名稱>_<變體>`；匯出 glTF 2.0 二進位（`.glb`），勾選「+Y Up」、套用修改器、包含自訂屬性；原始檔存到 `art/source/<dish_id>/`，匯出檔存到 `art/models/<dish_id>/`。

## 7. 步驟 ⑥ Godot 匯入與組裝

1. **匯入設定**（`.glb` 的 Advanced Import Settings）：
   - 確認 `-convcolonly` 物件已變成 `CollisionShape3D`。
   - Materials：「Extract」到 `art/materials/<dish_id>/`，再改用專案共用的 Q 版材質或 shader，只保留顏色貼圖。
   - Meshes：小物件關閉 LOD 產生（面數已經很低）。
2. **建立食物場景** `scenes/food/<dish_id>/food_<名稱>.tscn`：
   - 根節點用 `RigidBody3D`，掛 `food_item.gd`；把 `.glb` 實例化為子節點，或使用繼承場景。
   - 把碰撞形狀移到 `RigidBody3D` 底下（剛體只認直屬的碰撞形狀）。
   - 設定 `PhysicsMaterial`（從 `resources/physics_materials/` 選）、密度（從拆件表取得）。
   - 會進湯的物件加上 `BuoyancyBody` 節點，取樣點指向 `Buoyancy_*`。
   - `Anchor_*` 節點保留，給關卡配置使用。
3. **物理比例尺**：因為 1 單位 = 10 cm，專案的重力必須設為 `98`（`Physics > 3D > Default Gravity`），不然東西會像在月球上一樣慢慢掉。這一點要和程式確認一次。
4. **組裝料理場景** `scenes/dishes/<dish_id>.tscn`：放容器（`StaticBody3D`）、食物實例、`SoupVolume`（如果有湯）。

## 8. 步驟 ⑦ 驗收清單

每個物件都要通過：

- [ ] 三角面數、貼圖尺寸在預算內（食物 ≤ 3000 三角面、512²）。
- [ ] 尺寸符合拆件表，和其他食物放在一起比例正確。
- [ ] 遊戲內截圖：預設距離、檢查距離、灰階版，都能認出是什麼食物。
- [ ] 和同一道料理的其他物件並排，風格一致（顏色飽和度、圓潤程度、貼圖細緻度）。
- [ ] 從 3 個高度、3 個角度放下，都能在 3 秒內停穩；碰撞沒有懸空或陷入。
- [ ] 會進湯的物件，浮沉方向符合拆件表的密度。
- [ ] 每個 `Anchor_*` 上的香菜貼齊表面，旋轉時不穿模、不懸空。
- [ ] 資產紀錄已填寫。

## 9. 步驟 ⑧ 資產紀錄

在 `art/asset_log.md` 每個物件新增一筆：

```markdown
### food_beef_chunk_a
- 料理：beef_noodle_soup
- 管道：<Tripo 網頁版／API>
- 參考圖：art/source/beef_noodle_soup/ref_beef_chunk_a.png
- 參考圖的圖像模型與 prompt：<例如 Nano Banana；prompt 全文或指向 prompt 範本的哪一段>
- 風格基準圖：<本物件就是基準／art/source/style_anchor/…>
- 生成方式：圖片生 3D／多視角生 3D
- 3D 模型版本：<…>
- Task ID：<…>
- Seeds：model <…> / texture <…>
- 後處理：smart_lowpoly 3000 / convert GLTF 1024
- Blender 修改：<…>
- 最終三角面數／貼圖：<…>
- 使用點數：<…>
- 授權：<付費方案名稱；確認可商用>
```

## 10. 授權與成本

### 10.1 授權

- **API（開發者平台）：** [服務條款](https://developers.tripo3d.ai/en/terms) 3.2 節寫明，產出的模型可以用於合法的商業或非商業用途。但 Tripo **不保證產出是獨一無二的**，其他使用者可能得到相似的結果，所以招牌角色或商標類的造型不要只依賴 AI 生成。
- **Tripo Studio（網頁版）：** 第三方整理的資料指出免費方案的模型是公開的（CC BY 4.0）、不能商用，付費方案才有私人模型與商業授權。這部分的官方條款在 `www.tripo3d.ai`，**目前還沒核對**，用 Studio 生成正式資產前請先確認。
- 不論用哪個管道，都要在資產紀錄寫上使用的管道與方案。

### 10.2 點數價格

**網頁版：** 點數另計，以介面顯示為準。2026-10-23 的截圖中，Image 分頁用 Nano Banana 產生 4 張圖顯示 40 點（約每張 10 點）。

**API（2026-10-21 官方定價）：**

1 點 = 0.01 美元，從 1 美元起購；**失敗或取消的任務不扣點**。

| 項目 | 點數 |
|---|---:|
| 文生圖（`seedream_v4`／`seedream_v5`） | 5 |
| 圖片轉多視角 | 10 |
| P1 圖生 3D（含標準貼圖）／多視角生 3D | 50／50 |
| H3.1 圖生 3D（含標準貼圖）＋智慧低面數 | 30 + 10 |
| P2 Preview 圖生 3D（含標準貼圖） | 110 |
| 重新上貼圖（標準） | 10 |
| 格式轉換（基本／含自訂參數） | 5／10 |
| 重新拓撲（v3.0 三角面） | 35 |

### 10.3 每道料理的預算估計

以牛肉麵為例（5 種 Tripo 物件：牛肉塊 ×2 造型、麵條團 ×2 造型、青江菜；麵碗也用 Tripo）：

| 項目 | 每個物件 | 6 個物件合計 |
|---|---:|---:|
| 參考圖（API 每張 5 點，2 批共 8 張） | 40 | 240 |
| P1 候選 3 次 | 150 | 900 |
| 格式轉換 | 10 | 60 |
| 預留重新上貼圖 1 次 | 10 | 60 |
| **合計** | **210** | **約 1,260 點 ≈ 13 美元** |

需要多視角的物件每個再加約 10 點。改用 H3.1 + 智慧低面數，候選 3 次是 120 點，可以再省約 25%。參考圖多試幾批的成本很低，3D 候選次數才是預算的大頭，所以參考圖把關越嚴，越省。

## 11. 新增一道料理的快速檢查

1. 填拆件表 → 給企劃和關卡確認。
2. 用 [prompt 範本](tripo3d_prompt範本.md) 的「AI 助手 prompt」產生所有參考圖 prompt 與 3D 設定。
3. 先做風格基準物件的參考圖並定案（沿用專案既有基準圖時跳過）。
4. 其他物件上傳基準圖產生參考圖，每張都通過 3.4 的檢查。
5. 每個物件跑 ③–⑦。
6. 組裝料理場景，跑一次物理和湯的測試。
7. 寫資產紀錄，提交（二進位檔透過 Git LFS）。

## 12. Tripo 網頁版操作對照（持續補充）

網頁版的介面依使用者提供的截圖整理，**標「待確認」的項目還沒實際看過**。確認後請更新本節。

| 左側分頁 | 對應流程 | 已確認 | 待確認 |
|---|---|---|---|
| **Image** | ② 參考圖 | Prompt 輸入框（上限 10,000 字元，沒有負面欄位）、Generation Model（Nano Banana；GPT Image 2.5 需升級）、Aspect Ratio（1:1／16:9／9:16／4:3／3:4）、Number of Images（1–4）、4K Resolution 開關；產生 4 張顯示 40 點 | 輸入框左下角圖片按鈕是否為上傳參考圖；Templates 的用途 |
| **Model** | ③ 圖片生成 3D | — | 如何把 Image 分頁的結果直接帶過來；模型版本選項名稱（P1／H3.1）；面數上限、貼圖品質、PBR、去除光影（delight）、智慧低面數的對應選項；多視角輸入；seed 是否顯示 |
| **Segment** | 4.4 整盤切割（不建議） | — | — |
| **Retopo** | ④ 重新拓撲 | — | 面數設定、三角面／四邊面選項 |
| **Smart UV** | ④ Smart UV | — | — |
| **Texture** | ④ 重新上貼圖 | — | 是否能指定貼圖模型版本與去除光影 |
| **Rig** | 不使用 | — | — |
| 下載／匯出 | ④ 轉檔 | — | 能否選 GLB、貼圖尺寸、原點到底部中心、底部壓平 |

Studio（網頁版）的授權條款也還沒核對，見 10.1。

---

**參考資料**
- [Tripo 開發者文件](https://developers.tripo3d.ai/en/docs/introduction)（官方，2026-10-21 核對）：[模型與版本](https://developers.tripo3d.ai/en/docs/models-and-versions)、[圖生 3D（P 系列）](https://developers.tripo3d.ai/en/docs/generation-image-to-model/p)、[圖生 3D（H 系列）](https://developers.tripo3d.ai/en/docs/generation-image-to-model/standard)、[多視角生 3D](https://developers.tripo3d.ai/en/docs/generation-multiview-to-model/p)、[格式轉換](https://developers.tripo3d.ai/en/docs/models-convert)、[重新拓撲](https://developers.tripo3d.ai/en/docs/mesh-decimate)、[計費](https://developers.tripo3d.ai/en/docs/billing)
- [Tripo API 定價](https://developers.tripo3d.ai/en/pricing)、[Tripo API 服務條款](https://developers.tripo3d.ai/en/terms)（官方）
- [Tripo Python SDK API 文件（官方）](https://github.com/VAST-AI-Research/tripo-python-sdk/blob/master/docs/API.md)：參數名稱與可用值
- [Tripo Smart Mesh 功能頁](https://www.tripo3d.ai/features/smart-mesh)、[Tripo 低面數生成頁](https://www.tripo3d.ai/features/low-poly-3d-model-generator)
- [Tripo：如何在 Godot 使用 AI 3D 模型](https://www.tripo3d.ai/blog/how-to-use-ai-3d-models-in-godot)
- [Tripo 定價頁](https://www.tripo3d.ai/pricing)、[CostBench：Tripo 免費方案整理](https://www.costbench.com/software/ai-3d-generation/tripo-ai/free-plan/)
- [3D AI Studio：Tripo API 文件](https://www.3daistudio.com/Platform/API/Documentation/3d-generation/tripo)
