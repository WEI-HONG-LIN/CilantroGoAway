# Tripo3D Prompt 範本

**配套流程：** [`tripo3d_料理建模流程.md`](tripo3d_料理建模流程.md)

圖像生成工具與 Tripo 對英文 prompt 的理解通常比較好，所以 prompt 本體用英文，說明用中文。`{大括號}` 是要替換的欄位。

---

## 1. 共用區塊（每個 prompt 都要用，不要改）

### 1.1 風格描述 `STYLE`

```text
cute stylized 3D game asset, toy-like, soft clay and matte vinyl look, chunky rounded shapes,
softened edges, slightly exaggerated proportions, simple clean silhouette, hand-painted soft
colors, gentle color gradients, minimal surface detail, no realistic pores or noise, matte finish
with soft subtle highlight
```

> 意思：可愛 Q 版、玩具感、黏土或霧面軟膠質感、圓潤厚實、邊角柔和、比例略誇張、輪廓簡潔、手繪柔和配色、少量細節、霧面。對應企劃書 4.1。

### 1.2 構圖與光線 `SHOT`（只用在參考圖）

```text
single object only, centered, full object visible, occupies 75% of the frame,
3/4 top-down view at 30 degrees, plain pure white background, soft even studio lighting,
no cast shadow, no reflections, no props
```

### 1.3 負面描述 `NEGATIVE`

```text
photorealistic, photo scan, realistic texture, greasy, glossy oil, wet shine, noisy texture,
dirt, burnt, multiple objects, plate, bowl, table, chopsticks, hands, background scene,
steam, smoke, text, logo, watermark, cut off, cropped, blurry, low quality
```

> 生成**容器**時，要從 `NEGATIVE` 拿掉 `plate, bowl`；生成**食物**時保留，避免連盤子一起生成。

---

## 2. 參考圖 prompt（步驟 ②，貼到圖像生成工具）

### 2.1 食物範本

```text
{STYLE}, a single {物件英文名} ({物件說明}), {造型重點}, {顏色重點},
{底部描述}, {SHOT}
Negative: {NEGATIVE}
```

| 欄位 | 寫法 | 例子 |
|---|---|---|
| 物件英文名 | 具體的名詞 | `braised beef chunk` |
| 物件說明 | 一句話描述它在料理中的樣子 | `from Taiwanese beef noodle soup` |
| 造型重點 | 2–3 個能被認出來的特徵 | `irregular cube shape, visible soft tendon layer, slightly fibrous edges` |
| 顏色重點 | 主色 + 輔色，寫出明度 | `warm reddish brown with lighter tendon stripes` |
| 底部描述 | 平底或圓底（影響物理） | `flat stable bottom` 或 `rounded bottom` |

### 2.2 容器範本

```text
{STYLE}, a single empty {容器英文名}, {造型重點}, thick rounded rim, smooth inner surface clearly
visible, {顏色與花紋}, flat stable base, nothing inside, {SHOT}
Negative: {NEGATIVE 拿掉 plate, bowl}, food, soup, liquid, noodles
```

### 2.3 多視角（步驟 ② 的 3.3，背面複雜時）

先用 2.1 做出正面圖，再用同一個工具「以這張圖為參考」生成其他視角：

```text
same object as the reference image, identical style, size, colors and lighting,
{view} view, orthographic camera, plain pure white background, no shadow
```

`{view}` 依序填 `left side`、`back`、`right side`。四張圖的物件大小要一致；不一致就重新生成，不要硬塞給 Tripo。

---

## 3. Tripo 文生 3D prompt（步驟 ③，只用來快速試造型）

```text
{STYLE}, a single {物件英文名}, {造型重點}, {顏色重點}, {底部描述},
game-ready low poly prop, closed watertight mesh, solid object
```

`negative_prompt` 欄位填 `NEGATIVE`。

## 4. Tripo 重新上貼圖 prompt（`texture_model` 的 `text_prompt`）

```text
{STYLE}, {物件英文名}, {顏色重點}, flat hand-painted albedo colors, no baked shadows,
no baked highlights, no ambient occlusion darkening, even lighting
```

> 用途：模型造型滿意但貼圖有烘進去的陰影、太寫實或太油時使用。

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

### 5.2 參考圖 prompt

**牛肉塊 A**
```text
cute stylized 3D game asset, toy-like, soft clay and matte vinyl look, chunky rounded shapes,
softened edges, slightly exaggerated proportions, simple clean silhouette, hand-painted soft
colors, gentle color gradients, minimal surface detail, no realistic pores or noise, matte finish
with soft subtle highlight, a single braised beef chunk (from Taiwanese beef noodle soup),
irregular rounded cube shape, a soft translucent tendon layer on one side, slightly fibrous edges,
warm reddish brown with lighter beige tendon stripe, flat stable bottom, single object only,
centered, full object visible, occupies 75% of the frame, 3/4 top-down view at 30 degrees,
plain pure white background, soft even studio lighting, no cast shadow, no reflections, no props
Negative: photorealistic, photo scan, realistic texture, greasy, glossy oil, wet shine, noisy
texture, dirt, burnt, multiple objects, plate, bowl, table, chopsticks, hands, background scene,
steam, smoke, text, logo, watermark, cut off, cropped, blurry, low quality
```

**麵條團**（先做正面，再用 2.3 做其他三個視角）
```text
{STYLE}, a single clump of thick wheat noodles (from Taiwanese beef noodle soup), loosely
coiled into a soft oval nest, noodles simplified into a few thick smooth rounded strands
that merge together, creamy pale yellow with slightly darker strand gaps, flat bottom,
{SHOT}
Negative: {NEGATIVE}
```

**青江菜**
```text
{STYLE}, a single baby bok choy cut in half lengthwise, thick pale green-white stem at the
bottom fanning into a few broad rounded dark green leaves at the top, clear stem and leaf
separation, flat cut side facing down, {SHOT}
Negative: {NEGATIVE}
```

> 青江菜的葉子是寬大圓潤的形狀，和香菜（扇形分叉、波浪邊緣的小葉）明顯不同，符合企劃書的辨識度要求。

**麵碗**
```text
{STYLE}, a single empty deep ceramic noodle bowl, wide round opening, gently curved walls,
thick rounded rim, smooth inner surface clearly visible, off-white glaze with a simple
blue band pattern near the rim, flat stable base, nothing inside, {SHOT}
Negative: photorealistic, photo scan, realistic texture, multiple objects, table, chopsticks,
hands, background scene, food, soup, liquid, noodles, text, logo, watermark, cropped, blurry
```

### 5.3 Tripo 設定

| 物件 | 方式 | model_version | face_limit | smart_low_poly | convert_model |
|---|---|---|---|---|---|
| 牛肉塊 | image_to_model | P1 試造型 → v3.1 正式版 | 3000 | True | GLTF、512、底部中心原點 |
| 麵條團 | multiview_to_model | v3.1 | 3000 | True（失敗就關掉，改用 smart_lowpoly 後處理） | GLTF、512、底部中心原點 |
| 青江菜 | image_to_model | v3.1 | 3000 | True | GLTF、512、底部中心原點、flatten_bottom |
| 麵碗 | image_to_model | v3.1 | 5000 | True | GLTF、1024、底部中心原點、flatten_bottom |

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

請依照以下規則：
1. 把料理拆成「可以各自拿起的物件」。每個物件一次生成、一個 .glb。容器是空的、固定不動。
   液體（湯、醬汁）不建模，寫成 shader 需求。
2. 又薄又小的葉片（香菜、蔥花、碎葉、海苔）標為「Blender 手工」，不用 Tripo。
3. 每個物件寫出真實尺寸（cm）、密度（g/cm³，水 = 1.0）、是否平底、碰撞形狀（凸包數量，或容器用凹面）、
   香菜可以附著的面（Top／Side／Back／Bottom）。
4. 列出可以重用的既有資產：麵碗、湯碗、盤子、醬碟、青菜、共用香菜。
5. 每個要用 Tripo 的物件，寫出完整的英文參考圖 prompt，格式為：
   STYLE + 物件描述（物件名、造型重點 2–3 個、顏色與明度、底部形狀）+ SHOT，並附上 Negative。
   STYLE、SHOT、NEGATIVE 一字不改地使用以下內容：
   STYLE = "cute stylized 3D game asset, toy-like, soft clay and matte vinyl look, chunky rounded
   shapes, softened edges, slightly exaggerated proportions, simple clean silhouette,
   hand-painted soft colors, gentle color gradients, minimal surface detail, no realistic pores
   or noise, matte finish with soft subtle highlight"
   SHOT = "single object only, centered, full object visible, occupies 75% of the frame,
   3/4 top-down view at 30 degrees, plain pure white background, soft even studio lighting,
   no cast shadow, no reflections, no props"
   NEGATIVE = "photorealistic, photo scan, realistic texture, greasy, glossy oil, wet shine,
   noisy texture, dirt, burnt, multiple objects, plate, bowl, table, chopsticks, hands,
   background scene, steam, smoke, text, logo, watermark, cut off, cropped, blurry, low quality"
   （容器的 NEGATIVE 拿掉 plate, bowl，加上 food, soup, liquid。）
6. 檢查辨識度：任何綠色的物件都要說明它和香菜（扇形分叉、波浪葉緣、細葉柄的小葉）在輪廓上有什麼不同。
7. 背面形狀複雜的物件標註「需要多視角」，並附上 left／back／right 視角的 prompt。
8. 每個 Tripo 物件列出建議設定：生成方式、model_version（試造型 P1 → 正式版 v3.1）、
   face_limit（食物 3000、容器 5000）、smart_low_poly、convert_model 參數
   （GLTF、貼圖尺寸、pivot_to_center_bottom、flatten_bottom 是否開啟）。

輸出格式：
## 料理拆件表：{料理名稱}
（表格，欄位：# / 物件 ID / 中文名 / 類型 / 數量 / 尺寸 cm / 生成方式 / 碰撞 / 密度 / 進湯 / 掛點面）
## 液體與 shader 需求
## 重用資產
## 辨識度檢查
## 參考圖 prompt（每個物件一段）
## Tripo 設定表
## 風險與注意事項（例如可能生成失敗的造型、需要手工修正的地方）

物件 ID 用 snake_case：容器 bowl_／plate_／dish_ 開頭，食物 food_，誘餌 decoy_；
同一種食材的不同造型加 _a、_b。
````

---

## 7. 常見問題與調整方式

| 問題 | 調整 prompt 的方式 |
|---|---|
| 生成出連盤子、連桌子 | 在物件描述加 `isolated, floating object, no container`；確認參考圖背景是純白 |
| 太寫實、太油亮 | 加重 `matte, clay, toy` 的描述；貼圖用第 4 節重新上 |
| 細節糊成一團（例如麵條） | 在描述中**主動簡化**：`simplified into a few thick strands`，不要要求細節 |
| 底部不平、放不穩 | 描述加 `flat stable bottom`；`convert_model` 開 `flatten_bottom` |
| 同一道料理風格不一致 | 所有物件用同一個圖像工具、同一組 STYLE；先做一件「風格基準物件」，其他物件用它當風格參考 |
| 綠色食材和香菜太像 | 改輪廓（寬葉、圓葉、管狀），並拉開明度差；不要只改顏色 |
| smart_low_poly 失敗 | 關掉它重新生成，再用 `smart_lowpoly` 後處理；或在 Blender 減面 |
