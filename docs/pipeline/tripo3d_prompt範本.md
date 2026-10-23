# Tripo3D Prompt 範本

**配套流程：** [`tripo3d_料理建模流程.md`](tripo3d_料理建模流程.md)

圖像生成工具與 Tripo 對英文 prompt 的理解通常比較好，所以 prompt 本體用英文，說明用中文。`{大括號}` 是要替換的欄位。

> **標準做法是「先產生參考圖，再用圖片生成 3D」**（流程文件第 0 節原則 4）。本文件的主要 prompt 都是**產生參考圖用**；文字直接生 3D 的 prompt 只保留在第 4 節做比較用，不用於正式資產。

## 0. 先看你用哪個管道

| 管道 | 負面描述（Negative）欄位 | prompt 長度 | 用哪些區塊 |
|---|---|---|---|
| **Tripo 網頁版 Image 分頁**（主要） | **沒有**（2026-10-23 依介面截圖確認） | 介面顯示上限 10,000 字元 | `STYLE` + 物件描述 + `SHOT` + `ISOLATE` |
| Tripo API（`/v3/generation/text-to-image`） | 依圖像模型而定 | 依圖像模型而定 | 同上；`NEGATIVE` 只在有欄位時另外填 |
| 其他圖像生成工具 | 依工具而定 | 依工具而定 | 同上；有負面欄位才填 `NEGATIVE` |

**沒有負面欄位時，不要把負面描述接在 prompt 後面。** 圖像模型看到 `plate, bowl, table, chopsticks` 這些詞，反而可能把它們畫出來。要排除的東西，一律改寫成正面描述（`ISOLATE` 區塊）。

---

## 1. 共用區塊（每個 prompt 都要用，不要改）

### 1.1 風格描述 `STYLE`

```text
cute stylized 3D game asset, toy-like, soft clay and matte vinyl look, chunky rounded shapes,
softened edges, slightly exaggerated proportions, simple clean silhouette, hand-painted soft
colors, gentle color gradients, minimal surface detail, smooth clean surfaces, matte finish
with soft subtle highlight
```

> 意思：可愛 Q 版、玩具感、黏土或霧面軟膠質感、圓潤厚實、邊角柔和、比例略誇張、輪廓簡潔、手繪柔和配色、少量細節、表面乾淨、霧面。對應企劃書 4.1。

### 1.2 構圖與光線 `SHOT`

```text
centered, fully visible, filling about 75% of the frame, 3/4 top-down view at 30 degrees,
on a plain pure white background, soft even studio lighting, shadowless
```

### 1.3 隔離描述 `ISOLATE`（用正面描述排除其他東西）

**食物用：**
```text
the {物件英文名} is the only object in the image, isolated and floating alone on the white
background
```

**容器用：**
```text
the empty {容器英文名} is the only object in the image, clean and completely empty inside,
isolated on the white background
```

### 1.4 負面描述 `NEGATIVE`（只在有負面欄位時使用）

```text
photorealistic, photo scan, greasy, glossy oil, wet shine, noisy texture, dirt, burnt,
multiple objects, plate, bowl, table, chopsticks, hands, background, steam, text, logo,
watermark, cropped, blurry, low quality
```

> 生成容器時拿掉 `plate, bowl`，改加 `food, soup, liquid`。Tripo API 的 `negative_prompt` 上限 255 字元；上面約 200 字元。

### 1.5 玩具收尾 `TOY`（每個物件描述的最後一句）

```text
Rendered like a hand-sculpted clay toy of {物件英文名}, simplified shapes, flat painted colors,
dull matte surface, simplified soft grain.
```

> 為什麼需要：物件描述寫得越細（撕裂邊緣、纖維、醬汁），圖像模型越往寫實走，`STYLE` 會被蓋過。2026-10-23 牛肉塊 A 的試做中，沒有 `TOY` 時產出的是帶濕亮醬汁的寫實美食照；加上 `TOY` 並換成 GPT Image 2 之後才回到黏土玩具感。位置：放在物件描述之後、`ISOLATE` 之前。`simplified soft grain` 只適用有紋理的食物；沒有紋理的物件（碗、麵條團）刪掉這三個字。

---

## 2. 參考圖 prompt（步驟 ②）

### 2.1 食物範本

```text
{STYLE}.
A single {物件英文名} ({物件說明}): {造型重點}, {顏色重點}, {底部描述}. {TOY}
{ISOLATE（食物用）}, {SHOT}.
```

| 欄位 | 寫法 | 例子 |
|---|---|---|
| 物件英文名 | 具體的名詞 | `braised beef chunk` |
| 物件說明 | 一句話描述它在料理中的樣子 | `from Taiwanese beef noodle soup` |
| 造型重點 | 2–3 個能被認出來的特徵 | `irregular rounded cube shape, a soft tendon layer on one side` |
| 顏色重點 | 主色 + 輔色，寫出明度 | `warm reddish brown with a lighter beige tendon stripe` |
| 底部描述 | 平底或圓底（影響物理） | `flat stable bottom` 或 `rounded bottom` |

### 2.2 容器範本

```text
{STYLE}.
A single empty {容器英文名}: {造型重點}, thick rounded rim, smooth inner surface clearly visible,
{顏色與花紋}, flat stable base.
{ISOLATE（容器用）}, {SHOT}.
```

### 2.3 用風格基準圖產生其他物件（流程文件 3.2）

每道料理的第一個物件做好之後，就是**風格基準圖**。之後的物件都要**上傳風格基準圖當參考**，並在 prompt 最前面加上這段：

```text
Match the art style of the reference image exactly: same materials, same color saturation,
same lighting, same level of detail and the same degree of roundness. Do not copy its shape;
create a different object as described below.
```

後面接 2.1 或 2.2 的完整 prompt。

> Tripo 網頁版 Image 分頁的輸入框左下角有圖片按鈕，應該就是上傳參考圖的地方；實際行為還沒確認，見流程文件第 12 節。

### 2.4 多視角（背面形狀複雜時）

**建議做法：** 正面圖挑好之後，用 Tripo 的「圖片轉多視角」（API：`POST /v3/generation/image-to-multiview`，10 點）自動產生四個視角，不需要另外寫 prompt；某個視角不對時，用 Edit Multiview（每張 5 點）修正。

如果用其他圖像工具，以正面圖為參考，用這段 prompt 生成其他視角：

```text
the same object as the reference image, identical style, size, colors and lighting,
{view} view, orthographic camera, on a plain pure white background, shadowless
```

`{view}` 依序填 `left side`、`back`、`right side`。四張圖的物件大小要一致；不一致就重新生成。多視角生 3D 至少要 2 張（正面必填）。

### 2.5 寫物件描述的經驗（2026-10-23，牛肉塊 A 試做 5 輪的結論）

**固定圖像模型。** 整個專案用 **GPT Image 2**。同一份 prompt，GPT Image 2.5 會變得濕亮、像焦糖；GPT Image 2 偏霧面黏土。

**避開會被誤判成其他食物的詞：**

| 不要寫 | 會變成 | 改寫成 |
|---|---|---|
| `cube`、`rectangular` | 骰子、積木 | `thick chunky piece`、`plump rounded block` + `lumpy`、`uneven` |
| `tendon stripe`、`band`、`layer` | 繞一圈的緞帶、千層糕 | `a few thin light-tan tendon lines on the wide cut face`（寫位置，用 `thin lines`） |
| `flower shape`、`inset`、`jelly`、`amber` | 焦糖、糖果頂飾 | 不要把肌腱寫成裝飾圖案 |
| `mahogany` | 巧克力 | `soy-braised brown` |
| `reddish brown`（單獨使用） | 生肉、培根 | `deep reddish brown` 搭配 `soy-braised brown` 的外皮 |
| `fibrous edges`、`torn-looking`、`glossy` | 木紋、寫實濕亮美食照 | `simplified soft grain` + 第 1.5 節的 `TOY` |

**其他原則：**

1. 細節用「位置 + 尺寸」限定（`on the wide cut face`、`thin`），不要用抽象名詞。
2. 每次只改一個變因（模型、顏色或形狀擇一），才看得出是哪個改動有效。
3. 選圖時多問一句「它還像什麼？」（糖果、培根、麵包、積木），有就不合格。
4. 底部在 3/4 視角看不到，選圖後在 3D 預覽階段確認；必要時 prompt 加 `flat bottom resting on the ground`。
5. 基準物件選「穩定、單純」的造型，不一定選最有魅力的（見第 5.1 節）。

---

## 3. Tripo 重新上貼圖 prompt（貼圖重生成的文字提示）

```text
{STYLE}, {物件英文名}, {顏色重點}, flat hand-painted albedo colors, even lighting,
evenly lit surface without baked shadows or highlights
```

> 用途：模型造型滿意，但貼圖有烘進去的陰影、太寫實或太油時使用。先試試把貼圖模型設為 `v3.5-20260815` 並開啟 `delight`（去除參考圖的光影），通常就能解決陰影問題。
>
> **顏色太單調時**（牛肉塊 A 的外皮變成一片橘色），在文字提示的 `{顏色重點}` 寫出深淺：`subtle darker crevices and slightly lighter bumps`，並加上 `soft color variation`。**不要關掉 Remove Lighting**，否則參考圖的光影會烘進貼圖，食物翻面時陰影方向會錯。還是太平，就到 Blender 修色，並烘一層 AO（環境光遮蔽不依賴光的方向，可以安全烘進貼圖）。
>
> **看顏色時用 Tripo 預覽的 Unlit 模式**：有光照的預覽會被 Tripo 的燈光染色，不是貼圖的真實顏色；Unlit 看到的才是貼圖本身。

## 4. 文字直接生 3D（僅供比較，不用於正式資產）

想比較「文字生 3D」和「圖片生 3D」的差異時才用。正式資產一律走圖片路線，因為文字生 3D 會在內部自動產生一張你看不到的圖，每次的風格都不一樣。

```text
{STYLE}, a single {物件英文名}, {造型重點}, {顏色重點}, {底部描述},
isolated single object, game-ready low poly prop, closed watertight mesh, solid object
```

有負面欄位才填 `NEGATIVE`。

---

## 5. 範例：牛肉麵（beef_noodle_soup）

### 5.1 拆件表

| # | 物件 ID | 中文名 | 類型 | 數量 | 尺寸（cm） | 生成方式 | 碰撞 | 密度 | 進湯 | 掛點面 |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | bowl_noodle | 麵碗 | 容器 | 1 | 18×18×8 | Tripo 圖生（或 Blender 旋轉成形） | 凹面 `-colonly` | — | — | — |
| 2 | food_beef_chunk_a／_b | 牛肉塊（2 種造型） | 食物 | 3 | 4×3×2.5 | Tripo 圖生 | 凸包 ×1 | 1.1 | 是 | Top／Side／Bottom |
| 3 | food_noodle_clump_a／_b | 麵條團（2 種造型） | 食物 | 2–3 | 6×5×2 | Tripo 多視角 | 凸包 ×2 | 1.08 | 是 | Top／Bottom |
| 4 | food_bok_choy | 青江菜 | 食物 | 2 | 7×3×1.5 | Tripo 圖生 | 凸包 ×2 | 0.9 | 是 | Side |
| 5 | decoy_scallion | 蔥花 | 誘餌 | 6–10 | 0.6×0.6×0.3 | Blender 手工 | 凸包 ×1 | 0.7 | 是 | — |
| 6 | cilantro_* | 香菜 | 目標 | — | — | 共用模型 | — | 0.6／1.05 | 是 | — |

湯：牛肉湯預設，混濁度 0.6，液面高度在碗高的 70%。

**風格基準物件：牛肉塊 A。** 它的造型最單純、最容易做好，做好之後其他物件都以它的圖為參考。

### 5.2 參考圖 prompt（可以直接貼進 Tripo 網頁版 Image 分頁）

**牛肉塊 A（風格基準物件，不需要上傳參考圖）**
```text
cute stylized 3D game asset, toy-like, soft clay and matte vinyl look, chunky rounded shapes,
softened edges, slightly exaggerated proportions, simple clean silhouette, hand-painted soft
colors, gentle color gradients, minimal surface detail, smooth clean surfaces, matte finish
with soft subtle highlight.
A single braised beef chunk (from Taiwanese beef noodle soup): a thick chunky piece of
slow-braised beef with a lumpy rounded outline, a matte soy-braised brown crust with a few soft
rounded bumps, one wide cut face showing a few soft parallel muscle grain lines in deep
reddish brown and a few thin light-tan tendon lines, flat stable bottom. Rendered like a
hand-sculpted clay toy of braised beef, simplified shapes, flat painted colors, dull matte
surface, simplified soft grain.
The braised beef chunk is the only object in the image, isolated and floating alone on the
white background, centered, fully visible, filling about 75% of the frame, 3/4 top-down view
at 30 degrees, on a plain pure white background, soft even studio lighting, shadowless.
```

> 這是 2026-10-23 試做 5 輪後定案的版本（圖像模型：GPT Image 2）。前幾輪的失敗原因（變成緞帶、巧克力、寫實美食照）見第 2.5 節。選用的基準圖：第 5 輪的第 1 張（長方塊、切面兩條細肌腱）；它醬色外皮偏橘，之後用貼圖修色即可，不必重畫。

以下物件都要**上傳牛肉塊 A 的圖當參考**，並在最前面加上 2.3 的風格參考段落。每個物件描述的最後都要接第 1.5 節的 `TOY`（下面的範例已寫入）。

**麵條團**（正面圖挑好後，再做多視角）
```text
{2.3 風格參考段落}
{STYLE}.
A single clump of thick wheat noodles (from Taiwanese beef noodle soup): loosely coiled into a
soft oval nest, noodles simplified into a few thick smooth rounded strands that merge together,
creamy pale yellow with slightly darker strand gaps, flat bottom. Rendered like a hand-sculpted
clay toy of a noodle clump, simplified shapes, flat painted colors, dull matte surface.
The clump of noodles is the only object in the image, isolated and floating alone on the white
background, {SHOT}.
```

**青江菜**
```text
{2.3 風格參考段落}
{STYLE}.
A single baby bok choy cut in half lengthwise: thick pale green-white stem at the bottom fanning
into a few broad rounded dark green leaves at the top, clear stem and leaf separation, flat cut
side facing down. Rendered like a hand-sculpted clay toy of baby bok choy, simplified shapes,
flat painted colors, dull matte surface.
The baby bok choy is the only object in the image, isolated and floating alone on the white
background, {SHOT}.
```

> 青江菜的葉子是寬大圓潤的形狀，和香菜（扇形分叉、波浪邊緣的小葉）明顯不同，符合企劃書的辨識度要求。

**麵碗**
```text
{2.3 風格參考段落}
{STYLE}.
A single empty deep ceramic noodle bowl: wide round opening, gently curved walls, thick rounded
rim, smooth inner surface clearly visible, off-white glaze with a simple blue band pattern near
the rim, flat stable base. Rendered like a hand-sculpted clay toy of a noodle bowl, simplified
shapes, flat painted colors, dull matte surface.
The empty noodle bowl is the only object in the image, clean and completely empty inside,
isolated on the white background, {SHOT}.
```

### 5.3 生成 3D 的設定

共同參數：`texture: true`、`pbr: false`、`texture_quality: "standard"`、`texture_version: "v3.5-20260815"`、`delight: true`；不設定 `export_orientation`。網頁版上對應的選項名稱見流程文件第 12 節。

| 物件 | 方式 | `model` | `face_limit` | 備案 | Convert（`format: "GLTF"`） |
|---|---|---|---|---|---|
| 牛肉塊 | 圖片生 3D | `P1-20260311` | 3000 | `v3.1-20260211` + `smart_low_poly: true` | `texture_size: 512`、`pivot_to_center_bottom: true` |
| 麵條團 | 正面圖 → 圖片轉多視角 → 多視角生 3D | `P1-20260311` | 3000 | 同上 | `texture_size: 512`、`pivot_to_center_bottom: true` |
| 青江菜 | 圖片生 3D | `P1-20260311` | 3000 | 同上 | `texture_size: 512`、`pivot_to_center_bottom: true`、`flatten_bottom: true` |
| 麵碗 | 圖片生 3D | `P1-20260311` | 5000 | 同上，或 Blender 旋轉成形 | `texture_size: 1024`、`pivot_to_center_bottom: true`、`flatten_bottom: true` |

預估點數見流程文件 10.3。

> **網頁版（Smart Mesh 分頁）的實際操作**（2026-10-23 牛肉塊 A）：AI Model 選 **P1.0 – Fast**（35 點）、Topology 選 Triangle、Polycount 3000。網頁版的幾何與貼圖是**兩個步驟**：先生成幾何，滿意後才按 Texture（20 點）。詳見流程文件第 4.3b 節與第 12 節。

---

## 6. AI 助手 prompt：新增一道料理

把下面整段貼給 AI 助手（Claude 等），填上 `{料理名稱}` 與 `{料理描述}`，它會產出拆件表、所有參考圖 prompt 與 Tripo 設定。產出後要給企劃和關卡設計確認拆件表。

````text
你是《香菜退散！》的 3D 資產規劃師。這是一款 Godot 4.5 的 Q 版休閒遊戲：玩家把料理中的食物拿起、
翻面、找出香菜並挑掉。每個食物都是會依物理落下、滾動、停穩的剛體；湯由 shader 呈現，不建模。

請為以下料理規劃 Tripo3D 建模：
- 料理名稱：{料理名稱}
- 料理描述：{料理描述，例如「台灣的肉圓，Q 彈外皮，淋上紅色甜辣醬，盛在小碟中」}
- 在關卡中的用途：{例如「第二章新料理；要有 2 個以上可以翻面檢查的食物」}
- 既有的風格基準圖：{有／沒有。有的話寫出是哪一道料理的哪個物件}

請依照以下規則：
1. 把料理拆成「可以各自拿起的物件」。每個物件一次生成、一個 .glb。容器是空的、固定不動。
   液體（湯、醬汁）不建模，寫成 shader 需求。
2. 又薄又小的葉片（香菜、蔥花、碎葉、海苔）標為「Blender 手工」，不用 Tripo。
3. 每個物件寫出真實尺寸（cm）、密度（g/cm³，水 = 1.0）、是否平底、碰撞形狀（凸包數量，或容器用凹面）、
   香菜可以附著的面（Top／Side／Back／Bottom）。
4. 列出可以重用的既有資產：麵碗、湯碗、盤子、醬碟、青菜、共用香菜。
5. 所有物件都走「先產生參考圖，再用圖片生成 3D」。不要提供文字直接生 3D 的 prompt。
6. 指定一個「風格基準物件」：沒有既有基準圖時，選造型最單純的物件；有的話沿用既有基準圖。
   基準物件之外的每個物件，都要註明「上傳風格基準圖當參考」，並在 prompt 最前面加上：
   "Match the art style of the reference image exactly: same materials, same color saturation,
   same lighting, same level of detail and the same degree of roundness. Do not copy its shape;
   create a different object as described below."
7. 每個 Tripo 物件寫出完整的英文參考圖 prompt，格式為：STYLE. 物件描述. TOY ISOLATE, SHOT.
   物件描述包含物件名、造型重點 2–3 個、顏色與明度、底部形狀。
   描述的用詞限制（避免模型誤判成別的食物）：
   - 不寫 cube、rectangular、stripe、band、layer、flower、inset、jelly、amber、mahogany、
     fibrous、glossy；肉色用 deep reddish brown 與 soy-braised brown，不要單獨寫 reddish brown。
   - 肌腱、紋路這類細節要寫位置與尺寸，例如 "a few thin light-tan lines on the wide cut face"。
   - 每個物件描述的最後都要接 TOY，否則會變成寫實照片。
   - 整個專案固定用 GPT Image 2 產生參考圖。
   STYLE、SHOT、TOY 一字不改地使用以下內容：
   STYLE = "cute stylized 3D game asset, toy-like, soft clay and matte vinyl look, chunky rounded
   shapes, softened edges, slightly exaggerated proportions, simple clean silhouette,
   hand-painted soft colors, gentle color gradients, minimal surface detail, smooth clean
   surfaces, matte finish with soft subtle highlight"
   SHOT = "centered, fully visible, filling about 75% of the frame, 3/4 top-down view at 30 degrees,
   on a plain pure white background, soft even studio lighting, shadowless"
   TOY = "Rendered like a hand-sculpted clay toy of {物件英文名}, simplified shapes, flat painted
   colors, dull matte surface, simplified soft grain."（沒有紋理的物件刪掉 simplified soft grain）
   ISOLATE（食物）= "the {物件英文名} is the only object in the image, isolated and floating alone
   on the white background"
   ISOLATE（容器）= "the empty {容器英文名} is the only object in the image, clean and completely
   empty inside, isolated on the white background"
   Tripo 網頁版沒有負面描述欄位，所以**不要**輸出 Negative 段落，也不要在 prompt 中列出不要的東西
   （例如 plate, table, chopsticks）；要排除的東西一律用正面描述表達。
8. 檢查辨識度：任何綠色的物件都要說明它和香菜（扇形分叉、波浪葉緣、細葉柄的小葉）在輪廓上有什麼不同。
9. 背面形狀複雜的物件標註「需要多視角」（正面圖 → 圖片轉多視角 → 多視角生 3D）。
10. 每個物件列出生成 3D 的設定：model（首選 P1-20260311；備案 v3.1-20260211 + smart_low_poly）、
   face_limit（食物 3000、容器 5000）、Convert 參數（GLTF、texture_size 512 或 1024、
   pivot_to_center_bottom、flatten_bottom 是否開啟）。共同參數固定為 texture true、pbr false、
   texture_quality standard、texture_version v3.5-20260815、delight true，不設定 export_orientation。
11. 依官方 API 定價估算點數（1 點 = 0.01 美元）：每批參考圖 4 張、P1 圖生 3D 50、H3.1 圖生 3D 30 +
   智慧低面數 10、圖片轉多視角 10、格式轉換 10、重新上貼圖 10；每個物件以 3 次 3D 候選計算。
   網頁版的點數另計，以介面顯示為準。

輸出格式：
## 料理拆件表：{料理名稱}
（表格，欄位：# / 物件 ID / 中文名 / 類型 / 數量 / 尺寸 cm / 生成方式 / 碰撞 / 密度 / 進湯 / 掛點面）
## 風格基準物件
## 液體與 shader 需求
## 重用資產
## 辨識度檢查
## 參考圖 prompt（每個物件一段，依製作順序排列，基準物件放第一個）
## 生成 3D 設定表
## 點數預估
## 風險與注意事項（例如可能生成失敗的造型、需要手工修正的地方）

物件 ID 用 snake_case：容器 bowl_／plate_／dish_ 開頭，食物 food_，誘餌 decoy_；
同一種食材的不同造型加 _a、_b。
````

---

## 7. 常見問題與調整方式

| 問題 | 調整方式 |
|---|---|
| 圖中出現盤子、桌子、筷子 | 確認 prompt 裡沒有列出這些詞（包括負面描述）；加強 `ISOLATE` 描述 |
| 太寫實、太油亮 | 確認有加第 1.5 節的 `TOY`；圖像模型改回 GPT Image 2（2.5 會濕亮）；改用風格基準圖當參考 |
| 變成巧克力、糖果、培根、緞帶、骰子 | 查第 2.5 節的「避開的詞」表；肌腱不要寫成 stripe、band、flower |
| 貼圖顏色單調、外皮一整片單色 | 見第 3 節：顏色重點寫出深淺並加 `soft color variation`；先用 Unlit 預覽確認是貼圖還是預覽的問題；不要關 Remove Lighting |
| 細節糊成一團（例如麵條） | 在描述中**主動簡化**：`simplified into a few thick strands`，不要要求細節 |
| 底部不平、放不穩 | 描述加 `flat stable bottom`；轉檔時開 `flatten_bottom` |
| 同一道料理風格不一致 | 確認每個物件都上傳了風格基準圖，並加了 2.3 的風格參考段落；所有物件用同一個圖像模型 |
| 綠色食材和香菜太像 | 改輪廓（寬葉、圓葉、管狀），並拉開明度差；不要只改顏色 |
| 參考圖好看，但 3D 結果差 | 參考圖的視角改成更正面、物件更完整；背面複雜就改用多視角 |
| H3.1 的 smart_low_poly 失敗 | 失敗不扣點；改用 P1，或關掉 smart_low_poly 生成後用 Retopology 減面 |
| 貼圖有烘進去的陰影 | 參考圖改成 `shadowless`；`texture_version: "v3.5-20260815"` 加 `delight: true`；還是不行再用第 3 節重新上貼圖 |
