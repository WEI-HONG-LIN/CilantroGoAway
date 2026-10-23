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
cute stylized 3D game asset, toy-like, soft clay look, chunky rounded shapes, slightly
exaggerated proportions, simple clean silhouette, hand-painted colors, matte finish
```

> 意思：可愛 Q 版、玩具感、黏土質感、圓潤厚實、比例略誇張、輪廓簡潔、手繪配色、霧面。對應企劃書 4.1。
>
> **2026-10-23 修改（決策 D-20261023-04）：** 舊版寫了 `smooth clean surfaces, minimal surface detail, soft subtle highlight`，和風格基準圖（牛肉塊 A：表面有燉煮的凹凸與肌理、深色、霧面）互相矛盾，產生的圖會變得光滑、偏亮、像軟膠玩具。表面細節改由每個物件的「表面質感」欄位描述（2.1）。

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

---

## 2. 參考圖 prompt（步驟 ②）

### 2.1 食物範本

```text
{STYLE}.
A single {物件英文名} ({物件說明}): {造型重點}, {表面質感}, {顏色重點},
dull matte surface without shine, {底部描述}.
{ISOLATE（食物用）}, {SHOT}.
```

| 欄位 | 寫法 | 例子 |
|---|---|---|
| 物件英文名 | 具體的名詞 | `braised beef chunk` |
| 物件說明 | 一句話描述它在料理中的樣子 | `from Taiwanese beef noodle soup` |
| 造型重點 | 2–3 個能被認出來的特徵 | `a thick flattened wedge-shaped slab, rounded edges` |
| 表面質感 | 和基準圖同等級的細節；用「a few」「subtle」「gentle」控制程度（2.3） | `slightly uneven with a few gentle braised bumps and subtle muscle fiber lines` |
| 顏色重點 | 主色 + 輔色，寫出明度 | `deep dark reddish brown, the tendon a muted amber beige` |
| 底部描述 | 平底或圓底（影響物理） | `flat stable bottom` 或 `rounded bottom` |

### 2.2 容器範本

```text
{STYLE}.
A single empty {容器英文名}: {造型重點}, thick rounded rim, smooth inner surface clearly visible,
{顏色與花紋}, flat stable base.
{ISOLATE（容器用）}, {SHOT}.
```

### 2.3 用文字對齊風格基準圖（流程文件 3.2）

Tripo 網頁版 Image 分頁**不能上傳參考圖**（2026-10-23 確認），所以基準物件以外的物件，靠文字把質感寫得和基準圖一樣：

1. **表面質感**：基準圖（牛肉塊 A）是「微微不平、少量柔和凸起、細肌理」。其他物件寫同等級的細節，例如 `slightly uneven`、`a few subtle vein lines`。
2. **顏色**：偏深、偏沉的自然色，不要亮橘、亮綠；寫 `deep`、`muted`。
3. **霧面**：一律加 `dull matte surface without shine`。
4. **不要寫過頭**：`lumpy`、`knobbly`、`many bumps` 這類詞會讓整個物件被凹凸蓋過，連造型都跑掉（牛肉塊 B 第 2 版的教訓）。
5. **一次只改一個地方**：風格對了但比例不對（例如筋太寬）時，只改那一句，其他字不動。
6. 文字試 3 批還對不齊，改用能上傳參考圖的工具（流程文件 3.2 第 4 點）。

### 2.4 多視角（背面形狀複雜時）

**建議做法：** 正面圖挑好之後，用 Tripo 的「圖片轉多視角」（API：`POST /v3/generation/image-to-multiview`，10 點）自動產生四個視角，不需要另外寫 prompt；某個視角不對時，用 Edit Multiview（每張 5 點）修正。

如果用其他圖像工具，以正面圖為參考，用這段 prompt 生成其他視角：

```text
the same object as the reference image, identical style, size, colors and lighting,
{view} view, orthographic camera, on a plain pure white background, shadowless
```

`{view}` 依序填 `left side`、`back`、`right side`。四張圖的物件大小要一致；不一致就重新生成。多視角生 3D 至少要 2 張（正面必填）。

---

## 3. Tripo 重新上貼圖 prompt（貼圖重生成的文字提示）

```text
{STYLE}, {物件英文名}, {顏色重點}, flat hand-painted albedo colors, even lighting,
evenly lit surface without baked shadows or highlights
```

> 用途：模型造型滿意，但貼圖有烘進去的陰影、太寫實或太油時使用。先試試把貼圖模型設為 `v3.5-20260815` 並開啟 `delight`（去除參考圖的光影），通常就能解決陰影問題。

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
| 1 | bowl_noodle | 麵碗 | 容器 | 1 | 18×18×8 | Blender 旋轉成形（已完成） | 凹面 `-colonly` | — | — | — |
| 2 | food_beef_chunk_a／_b | 牛肉塊（A 圓潤方塊、B 扁楔形） | 食物 | 3 | 4×3×2.5 | Tripo 圖生 | 凸包 ×1 | 1.1 | 是 | Top／Side／Bottom |
| 3 | food_noodle_clump_a／_b | 麵條團（2 種造型） | 食物 | 2–3 | 6×5×2 | Tripo 多視角 | 凸包 ×2 | 1.08 | 是 | Top／Bottom |
| 4 | food_bok_choy_leaf_a／_b | 青江菜葉（A 大外葉、B 小內葉；單片，不是整把） | 食物 | 2 | 8×4×1.2 | Tripo 圖生 | 凸包 ×2 | 0.9 | 是 | Top／Bottom |
| 5 | decoy_scallion | 蔥花 | 誘餌 | 6–10 | 0.6×0.6×0.3 | Blender 手工 | 凸包 ×1 | 0.7 | 是 | — |
| 6 | cilantro_* | 香菜 | 目標 | — | — | 共用模型 | — | 0.6／1.05 | 是 | — |
| 7 | bowl_soup_small | 小湯碗（1-6 套餐的小碗牛肉湯） | 容器 | 1 | 12×12×6 | Blender，麵碗縮放（已完成） | 凹面 `-colonly` | — | — | — |
| 8 | deco_noodle_strands | 裝飾散麵（掛在麵條團與碗緣，不能互動） | 裝飾（固定） | 3–5 | 長 8–12，粗 0.5 | Blender 沿曲線手工 | 無 | — | — | — |

湯：牛肉湯預設，混濁度 0.6，液面高度在碗高的 70%。

麵條維持「麵條團」，不做單根可互動的麵條（2026-10-23 使用者確認，維持 D-20261020-02）；散麵只是裝飾，單根軟麵列為 MVP 後的擴充。

**風格基準物件：牛肉塊 A**（`art/source/style_anchor/beef_noodle_soup_beef_chunk_a.png`，GPT Image 2）。全遊戲的風格都以它為準。

### 5.2 參考圖 prompt（可以直接貼進 Tripo 網頁版 Image 分頁，Generation Model 選 GPT Image 2）

**牛肉塊 A（風格基準物件）**：用舊版 `STYLE` 產生，prompt 不再使用；之後要重做 A 時，用牛肉塊 B 的 prompt 把造型改回「irregular rounded cube shape, one flat cut face showing dark red muscle fibers with thin pale beige tendon lines」。

**牛肉塊 B**（2026-10-23 定案）
```text
cute stylized 3D game asset, toy-like, soft clay look, chunky rounded shapes, slightly
exaggerated proportions, simple clean silhouette, hand-painted colors, matte finish.
A single braised beef chunk (from Taiwanese beef noodle soup): a thick flattened wedge-shaped
slab, wider at one end and tapering to the other, rounded edges, one thin narrow strip of soft
translucent tendon near one edge of the top surface, the tendon strip only about one fifth of the
chunk's width, the meat clearly dominant, the outer surface slightly uneven with a few gentle
braised bumps and subtle muscle fiber lines, deep dark reddish brown like slow-braised beef,
the tendon a muted amber beige, dull matte surface without shine, flat stable bottom.
The braised beef chunk is the only object in the image, isolated and floating alone on the
white background, centered, fully visible, filling about 75% of the frame, 3/4 top-down view
at 30 degrees, on a plain pure white background, soft even studio lighting, shadowless.
```

**青江菜葉 A**（B 把 `a large outer leaf` 改成 `a small tender inner leaf, shorter and narrower`）
```text
cute stylized 3D game asset, toy-like, soft clay look, chunky rounded shapes, slightly
exaggerated proportions, simple clean silhouette, hand-painted colors, matte finish.
A single bok choy leaf separated from the bunch, a large outer leaf (from Taiwanese beef noodle
soup): one thick spoon-shaped pale celadon green-white stalk at the bottom, widening into one
broad rounded dark green leaf blade with smooth unbroken edges and a few subtle vein lines,
the leaf blade thick and soft like clay, slightly wilted and gently curved like a cooked
vegetable, lying flat on its back, deep muted green leaf and pale stalk, dull matte surface
without shine, flat stable underside.
The bok choy leaf is the only object in the image, isolated and floating alone on the white
background, centered, fully visible, filling about 75% of the frame, 3/4 top-down view at
30 degrees, on a plain pure white background, soft even studio lighting, shadowless.
```

> 青江菜葉是寬大圓潤、葉緣光滑的湯匙形，和香菜（扇形分叉、波浪葉緣、細葉柄的小葉）明顯不同。葉面寫成「像黏土一樣厚」，避免太薄造成 Tripo 破面。柔軟感由物理材質與 shader 呈現，不靠模型。

**麵條團**（正面圖挑好後，再做多視角）
```text
cute stylized 3D game asset, toy-like, soft clay look, chunky rounded shapes, slightly
exaggerated proportions, simple clean silhouette, hand-painted colors, matte finish.
A single clump of thick wheat noodles (from Taiwanese beef noodle soup): loosely coiled into a
soft oval nest, noodles simplified into a few thick smooth rounded strands that merge together,
slightly uneven soft surface, creamy muted pale yellow with slightly darker strand gaps,
dull matte surface without shine, flat bottom.
The clump of noodles is the only object in the image, isolated and floating alone on the white
background, centered, fully visible, filling about 75% of the frame, 3/4 top-down view at
30 degrees, on a plain pure white background, soft even studio lighting, shadowless.
```

**麵碗**（只用來產生花紋與顏色的參考圖；模型改在 Blender 做，見流程文件 6.1。小湯碗把 `deep ceramic noodle bowl: wide round opening` 改成 `small ceramic soup bowl: small round opening`）
```text
cute stylized 3D game asset, toy-like, soft clay look, chunky rounded shapes, slightly
exaggerated proportions, simple clean silhouette, hand-painted colors, matte finish.
A single empty deep ceramic noodle bowl: wide round opening, gently curved walls, thick rounded
rim, smooth inner surface clearly visible, muted off-white glaze with a simple blue band pattern
near the rim, dull matte surface without shine, flat stable base.
The empty noodle bowl is the only object in the image, clean and completely empty inside,
isolated on the white background, centered, fully visible, filling about 75% of the frame,
3/4 top-down view at 30 degrees, on a plain pure white background, soft even studio lighting,
shadowless.
```

### 5.4 共用容器（Blender，2026-10-23 完成）

所有容器用同一套奶白釉＋藍色回紋，原始檔都在 `art/source/shared/tableware.blend`（做法見流程文件 6.1）。

| 物件 ID | 中文名 | 料理 | 尺寸（cm，直徑×高） | 做法 | 匯出 |
|---|---|---|---|---|---|
| bowl_noodle | 麵碗 | beef_noodle_soup | 18×8 | 旋轉成形；碗緣下藍帶＋回紋 20 組 | `art/models/beef_noodle_soup/bowl_noodle.glb` |
| bowl_soup_small | 小湯碗（1-6） | beef_noodle_soup | 12×6 | 麵碗縮放，共用貼圖 | `art/models/beef_noodle_soup/bowl_soup_small.glb` |
| bowl_rice | 飯碗 | braised_pork_rice | 13×7.5 | 麵碗縮放，共用貼圖 | `art/models/braised_pork_rice/bowl_rice.glb` |
| plate_dumpling | 水餃盤 | dumplings | 24×2.5 | 旋轉成形；盤緣藍線＋回紋 40 組＋內圈細線 | `art/models/dumplings/plate_dumpling.glb` |
| plate_dumpling_small | 水餃小盤（1-6） | dumplings | 16×2 | 水餃盤縮放，共用貼圖 | `art/models/dumplings/plate_dumpling_small.glb` |
| dish_sauce | 沾醬碟 | dumplings | 8×2.5 | 旋轉成形；碟緣藍邊 | `art/models/dumplings/dish_sauce.glb` |

物件 ID 中 `bowl_rice`、`plate_dumpling`、`plate_dumpling_small`、`dish_sauce` 是 3D 美術的提案，待企劃確認。

### 5.3 生成 3D 的設定

共同參數：`texture: true`、`pbr: false`、`texture_quality: "standard"`、`texture_version: "v3.5-20260815"`、`delight: true`；不設定 `export_orientation`。網頁版上對應的選項名稱見流程文件第 12 節。

| 物件 | 方式 | `model` | `face_limit` | 備案 | Convert（`format: "GLTF"`） |
|---|---|---|---|---|---|
| 牛肉塊 | 圖片生 3D | `P1-20260311` | 3000 | `v3.1-20260211` + `smart_low_poly: true` | `texture_size: 512`、`pivot_to_center_bottom: true` |
| 麵條團 | 正面圖 → 圖片轉多視角 → 多視角生 3D | `P1-20260311` | 3000 | 同上 | `texture_size: 512`、`pivot_to_center_bottom: true` |
| 青江菜葉 | 圖片生 3D | `P1-20260311` | 3000 | 同上 | `texture_size: 512`、`pivot_to_center_bottom: true`、`flatten_bottom: true` |

> 單張圖片生成 3D 時，背面的形狀會被推測出來，但貼圖顏色只能靠猜（例如牛肉塊 B 底部有筋的溝、沒有筋的顏色）。底部的小問題可以接受或在 Blender 修；背面是重點的物件改用多視角。

預估點數見流程文件 10.3。

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
- 既有的風格基準圖：{有／沒有。有的話寫出是哪一道料理的哪個物件，並描述它的表面質感與顏色}

請依照以下規則：
1. 把料理拆成「可以各自拿起的物件」。每個物件一次生成、一個 .glb。容器是空的、固定不動。
   液體（湯、醬汁）不建模，寫成 shader 需求。
2. 又薄又小的葉片（香菜、蔥花、碎葉、海苔）標為「Blender 手工」，不用 Tripo。
3. 每個物件寫出真實尺寸（cm）、密度（g/cm³，水 = 1.0）、是否平底、碰撞形狀（凸包數量，或容器用凹面）、
   香菜可以附著的面（Top／Side／Back／Bottom）。
4. 列出可以重用的既有資產：麵碗、湯碗、盤子、醬碟、青菜、共用香菜。
5. 所有物件都走「先產生參考圖，再用圖片生成 3D」。不要提供文字直接生 3D 的 prompt。
6. 指定一個「風格基準物件」：沒有既有基準圖時，選造型最單純的物件；有的話沿用既有基準圖。
   Tripo 網頁版不能上傳參考圖，所以每個物件的 prompt 都要用文字寫出和基準圖同等級的表面質感
   （微微不平、少量柔和細節；不要用 lumpy、knobbly、many bumps），顏色偏深偏沉（deep, muted）。
7. 每個 Tripo 物件寫出完整的英文參考圖 prompt，格式為：STYLE. 物件描述. ISOLATE, SHOT.
   物件描述包含物件名、造型重點 2–3 個、表面質感、顏色與明度、"dull matte surface without shine"、底部形狀。
   STYLE、SHOT 一字不改地使用以下內容：
   STYLE = "cute stylized 3D game asset, toy-like, soft clay look, chunky rounded shapes, slightly
   exaggerated proportions, simple clean silhouette, hand-painted colors, matte finish"
   SHOT = "centered, fully visible, filling about 75% of the frame, 3/4 top-down view at 30 degrees,
   on a plain pure white background, soft even studio lighting, shadowless"
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
| 太寫實、太油亮 | 加重 `matte, clay, toy` 的描述；加 `dull matte surface without shine` |
| 細節糊成一團（例如麵條） | 在描述中**主動簡化**：`simplified into a few thick strands`，不要要求細節 |
| 底部不平、放不穩 | 描述加 `flat stable bottom`；轉檔時開 `flatten_bottom` |
| 同一道料理風格不一致 | 照 2.3 用文字補上表面質感、深色、霧面；所有物件用同一個圖像模型（GPT Image 2）；3 批還不行就改用能上傳參考圖的工具 |
| 綠色食材和香菜太像 | 改輪廓（寬葉、圓葉、管狀），並拉開明度差；不要只改顏色 |
| 參考圖好看，但 3D 結果差 | 參考圖的視角改成更正面、物件更完整；背面複雜就改用多視角 |
| H3.1 的 smart_low_poly 失敗 | 失敗不扣點；改用 P1，或關掉 smart_low_poly 生成後用 Retopology 減面 |
| 貼圖有烘進去的陰影 | 參考圖改成 `shadowless`；`texture_version: "v3.5-20260815"` 加 `delight: true`；還是不行再用第 3 節重新上貼圖 |
