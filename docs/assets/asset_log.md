# 資產紀錄

美術檔案只留在本機，這份紀錄會上傳 GitHub。每個資產一筆，格式見 `docs/pipeline/tripo3d_料理建模流程.md` 第 9 節。

### food_beef_chunk_a
- 料理：beef_noodle_soup
- 管道：Tripo 網頁版
- 參考圖：art/source/beef_noodle_soup/ref_beef_chunk_a.png
- 參考圖的圖像模型與 prompt：GPT Image 2；舊版 `STYLE`（prompt 範本 1.1 修改前）＋ 牛肉塊 A 的描述
- 風格基準圖：本物件就是基準（art/source/style_anchor/beef_noodle_soup_beef_chunk_a.png）
- 生成方式：圖片生 3D
- Tripo 原始模型：art/source/beef_noodle_soup/tripo_beef_chunk_a.glb
- 3D 模型版本：<待補>
- Task ID：Tripo 網頁版不顯示，以 Model Info 截圖（生成時間、Privacy 會員設定）為準，存 `art/source/licenses/tripo/`
- Seeds：<待補>
- 後處理：轉檔 GLB
- Blender 修改（2026-10-23）：合併重複頂點、縮放到長 4 cm、壓平最底 4% 當平穩底面、原點在底部中心；原始檔 art/source/beef_noodle_soup/beef_noodle_soup.blend（`food` 集合；Tripo 原始在 `raw` 集合）
- 尺寸：4.0×3.1×2.9 cm
- 最終三角面數／貼圖：2,980／512²（Tripo 原貼圖）
- 碰撞：`-convcolonly` 凸包 ×1（230 面）；掛點 `Anchor_BeefChunk_Top_01`、`_Side_01`（-Y 的切面）、`_Bottom_01`；浮力點 `Buoyancy_01`–`_04`
- 匯出：art/models/beef_noodle_soup/food_beef_chunk_a.glb
- 使用點數：<待補>
- 授權：Tripo Pro（可商用；使用者確認 2026-10-23）。證明：訂閱收據＋生成紀錄截圖，存本機 `art/source/licenses/tripo/`

### food_beef_chunk_b
- 料理：beef_noodle_soup
- 管道：Tripo 網頁版
- 參考圖：art/source/beef_noodle_soup/ref_beef_chunk_b.png
- 參考圖的圖像模型與 prompt：GPT Image 2；prompt 範本 5.2「牛肉塊 B」（第 4 版，2026-10-23）
- 風格基準圖：art/source/style_anchor/beef_noodle_soup_beef_chunk_a.png（文字對齊，未上傳）
- 生成方式：圖片生 3D
- Tripo 原始模型：art/source/beef_noodle_soup/tripo_beef_chunk_b.glb（3,012 三角面、貼圖 512²、1 材質、原點在底部中心、長 1.0 單位）
- 3D 模型版本：<待補>
- Task ID：Tripo 網頁版不顯示，以 Model Info 截圖（生成時間、Privacy 會員設定）為準，存 `art/source/licenses/tripo/`
- Seeds：<待補>
- 後處理：轉檔 GLB
- Blender 修改（2026-10-23）：同牛肉塊 A（縮放到長 4 cm、壓平底部）；底部筋的溝保留；原始檔 art/source/beef_noodle_soup/beef_noodle_soup.blend（`food` 集合；Tripo 原始在 `raw` 集合）
- 尺寸：4.0×3.1×1.3 cm
- 最終三角面數／貼圖：3,012／512²
- 碰撞：凸包 ×1（228 面）；掛點 `Anchor_BeefChunk_Top_01`、`_Side_01`、`_Bottom_01`；浮力點 ×4
- 匯出：art/models/beef_noodle_soup/food_beef_chunk_b.glb
- 使用點數：<待補>
- 授權：Tripo Pro（可商用；使用者確認 2026-10-23）。證明：訂閱收據＋生成紀錄截圖，存本機 `art/source/licenses/tripo/`


### food_noodle_clump_a／_b
- 料理：beef_noodle_soup
- 管道：Tripo 網頁版（參考圖 GPT Image 2，prompt 範本 5.2「麵條團」；單張圖生 3D，多視角的側視角高度不對而放棄）
- 參考圖／原始：art/source/beef_noodle_soup/ref_noodle_clump_a/_b.png、tripo_noodle_clump_a/_b.glb
- Blender 修改（2026-10-23）：縮放到 6 cm、壓平底部；A 的幾段麵條是分開的網格，都保留（一起當一個剛體）；B 原本太扁，加上中間隆起、每條麵條隨機抬高與波浪起伏；原始檔 art/source/beef_noodle_soup/beef_noodle_soup.blend（`food` 集合；Tripo 原始在 `raw` 集合）
- 尺寸：A 6.0×5.8×1.7 cm；B 6.0×6.0×1.5 cm
- 三角面數／貼圖：A 3,011、B 2,888／512²
- 碰撞：沿長邊切兩半各一個凸包 `_a-convcolonly`、`_b-convcolonly`（約 225 面）；掛點 `Anchor_NoodleClump_Top_01`、`_Bottom_01`；浮力點 ×4
- 匯出：art/models/beef_noodle_soup/food_noodle_clump_a.glb、_b.glb
- 備註：香菜藏在麵條縫隙時，凸包會蓋住縫隙，程式要讓香菜的點選優先於食物碰撞
- 授權：Tripo Pro（可商用；使用者確認 2026-10-23）。證明：訂閱收據＋Model Info 截圖，存本機 `art/source/licenses/tripo/`

### food_bok_choy_leaf_a／_b
- 料理：beef_noodle_soup
- 管道：Tripo 網頁版（prompt 範本 5.2「青江菜葉」B 版；A 用同一份 prompt 改成大外葉重新生成）
- 參考圖／原始：art/source/beef_noodle_soup/ref_bok_choy_leaf_a/_b.png、tripo_bok_choy_leaf_a/_b.glb
- Blender 修改（2026-10-23）：Tripo 照參考圖的俯視角把葉子做成斜的（A 約 45°），用主成分把葉面轉平，葉尖跟著壓低；縮放（A 長 8 cm、B 長 6 cm）；原點在底部中心；不壓平底部（保留梗的 U 形）；原始檔 art/source/beef_noodle_soup/beef_noodle_soup.blend（`food` 集合；Tripo 原始在 `raw` 集合）
- 尺寸：A 8.0×5.5×1.5 cm；B 4.4×6.0×1.4 cm
- 三角面數／貼圖：A 2,888、B 2,924／512²
- 碰撞：沿長邊切兩半各一個凸包；掛點 `Anchor_BokChoyLeaf_Top_01`、`_Bottom_01`；浮力點 ×4
- 匯出：art/models/beef_noodle_soup/food_bok_choy_leaf_a.glb、_b.glb
- 備註：柔軟感建議用頂點晃動 shader，不用軟體物理
- 授權：Tripo Pro（可商用；使用者確認 2026-10-23）。證明：訂閱收據＋Model Info 截圖，存本機 `art/source/licenses/tripo/`

### deco_noodle_strands_a／_b／_c／_d
- 料理：beef_noodle_soup（裝飾散麵，固定、不能互動，掛在麵條團與碗緣）
- 管道：Blender 手工（Bezier 曲線＋bevel，轉成網格；Claude 透過 Blender MCP，2026-10-23）
- 原始檔：art/source/beef_noodle_soup/beef_noodle_soup.blend（`deco` 集合）
- 尺寸：長 8.7／9.7／10.6／8.3 cm，粗 0.5 cm；一端微微下垂，可以掛在碗緣
- 三角面數：248–308；材質 1 個（麵條暖黃 sRGB 0.886,0.667,0.302，取自麵條團 A 貼圖中位數）；無碰撞
- 匯出：art/models/beef_noodle_soup/deco_noodle_strands_a.glb … _d.glb
- 授權：自製，無第三方授權問題

### bowl_noodle
- 料理：beef_noodle_soup（麵碗）
- 管道：Blender 手工（Claude 透過 Blender MCP 以 Python 建立，2026-10-23）
- 原始檔：art/source/shared/tableware.blend
- 生成方式：旋轉成形＋程式繪製的回紋貼圖（流程文件 6.1；D-20261023-06）
- 尺寸：18×8 cm（直徑×高）
- 三角面數／貼圖：3,072／2048×512；碰撞 `bowl_noodle-colonly`（本體減面 50%）
- 匯出：art/models/beef_noodle_soup/bowl_noodle.glb
- 授權：自製，無第三方授權問題

### bowl_soup_small
- 料理：beef_noodle_soup（小湯碗）
- 管道：Blender 手工（Claude 透過 Blender MCP 以 Python 建立，2026-10-23）
- 原始檔：art/source/shared/tableware.blend
- 生成方式：旋轉成形＋程式繪製的回紋貼圖（流程文件 6.1；D-20261023-06）
- 尺寸：12×6 cm（直徑×高）
- 三角面數／貼圖：3,072／共用 bowl_noodle 貼圖；碰撞 `bowl_soup_small-colonly`（本體減面 50%）
- 匯出：art/models/beef_noodle_soup/bowl_soup_small.glb
- 授權：自製，無第三方授權問題

### bowl_rice
- 料理：braised_pork_rice（飯碗）
- 管道：Blender 手工（Claude 透過 Blender MCP 以 Python 建立，2026-10-23）
- 原始檔：art/source/shared/tableware.blend
- 生成方式：旋轉成形＋程式繪製的回紋貼圖（流程文件 6.1；D-20261023-06）
- 尺寸：13×7.5 cm（直徑×高）
- 三角面數／貼圖：3,072／共用 bowl_noodle 貼圖；碰撞 `bowl_rice-colonly`（本體減面 50%）
- 匯出：art/models/braised_pork_rice/bowl_rice.glb
- 授權：自製，無第三方授權問題

### plate_dumpling
- 料理：dumplings（水餃盤）
- 管道：Blender 手工（Claude 透過 Blender MCP 以 Python 建立，2026-10-23）
- 原始檔：art/source/shared/tableware.blend
- 生成方式：旋轉成形＋程式繪製的回紋貼圖（流程文件 6.1；D-20261023-06）
- 尺寸：24×2.5 cm（直徑×高）
- 三角面數／貼圖：2,688／2048×512；碰撞 `plate_dumpling-colonly`（本體減面 50%）
- 匯出：art/models/dumplings/plate_dumpling.glb
- 授權：自製，無第三方授權問題

### plate_dumpling_small
- 料理：dumplings（水餃小盤）
- 管道：Blender 手工（Claude 透過 Blender MCP 以 Python 建立，2026-10-23）
- 原始檔：art/source/shared/tableware.blend
- 生成方式：旋轉成形＋程式繪製的回紋貼圖（流程文件 6.1；D-20261023-06）
- 尺寸：16×2 cm（直徑×高）
- 三角面數／貼圖：2,688／共用 plate_dumpling 貼圖；碰撞 `plate_dumpling_small-colonly`（本體減面 50%）
- 匯出：art/models/dumplings/plate_dumpling_small.glb
- 授權：自製，無第三方授權問題

### dish_sauce
- 料理：dumplings（沾醬碟）
- 管道：Blender 手工（Claude 透過 Blender MCP 以 Python 建立，2026-10-23）
- 原始檔：art/source/shared/tableware.blend
- 生成方式：旋轉成形＋程式繪製的回紋貼圖（流程文件 6.1；D-20261023-06）
- 尺寸：8×2.5 cm（直徑×高）
- 三角面數／貼圖：2,048／2048×512；碰撞 `dish_sauce-colonly`（本體減面 50%）
- 匯出：art/models/dumplings/dish_sauce.glb
- 授權：自製，無第三方授權問題

### tool_chopsticks／tool_tweezers／tool_spoon
- 用途：餐具（企劃書 4.2、7.4）
- 管道：Blender 手工（Claude 透過 Blender MCP 以 Python 建立，2026-10-23）
- 原始檔：art/source/shared/tableware.blend
- 匯出：art/models/tools/tool_chopsticks.glb、tool_tweezers.glb、tool_spoon.glb
- 三角面數：712／372／1,496；材質各 2 個（主色＋藍色）
- 動畫：筷子、鑷子各有 `grip`（12 格）
- 2026-10-25 改版（使用者回饋）：
  - 筷子改成兩根獨立的直筷，尾端不相連。支點在離筷尖 1.5 單位（手握處），根節點原點在筷尖。`grip` 只動 `chopstick_R`（上筷，第 1 格張開、第 6 格夾合、第 12 格張開），`chopstick_L`（下筷）固定。
  - 湯匙改成一體成形的中式湯匙：橢圓匙面平順收窄成匙柄，匙柄末端上翹，厚度 0.3 cm。原點在匙面中心。
- 授權：自製，無第三方授權問題

### decoy_scallion_a／_b／_c
- 用途：誘餌（蔥花），牛肉麵與水餃共用（企劃書 3.3、4.2）
- 管道：Blender 手工（Claude 透過 Blender MCP 以 Python 建立，2026-10-23）
- 原始檔：art/source/shared/tableware.blend（`decoys` 集合）
- 造型：A 圓圈 6×6×2.2 mm；B 斜切橢圓 8×6 mm；C 薄片 5.9×5.4×1.6 mm。壁厚、邊緣倒圓角（2026-10-23 v2，參考 Tripo 試作版的玩具感調整）
- 顏色：外皮與內壁綠 sRGB (118,182,42)、切面淡黃綠 (222,238,150)，粗糙度 0.85；比香菜亮，靠「中空圓圈」的輪廓和香菜區分
- 與 Tripo 試作比較（2026-10-23）：Tripo 版（art/source/beef_noodle_soup/tripo_scallion.glb，988 面）洞太小、縮到 6 mm 看起來像綠色圓珠，且只有一種形狀，因此採用 Blender 版；Tripo 版留作參考
- 三角面數：各 384；材質 2 個；碰撞 `-convcolonly` 凸包 ×1；浮力取樣點 `Buoyancy_01`–`_04`
- 匯出：art/models/shared/decoy_scallion_a.glb、_b.glb、_c.glb
- 授權：自製，無第三方授權問題

### cilantro_full／_small／_fragment（香菜，全遊戲共用）
- 用途：目標物（企劃書 3.2、4.2：完整葉、小葉、碎葉 × 2 色＋浸濕變體）
- 管道：Tripo 生成 → Blender 清理（D-20261023-07）。參考圖用 GPT Image 2，3D 用 P1、face_limit 500 生成（實際約 3,000 面）
- 參考圖與原始檔：art/source/beef_noodle_soup/ref_cilantro_<full|small|fragment>_tripo.png、tripo_cilantro_<full|small|fragment>.glb（共用資產，之後可移到 shared/）
- prompt：建模計畫文件「香菜（Tripo 版）」段落；小葉用第 2 版（圓扇形嫩葉，第 1 版畫成和完整葉一樣的三裂葉）
- Tripo task ID／seed：網頁版不顯示，以 Model Info 截圖為準（小葉生成時間 2026-10-23 22:20:33）；方案：Pro
- Blender 清理：減面到 600 三角面；補 Tripo 原始的小破洞（小葉 6 邊、碎葉 3 邊）；用主成分把葉面轉平（Tripo 照參考圖的 60° 視角把葉子做成傾斜）；原點在葉柄根部，碎葉在撕口中央
- 尺寸：full 2.1×2.9 cm、small 1.5×1.4 cm、fragment 0.7×0.8 cm；厚度約 0.7–2.5 mm（含葉面彎曲）
- 顏色：貼圖 512²。亮綠＝原貼圖 ×0.85；深綠 ×(0.62,0.70,0.62)；浸濕 ×(0.38,0.46,0.40)、粗糙度 0.35。貼圖存在 art/source/shared/cilantro_tex/
- 明度（貼圖中位數 CIE L*）：亮綠約 50、深綠約 41、浸濕約 27；蔥花外皮 67.6、切面 91.2。灰階對照圖已確認可分辨；青江菜靠寬大湯匙形葉和淡色粗梗區分
- 碰撞 `-convcolonly` 凸包 ×1；浮力取樣點 `Buoyancy_01`–`_04`（碎葉 3 個）
- 匯出：art/models/shared/cilantro/cilantro_<full|small|fragment>_<light|dark|soaked>.glb（3 造型 × 3 材質 = 9 個，每個 360–510 KB）
- 原始檔：art/source/shared/tableware.blend（`cilantro` 集合；Blender 手工 v1 在 `cilantro_blender_v1` 集合，已排除不匯出）
- 授權：Tripo Pro（可商用；使用者確認 2026-10-23）。證明：訂閱收據＋生成紀錄截圖，存本機 `art/source/licenses/tripo/`

### scene_table／scene_backdrop／scene_discard_dish／scene_temp_plate（場景，M5）
- 用途：企劃書 4.2「場景」：桌面、背景、棄置碟、暫放盤。取代 `game.tscn` 的灰盒
- 管道：Blender 手工（Claude 透過 Blender MCP 以 Python 建立，2026-10-28）；貼圖用程式產生（木紋、磁磚、地磚、紅木牌），存 art/source/scene/tex/
- 原始檔：art/source/scene/scene.blend（`scene` 集合）
- 尺寸與原點（1 單位 = 10 cm，對齊目前灰盒，換模型不用改位置）：
  - `scene_table`：桌面 9×6、厚 0.4，含桌框與四支桌腳（落地在 y = -7.5）。原點在桌面中心、y = 0 就是桌面。1,052 三角面，木紋貼圖 2048×1366
  - `scene_backdrop`：小吃店角落。白磁磚牆裙、米色牆、深色木飾條、8 塊沒有文字的紅木牌、紅磚色地磚，加 2 張紅色塑膠椅（`scene_stool_a`／`_b`）。地板 y = -7.5，後牆在桌子後方 11 單位，左右牆在 x = ±15。牆 158 三角面、椅子各 732
  - `scene_discard_dish`：白瓷小碟、藍邊，碟心畫紅色禁止符號。半徑 0.4、高 0.1，原點在中心（底部 y = -0.05），和灰盒圓柱一樣
  - `scene_temp_plate`：白琺瑯托盤、藍邊。2×1.4、高 0.1，原點在中心，盤面在 y = +0.05（`temp_plate.gd` 的 `surface_height`）
- 碰撞：都只有外觀，沿用 `game.tscn` 現有的碰撞形狀（大小相同）
- 鍵光從左前上方打（見下方燈光），左右牆的影子不會落到桌上
- 匯出：art/models/scene/scene_table.glb、scene_backdrop.glb、scene_discard_dish.glb、scene_temp_plate.glb
- 授權：自製，無第三方授權問題

### decoy_greens_a／_b（青菜碎葉誘餌，M5）
- 用途：誘餌（企劃書 4.2「蔥花、青菜碎葉」），全遊戲共用
- 管道：Blender 手工（2026-10-28），原始檔 art/source/scene/scene.blend（`decoys` 集合）
- 造型：撕下來的青菜葉片，圓滑葉緣、一邊是撕口，有淡色主脈和側脈，沒有分叉。A 1.2×1.6 cm、B 0.8×1.0 cm，厚 0.6 mm，葉面微彎
- 顏色：黃綠 sRGB (112,163,51)、葉脈淡綠，貼圖 256²（art/source/scene/tex/decoy_greens.png）。比香菜淺、偏黃；和香菜的彩色／灰階對照圖已確認可分辨（靠圓滑葉緣與葉脈）
- 三角面數：各 896；碰撞 `-convcolonly` 凸包 ×1；浮力取樣點 `Buoyancy_01`–`_04`
- 匯出：art/models/shared/decoy_greens_a.glb、_b.glb
- 授權：自製，無第三方授權問題

### table_lighting（燈光預設，M5）
- 用途：企劃書 4.1「柔和主光、環境補光、接觸陰影」
- 檔案：art/lighting/table_lighting.tscn（取代 `game.tscn` 的 WorldEnvironment 與 DirectionalLight3D，一個場景只能有一個 WorldEnvironment）
- 內容：
  - KeyLight：暖白方向光，從左前上方 50° 打下，柔邊陰影（angular distance 1.5°），陰影偏移已依 10 cm 單位調小
  - FillLight：冷色補光，從右前方低角度，不投影
  - LampLight：桌子正上方的暖色點光，像小吃店吊燈
  - Environment：環境光、SSAO（接觸陰影，半徑 0.6）、輕微光暈、飽和度 1.05
  - CameraAttributesPractical：遠景景深，後面的牆和椅子微糊，讓視線集中在料理
- 授權：自製

### 臭味煙霧特效（hint_smoke，M5）
- 用途：企劃書 8.1「提示：臭味煙霧」的外觀。煙霧粒子與 shader 由 3D 美術製作，選香菜與定位由程式負責
- 檔案（3 種藏法各一個）：
  - art/vfx/hint_smoke.tscn：黏在食物上，從香菜附近往上冒
  - art/vfx/hint_smoke_seep.tscn：藏在背面，從食物底下往四周滲出再往上飄。環形發射半徑 0.2–0.3，請依食物半徑縮放節點
  - art/vfx/hint_smoke_bubbles.tscn：沉在湯底，放在湯面高度，湯面冒臭泡泡，泡泡破掉時冒小口煙
- 結構：根節點 Node3D，底下是 `Puffs`（卡通雲朵煙團）、`Wisps`（漫畫式彎曲臭味線），湯底版多一個 `Bubbles`。都是 GPUParticles3D，`local_coords` 開著，所以把節點掛在食物底下，煙就會跟著食物走
- 開始：加進場景樹就開始冒。結束（6 秒到了或香菜被挑掉）：把所有 GPUParticles3D 的 `emitting` 設成 false，等 2.5 秒讓粒子淡完再刪節點
- 外觀：淡紫灰 sRGB (184,163,204)，描邊深紫，半透明（煙團 0.55、線 0.75），不寫深度、不投影，不會擋住香菜。不用綠色
- Shader：shaders/vfx_hint_smoke_puff.gdshader、vfx_hint_smoke_wisp.gdshader、vfx_hint_bubble.gdshader（形狀都用數學畫，不用貼圖）
- 授權：自製

### 通關慶祝（clear_celebration，M5）
- 用途：企劃書 4.3「通關時：星星、粒子與短暫的料理完成動畫」
- 檔案：art/vfx/clear_celebration.tscn，放在料理中心、桌面高度
- 播放：`$AnimationPlayer.play("play")`，長 1.8 秒。內容：
  - `Ring`：從料理底下擴散的一圈金光（0.8 秒，半徑 0.2 → 1.8）
  - `Stars`：18 顆金色圓角星星往上噴，轉著落下（one shot）
  - `Sparkles`：24 個四芒小閃光在料理周圍閃（one shot）
- 沒有做料理本體的彈跳：碗和食物是物理物件，縮放會讓碰撞和外觀對不上，所以料理完成感改用光圈加閃光表現
- Shader：shaders/vfx_clear_star.gdshader、vfx_clear_ring.gdshader
- 授權：自製
