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

### 滷肉飯食物（braised_pork_rice，2026-11-09）
- 管道：Tripo 網頁版，Claude 透過 Claude in Chrome 操作（2026-11-09）。參考圖 GPT Image 2，在 Image 分頁**上傳風格基準圖**（art/source/style_anchor/beef_noodle_soup_beef_chunk_a.png）＋文字描述；3D 用 Smart Mesh「P1.0 - Fast」（35 點）＋ Texture（20 點）；Privacy：Private
- Task ID：網頁版不顯示，以 Model Info 截圖為準，存 `art/source/licenses/tripo/<物件 ID>_info.jpg`
- 原始檔：art/source/braised_pork_rice/ref_<物件>.png、tripo_<物件>.glb；Blender 檔 art/source/braised_pork_rice/braised_pork_rice.blend（`food` 集合；Tripo 原始在 `raw` 集合）
- 共通的 Blender 修改：合併重複頂點、重算法線、縮放、原點在底部中心、壓平最底 2–4%、凸包碰撞 `-convcolonly`（約 200 面）；掛點 Empty 的 Z 軸朝外（匯出後是 Godot +Y），葉子方向沿 Blender +Y；不加浮力點（滷肉飯不進湯）
- 授權：Tripo Pro（可商用）。證明：Model Info 截圖（Privacy: Private、Tripo P1.0、生成時間），存本機 `art/source/licenses/tripo/`

| 物件 ID | 中文名 | 尺寸（cm） | 三角面／貼圖 | 碰撞 | 掛點 | Model Info 生成時間 |
|---|---|---|---|---|---|---|
| food_rice_mound | 飯面＋肉燥（固定，不能拿起） | 直徑約 8.1、高 5.65 | 4,990／1024² | 凸包 ×1 | `Anchor_Rice_Top_01`–`_06` | 2026-11-09 21:58:28 |
| food_pork_chunk_a | 滷肉塊 A（方塊） | 3.0×2.4×2.0 | 2,984／512² | 凸包 ×1 | `Anchor_PorkChunk_Top_01`、`_Side_01`（-Y 面，Godot +Z）、`_Bottom_01` | 2026-11-09 21:56:19 |
| food_pork_chunk_b | 滷肉塊 B（斜楔形） | 2.9×3.2×2.0 | 2,984／512²（原 4,998，已減面） | 凸包 ×1 | 同上 | 2026-11-09 21:58:39 |
| food_pork_bit_a／_b／_c | 小滷肉塊（3 種造型） | 1.6×1.2×1.4／1.5×1.3×1.2／1.4×1.5×1.2 | 約 1,500／512² | 凸包 ×1 | `Anchor_PorkBit_Top_01`、`_Bottom_01` | 22:30:56／22:30:50／22:30:43 |
| food_egg_half | 對半滷蛋 | 4.0×3.6×2.0 | 2,727／512² | 凸包 ×1 | `Anchor_EggHalf_Top_01`（蛋白圓頂）、`_Side_01`、`_Bottom_01`（切面） | 2026-11-09 21:58:51 |
| food_greens | 青菜（一小把青江菜） | 4.4×3.6×2.4 | 2,984／512² | 沿長邊切兩半，凸包 ×2 | `Anchor_Greens_Top_01`、`_Bottom_01` | 2026-11-09 21:58:09 |
| food_radish_slice | 黃蘿蔔片 | 直徑 3.0、厚 0.5 | 2,896／512² | 凸包 ×1 | `Anchor_Radish_Top_01`、`_Bottom_01` | 2026-11-09 21:57:53 |

- 匯出：art/models/braised_pork_rice/<物件 ID>.glb
- 滷蛋：Tripo 做出來是切面朝上斜放，已轉成**切面朝下**（企劃書與掛點需求表的擺法），Bottom 要翻過來才看得到。
- 飯面：原點在底部中心，放在 `bowl_rice` 裡 y = 0.15（碗內底）時，頂點在 y = 0.715，和程式的暫代飯面同高。下半部依碗內壁收窄（底部半徑 0.27、頂緣約 0.41），不會穿出碗壁。頂面大部分是肉燥，白飯只在外圈。
- 飯面掛點位置沿用程式暫代飯面的 `RICE_ANCHORS`，但 03 和 05 太靠邊打不到飯面，往中心移了 15% 和 5%；以 GLB 裡的位置為準。
- 小滷肉塊是使用者 2026-11-09 要求新增的（「加幾個長相不同的小滷肉塊」），用途和數量由關卡設計決定；掛點名稱 `PorkBit` 是 3D 美術的提案。
- 物件 ID `food_rice_mound`、`food_pork_bit_*`、`food_greens`、`food_radish_slice` 是 3D 美術的提案，待企劃確認。

### 水餃食物（dumplings，2026-11-09）
- 管道：同上面的滷肉飯（Claude in Chrome 操作 Tripo 網頁版；GPT Image 2 上傳風格基準圖；Smart Mesh P1.0 + Texture；Private）
- 原始檔：art/source/dumplings/ref_<物件>.png、tripo_<物件>.glb；Blender 檔 art/source/dumplings/dumplings.blend（`food`／`raw` 集合）
- Blender 修改：同滷肉飯的共通做法。完整水餃**立著放、摺邊朝上**（使用者 2026-11-09 選定；暫代水餃和掛點需求表原本是平躺），長軸沿 Blender Y（Godot Z），兩面肚子朝 ±X；壓平最底 6% 讓它站穩
- 授權：Tripo Pro（可商用）。證明：Model Info 截圖存本機 `art/source/licenses/tripo/`

| 物件 ID | 中文名 | 尺寸（cm） | 三角面／貼圖 | 碰撞 | 掛點 | Model Info 生成時間 |
|---|---|---|---|---|---|---|
| food_dumpling_a | 完整水餃 A（圓胖） | 1.8×4.2×2.6 | 2,990／512² | 凸包 ×1 | `Anchor_Dumpling_Top_01`（+X 側的肚子，半高處，法線朝 +X）、`_Side_01`（-X 側、摺邊正下方，3/4 高處）、`_Bottom_01` | 2026-11-09 22:55:09 |
| food_dumpling_b | 完整水餃 B（摺紋明顯） | 1.9×3.8×2.0 | 2,930／512² | 凸包 ×1 | 同上 | 2026-11-09 22:55:03 |
| food_dumpling_cut | 切開的水餃（看得到餡） | 3.4×2.7×2.2 | 2,930／512² | 凸包 ×1 | `Anchor_DumplingCut_Top_01`、`_Side_01`（剖面的餡上，Godot +Z）、`_Bottom_01` | 2026-11-09 22:55:15 |
| food_dumpling_wrapper | 水餃皮（空的） | 4.5×3.6×1.5 | 2,896／512² | 凸包 ×1（會蓋住皮的凹處） | `Anchor_DumplingWrapper_Top_01`（皮的內底）、`_Bottom_01` | 2026-11-09 22:55:21 |
| food_dumpling_filling | 水餃餡 | 3.0×2.3×1.8 | 2,990／512² | 凸包 ×1 | `Anchor_DumplingFilling_Top_01`、`_Bottom_01` | 2026-11-09 22:55:27 |

- 匯出：art/models/dumplings/<物件 ID>.glb
- 切開的水餃、水餃皮、水餃餡是使用者 2026-11-09 要求新增的，用途由企劃和關卡設計決定；物件 ID 和掛點名稱（`DumplingCut`、`DumplingWrapper`、`DumplingFilling`）是 3D 美術的提案。
- 水餃皮的凸包會填滿凹處：香菜如果要藏在皮裡面，程式要讓香菜的點選優先（同麵條團）。

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

### env_xiaochi_table_a（餐館場景・台式小吃店，桌子）
- 用途：取代 `scene_table`（M5）的外觀；餐館場景建模計畫第 1 階段（`docs/pipeline/餐館場景建模計畫.md`）
- 風格基準：GPT Image 2 概念圖 C（Tripo Pro，2026-11-14，使用者選定）；只取顏色與構圖，造型照 Q 版
- 管道：Blender 手工（2026-11-14），貼圖用程式產生
- 原始檔：art/source/env/xiaochi/xiaochi.blend（`_preview` 集合不匯出）；貼圖 art/source/env/xiaochi/tex/
- 尺寸與原點：和 `scene_table` 完全相同。桌面 9×6、厚 0.4，頂面 y = 0，原點在桌面中心，桌腳到 y = -7.5
- 三角面：1,484（桌面 300、桌框 4×108、桌腳 4×188）；材質 2 個：`mat_env_xiaochi_table_top`、`mat_env_xiaochi_table_frame`。2026-11-14 使用者反映遊戲內桌面太亮面、偏橘，改為 roughness 0.86、specular 0.25（遊戲內由 art/materials/env_xiaochi/env_xiaochi_table_{top,frame}.tres 覆寫；重新匯出 glb 時要沿用這兩個值）
- 貼圖：桌面 2048×1366（平均 #683A1F，灰階約 27%）、桌框 1024²（平均 #57301A）。木紋寬、低對比，最細的深色紋約 2.5 cm
- UV：UVMap＋UV2（lightmap，匯出為 TEXCOORD_1）
- 碰撞：無，沿用 `game.tscn` 的桌面碰撞
- 灰階檢查（Blender 預覽燈光）：桌面 35%；淺色香菜比木頭亮約 0.11；深色香菜碎葉只亮 0.04（看得到但淡），等遊戲內燈光定案後用遊戲截圖複查
- 匯出：art/models/env/xiaochi/env_xiaochi_table_a.glb
- 授權：自製；概念圖由 Tripo Pro 方案產生

### 小吃店場景套組 env_xiaochi（餐館場景第 2、3 階段）
- 用途：取代 `scene_backdrop`；場景套組 `art/env/xiaochi/env_xiaochi.tscn`（介面見 `docs/pipeline/餐館場景建模計畫.md` 4.2）。只有外觀、沒有碰撞，房間尺寸和 `scene_backdrop` 相同
- 管道：Blender 手工（2026-11-14，建模腳本在 xiaochi.blend 的 `env_builders` 文字區塊）＋3 個 Tripo 道具；貼圖用程式產生
- 原始檔：art/source/env/xiaochi/xiaochi.blend、art/source/env/common/env_common.blend；貼圖 art/source/env/xiaochi/tex/（trim 2048、props 1024、Tripo 道具各 512）
- 匯出（art/models/env/xiaochi/，三角面）：wall_tile_a 90、wall_tile_b 264、wall_corner_in 68、menu_board_a–d 各 44（牛肉麵、滷肉飯、水餃、酸辣湯；字型 jf open 粉圓 OFL，烘進貼圖）、stool_a 584（經典鏤空紅凳：4 支外八腳＋腳環）、condiment_set 604、shelf_a 824、counter_a 700（含 `SteamPoint`）、fan_a 876（`FanHead` 擺頭、`FanBlades` 旋轉，動畫 `fan_swing_loop` 8 秒）
- 共用件（art/models/env/common/）：floor_plane 36、light_tube_a 164
- Tripo 道具：env_xiaochi_prop_lucky_cat（1,480，高 15 cm）、env_xiaochi_prop_thermos（1,480，高 30 cm）、env_xiaochi_prop_cash_register（1,378，寬 30 cm，薄荷綠降飽和約 55%）。參考圖 GPT Image 2，Smart Mesh P1.0、1,500 面、Private，貼圖 512；原始檔 art/source/env/xiaochi/tripo_*.glb
- 整套：約 13,100 三角面、10 種材質；每個網格都有 UV2
- 盆栽 `env_xiaochi_plant_a` 取消（綠色會干擾找香菜）
- 灰階（遊戲鏡頭、現行燈光）：桌面 0.42–0.45、地板 0.40、後牆磁磚 0.68–0.70。背景比桌面亮，待燈光以衰減／霧／暗角處理
- 已知限制：遊戲鏡頭最遠時後牆只看到約地板上方 0.95 m，菜牌、電扇、日光燈只在全景看得到；每個 glb 內嵌自己的材質，匯入時應抽成共用材質
- 授權：自製；Tripo 道具用 Pro 方案生成（證明存本機 art/source/licenses/tripo/）

### 新料理共用事項（meatball_soup／century_egg_tofu／gua_bao／oyster_misua／pho，2026-11-22～27）
- dish_id 是暫定名，待遊戲企劃確認。物件 ID、掛點名稱也是 3D 美術的提案。總清單與接手事項見 `docs/assets/new_dishes_summary.md`。
- Tripo 管道：同滷肉飯（Claude 透過 Claude in Chrome 操作 Tripo 網頁版；Image 分頁 GPT Image 2、上傳風格基準圖 `art/source/style_anchor/beef_noodle_soup_beef_chunk_a.png`；Smart Mesh「P1.0 - Fast」三角面 3000＋ Texture；Privacy：Private；Export GLB 512）。
- 2026-11-22 實際價格：GPT Image 2 一批 2 張 40 點、P1.0 35 點、Texture 20 點，每個 Tripo 物件約 55 點＋參考圖。
- Task ID：網頁版不顯示，以 Model Info 截圖為準，存本機 `art/source/licenses/tripo/<物件 ID>_info.png`。
- 授權：Tripo Pro（可商用，方案到期 2027-10-23）；Blender 手工物件為自製。
- 真實照片參考：`art/source/<dish_id>/photo_ref/`（Wikimedia Commons，來源網址與授權在同資料夾 `sources.txt`），只當內部比對，不上傳 GitHub、不當 Tripo 輸入。
- 共通的 Blender 修改：合併重複頂點、重算法線、縮放（1 單位 = 10 cm）、原點在底部中心、壓平最底 2–3%、減面到 ≤ 3,000 三角面、凸包碰撞 `-convcolonly`（約 100–200 面）；掛點 Empty 的 Z 軸朝外（匯出後是 Godot +Y）；進湯物件 4–8 個 `Buoyancy_*`。
- Blender 原始檔：`art/source/<dish_id>/<dish_id>.blend`（`raw` 集合是 Tripo 原檔，`food` 集合是清理後；`dish_preview` 只是預覽）；共用腳本 `art/source/_tools/bl_helpers.py`。
- 預覽圖（含真實照片對照）：`art/source/<dish_id>/preview_compare.png`。

### 容器（Blender，新料理）
- 管道：Blender 手工；複製 `tableware.blend` 既有的碗盤再縮放（共用回紋貼圖與顏色，流程文件 6.1；D-20261023-06）；碰撞 `<物件>-colonly`（凹面，只能用在固定物件）
- 原始檔：art/source/shared/tableware.blend

| 物件 ID | 料理 | 來源形狀 | 尺寸（cm） | 三角面 | 匯出 |
|---|---|---|---|---|---|
| bowl_meatball_soup | meatball_soup | bowl_noodle 縮放 | 直徑 14.2、高 7.0 | 3,072 | art/models/meatball_soup/bowl_meatball_soup.glb |
| plate_century_egg_tofu | century_egg_tofu | plate_dumpling_small 改成圓角長方（超橢圓 n=5） | 15.6×10.3×2.0 | 2,688 | art/models/century_egg_tofu/plate_century_egg_tofu.glb |
| plate_gua_bao | gua_bao | plate_dumpling 縮放 | 直徑 20、高 2.3 | 2,688 | art/models/gua_bao/plate_gua_bao.glb |
| bowl_oyster_misua | oyster_misua | bowl_noodle 縮放 | 直徑 13.1、高 7.0 | 3,072 | art/models/oyster_misua/bowl_oyster_misua.glb |
| bowl_pho | pho | bowl_noodle 放大 | 直徑 21.2、高 9.0 | 3,072 | art/models/pho/bowl_pho.glb |

### 貢丸湯食物（meatball_soup，2026-11-22）
- 參考圖：art/source/meatball_soup/ref_meatball.png、ref_fried_shallot.png（prompt 照範本 2.1，加上風格基準圖前綴）
- 原始檔：art/source/meatball_soup/tripo_meatball.glb、tripo_fried_shallot.glb；Blender 檔 art/source/meatball_soup/meatball_soup.blend
- 使用點數：參考圖 2 批 80 ＋ 3D 2×35 ＋ 貼圖 2×20 = 190 點

| 物件 ID | 中文名 | 管道 | 尺寸（cm） | 三角面／貼圖 | 碰撞 | 掛點 | 浮力點 | Model Info 生成時間 |
|---|---|---|---|---|---|---|---|---|
| food_meatball_whole | 貢丸 | Tripo | 3.4×3.4×2.8 | 2,974／512² | 凸包 ×1 | `Anchor_Meatball_Top_01`、`_Side_01`、`_Bottom_01` | 6 | 2026-11-22 10:58:10 |
| food_meatball_half | 半顆貢丸（切面朝下） | 同一個 Tripo 模型用 Blender 切半、補切面（材質 `meatball_inside`） | 2.8×3.4×1.7 | 1,766／512²＋純色 | 凸包 ×1 | `Anchor_MeatballHalf_Top_01`（圓頂）、`_Side_01`、`_Bottom_01`（切面） | 4 | 同上 |
| food_fried_shallot | 油蔥酥小堆 | Tripo | 2.6×2.6×1.0 | 2,885／512² | 凸包 ×1 | `Anchor_FriedShallot_Top_01`、`_Bottom_01` | 4 | 2026-11-22 11:09:40 |
| decoy_celery_a／_b／_c | 芹菜末（C 形薄片／短弧塊／小方丁） | Blender 手工 | 0.8×0.4×0.2／0.6×0.2×0.3／0.5×0.35×0.3 | 708／708／60，雙材質純色 | 凸包 ×1 | — | 4 | — |

- 貼圖修色：Tripo 貢丸偏鮭魚橘，已在 Blender 降飽和、偏灰粉褐（對照真實照片）；油蔥酥原本亮橘，已改成金黃褐。
- 芹菜末顏色：外皮 sRGB (150,196,112)、切面 (208,228,172)，灰階約 0.67／0.85；香菜貼圖灰階中位數 0.21（浸濕）–0.41（亮綠），差 ≥ 0.25，輪廓是 C 形／方丁，和香菜的扇形葉不同。
- 建議密度：貢丸 1.05（略沉、會在湯裡半浮）、半顆貢丸 1.05、油蔥酥 0.5（浮在湯面）、芹菜末 0.7（浮）。
- 半顆貢丸切面朝下比較穩；要看到切面，玩家要翻面。

### 皮蛋豆腐食物（century_egg_tofu，2026-11-22）
- 參考圖：art/source/century_egg_tofu/ref_century_egg_wedge_a.png、_b.png（同一批 2 張，各轉一個 3D）
- 原始檔：art/source/century_egg_tofu/tripo_century_egg_wedge_a.glb、_b.glb；Blender 檔 art/source/century_egg_tofu/century_egg_tofu.blend
- 使用點數：參考圖 1 批 40 ＋ 3D 2×35 ＋ 貼圖 2×20 = 150 點（第 3 塊改用 Blender 從 A 變形，省 95 點）

| 物件 ID | 中文名 | 管道 | 尺寸（cm） | 三角面／貼圖 | 碰撞 | 掛點 | Model Info 生成時間 |
|---|---|---|---|---|---|---|---|
| food_century_egg_wedge_a | 皮蛋塊 A（厚楔形） | Tripo | 3.5×3.6×3.1 | 2,980／512² | 凸包 ×1 | `Anchor_EggWedgeA_Top_01`、`_Side_01`、`_Bottom_01` | 2026-11-22 11:42:06 |
| food_century_egg_wedge_b | 皮蛋塊 B（半月片，切面朝上） | Tripo | 4.0×3.4×2.0 | 2,902／512² | 凸包 ×1 | `Anchor_EggWedgeB_*`（同上） | 2026-11-22 11:38:57 |
| food_century_egg_wedge_c | 皮蛋塊 C（小塊） | Blender：A 縮 0.8、鏡像、轉 70° | 3.0×2.7×2.5 | 2,980／共用 A 貼圖 | 凸包 ×1 | `Anchor_EggWedgeC_*`（同上） | 同 A |
| food_tofu_block | 豆腐塊 | Blender 手工（圓角方塊，頂面微凸） | 8.0×6.0×3.5 | 300／純色 | 凸包 ×1 | `Anchor_TofuBlock_Top_01`–`_03`、`_Side_01`、`_Bottom_01` | — |
| food_bonito_flake_a／_b／_c | 柴魚片 | Blender 手工（捲曲薄片，厚 1.2 mm，順紋深色條） | 2.3×1.5×1.1／1.4×1.4×1.1／1.7×1.1×0.7 | 476，雙材質純色 | 凸包 ×1 | — | — |
| deco_sauce_film | 醬汁膜（不能互動，放在豆腐下） | Blender 手工 | 9.1×6.1×0.1 | 160／純色 | 無 | — | — |

- 皮蛋貼圖重新上色（對照真實照片）：Tripo 的蛋白偏紅橘，改成深茶褐 sRGB 約 (78,44,22)；蛋黃改成深石板灰 (44,48,50)（不帶綠），外圈與中心是奶油色 (212,204,156)。蛋黃灰階約 0.18、外圈約 0.79，香菜 0.21–0.41；輪廓是楔形／半月，和香菜的扇形葉不同。
- 建議密度：皮蛋 1.1、豆腐 1.05（軟，建議高摩擦低彈性）、柴魚片 0.4（建議高阻力、低重力影響，程式端調）。
- 豆腐是一整塊，不切；香菜可放在豆腐頂面（3 個掛點）。

### 刈包食物（gua_bao，2026-11-22）
- 參考圖：art/source/gua_bao/ref_bun.png、ref_pork_belly_a.png、_b.png（同一批）、ref_suan_cai.png
- 原始檔：art/source/gua_bao/tripo_bun.glb、tripo_pork_belly_a.glb、_b.glb、tripo_suan_cai.glb；Blender 檔 art/source/gua_bao/gua_bao.blend
- 使用點數：參考圖 4 批 160（三層肉第 1 批太像巧克力蛋糕，重抽 1 次）＋ 3D 4×35 ＋ 貼圖 4×20 = 380 點

| 物件 ID | 中文名 | 管道 | 尺寸（cm） | 三角面／貼圖 | 碰撞 | 掛點 | Model Info 生成時間 |
|---|---|---|---|---|---|---|---|
| food_gua_bao_bun | 刈包皮（合起來，一整個剛體） | Tripo | 7.5×9.5×3.4 | 2,959／512² | 凸包 ×1 | `Anchor_GuaBao_Top_01`、`_Bottom_01` | 2026-11-22 11:51:46 |
| food_gua_bao_bun_bottom | 刈包皮下半（可打開版） | 同一個 Tripo 模型在接縫高度（1.8 cm）切開、補內面（材質 `bun_inside`） | 7.5×9.5×1.8 | 2,199 | 凸包 ×1 | `Anchor_BunBottom_Inside_01`、`_02`（內面，放餡料處）、`_Bottom_01`；`Hinge`（鉸鏈線，見下） | 同上 |
| food_gua_bao_bun_top | 刈包皮上半（蓋子） | 同上 | 7.4×9.5×1.6 | 1,388 | 凸包 ×1 | `Anchor_BunTop_Inside_01`（內面）、`_Top_01` | 同上 |
| food_pork_belly_a／_b | 三層肉片（波浪／較平） | Tripo（同一批 2 張各轉一個） | 7.0×3.3×1.8／7.0×2.9×1.8 | 2,974／2,950，512² | 凸包 ×1 | `Anchor_PorkBelly_Top_01`、`_Side_01`、`_Bottom_01` | 11:57:24／12:01:19 |
| decoy_suan_cai_a／_b／_c | 酸菜碎（整堆／半堆／小塊） | a 是 Tripo；b、c 用 Blender 從 a 切出來 | 3.6×3.6×1.4／2.0×3.6×1.4／1.4×2.0×1.3 | 2,975／1,803／820，512² | 凸包 ×1 | — | 12:06:04 |
| food_peanut_powder | 花生粉堆 | Blender 手工（顆粒用程式繪製的貼圖，俯視投影 UV） | 4.7×3.6×1.1 | 960／512² | 凸包 ×1 | `Anchor_PeanutPowder_Top_01`、`_02` | — |

- 可打開的刈包：下半原點在底部中心；**上半原點就在鉸鏈線上**（刈包皮 +X 側、接縫高度），所以把上半放在下半的 `Hinge` 位置、繞 Y 軸（Blender Y = Godot −Z）轉正角度就會往上翻開。預覽圖是轉 115°。合起來的 `food_gua_bao_bun` 給不需要打開的關卡用。
- 貼圖修色：刈包皮原本偏黃，改成奶白；三層肉肥肉帶改成淡象牙粉 (226,196,166)、瘦肉暖紅褐 (146,78,50)；酸菜原本是鮮黃（像起司通心粉），改成淡黃橄欖色，灰階中位數 0.69（p10 0.61），香菜 0.21–0.41，輪廓是碎塊堆，不是葉片。
- 建議密度：刈包皮 0.5（軟、輕）、三層肉 1.0、酸菜 0.8、花生粉 0.6。
- 和真實照片比對（art/source/gua_bao/photo_ref/）：刈包皮、三層肉的形狀與顏色相符；真實的酸菜是深橄欖綠的細絲，和香菜灰階太接近，所以刻意改成淡黃橄欖色、做成碎塊堆（遊戲辨識度優先，偏離寫實）。

### 蚵仔麵線食物（oyster_misua，第 1 部分，2026-11-22）
- 用 11/22 剩下的點數先做蚵仔、大腸各 1 個；第 2 個造型、麵線團 ×2 在 11/27 做（見第 2 部分）。
- 參考圖：art/source/oyster_misua/ref_oyster.png、ref_intestine.png；原始檔 tripo_oyster.glb、tripo_intestine.glb；Blender 檔 art/source/oyster_misua/oyster_misua.blend
- 使用點數：參考圖 2 批 80 ＋ 3D 2×35 ＋ 貼圖 2×20 = 190 點

| 物件 ID | 中文名 | 管道 | 尺寸（cm） | 三角面／貼圖 | 碰撞 | 掛點 | 浮力點 | Model Info 生成時間 |
|---|---|---|---|---|---|---|---|---|
| food_oyster_a | 蚵仔（裹粉） | Tripo | 3.2×2.0×1.1 | 2,971／512² | 凸包 ×1 | `Anchor_Oyster_Top_01`、`_Bottom_01` | 4 | 2026-11-22 12:37:59 |
| food_intestine_a | 大腸段（中空） | Tripo（模型本身就是真的中空管） | 1.9×2.6×1.8（管軸沿 Blender Y＝Godot −Z） | 2,930／512² | **凸包 ×4**（`food_intestine_a_wall1`–`4-convcolonly`，繞管軸分 4 片管壁，中間的洞是空的） | `Anchor_Intestine_Top_01`、`_Bottom_01`、`_Inside_01`（管洞正中央，Z 軸沿管軸，給「塞在大腸裡」的香菜用） | 4 | 2026-11-22 12:42:42 |
| food_garlic_paste | 蒜泥小堆 | Blender 手工 | 1.8×1.7×0.6 | 528／256² | 凸包 ×1 | `Anchor_GarlicPaste_Top_01` | 4 | — |
| deco_misua_strands_a／_b／_c | 散麵線（裝飾，不能互動） | Blender 手工（曲線轉網格，紅麵線色） | 長 6.1–8.5，粗 0.13 | 576–1,152 | 無 | — | — | — |

- 和真實照片比對（art/source/oyster_misua/photo_ref/）：蚵仔是灰米色本體＋深灰荷葉邊，原本偏黃，已降飽和；大腸原本偏橘，已調成較暗的焦糖褐。
- 大腸的 4 片凸包碰撞會留出中間的洞；程式要把這 4 個碰撞形狀都搬到同一個 RigidBody 底下。
- 建議密度：蚵仔 1.05、大腸 1.0（濃湯裡半浮）、蒜泥 1.0。
- 蚵仔麵線的湯是不透明的勾芡濃湯，需要程式另外做不透明濃湯 shader（沉在湯裡的物件看不到，要靠提示或撈起來）。

### 越南河粉食物（pho，2026-11-27）
- 參考圖：art/source/pho/ref_thai_basil.png、ref_mint.png、ref_beef.png、ref_noodle.png、ref_lime.png；原始檔 tripo_*.glb；Blender 檔 art/source/pho/pho.blend
- 真實照片：art/source/pho/photo_ref/（牛肉河粉 3 張、九層塔、薄荷、檸檬角；來源與授權見 sources.txt）
- 使用點數：3D 5×35 ＋ 貼圖 5×20 = 275 點（這次 GPT Image 2 參考圖在免費額度內，0 點；河粉參考圖第 1 批像烏龍麵，重抽 1 次也是 0 點）。第 2 種造型全部用 Blender 改，沒有另外生成。

| 物件 ID | 中文名 | 管道 | 尺寸（cm） | 三角面／貼圖 | 碰撞 | 掛點 | 浮力點 | Model Info 生成時間 |
|---|---|---|---|---|---|---|---|---|
| food_pho_beef_a | 牛肉片 A | Tripo，Blender 壓薄到 0.5 cm | 4.5×6.0×0.5 | 2,975／512² | 凸包 ×1 | `Anchor_PhoBeef_Top_01`、`_Bottom_01` | 4 | 2026-11-27 21:03:16 |
| food_pho_beef_b | 牛肉片 B | Blender：A 切掉一端、縮 0.9、轉 35° | 4.6×4.4×0.4 | 2,115 | 凸包 ×1 | 同上 | 4 | 同 A |
| food_pho_noodle_a | 河粉團 A（寬扁麵） | Tripo | 5.1×6.0×2.3 | 2,975／512² | 凸包 ×1 | `Anchor_PhoNoodle_Top_01`、`_Side_01`、`_Bottom_01` | 6 | 2026-11-27 21:08:32 |
| food_pho_noodle_b | 河粉團 B | Blender：A 非等比縮放、轉 80° | 5.7×4.3×1.9 | 2,975 | 凸包 ×1 | 同上 | 6 | 同 A |
| food_lime_wedge | 檸檬角 | Tripo | 4.2×3.4×2.6 | 2,759／512² | 凸包 ×1 | `Anchor_LimeWedge_Top_01`、`_Side_01`、`_Bottom_01` | 4 | 2026-11-27 21:13:04 |
| decoy_thai_basil_a | 九層塔葉（誘餌） | Tripo＋減面＋PCA 壓平（照香菜流程） | 1.9×4.5×0.25 | 596／512² | 凸包 ×1 | — | 4 | 2026-11-27 20:54:44 |
| decoy_thai_basil_b | 九層塔葉 B | Blender：A 縮 0.75、葉面微捲、轉 20° | 1.6×3.2×0.33 | 596 | 凸包 ×1 | — | 4 | 同 A |
| decoy_mint_a | 薄荷葉（誘餌） | Tripo＋減面＋PCA 壓平 | 2.2×3.4×0.3 | 596／512² | 凸包 ×1 | — | 4 | 2026-11-27 20:59:04 |
| decoy_mint_b | 薄荷葉 B | Blender：A 縮 0.78、葉面微捲、轉 −25° | 1.8×2.4×0.39 | 596 | 凸包 ×1 | — | 4 | 同 A |
| food_bean_sprout_a／_b／_c | 豆芽 | Blender 手工（11/22 已做，補回掛點與浮力點） | 4.5–5.6 長 | 564 | 凸包 ×1 | `Anchor_BeanSprout_Top_01` | 4 | — |
| bowl_pho | 大湯碗 | Blender（容器表） | 直徑 21.2、高 9.0 | 3,072 | 凹面 `-colonly` | — | — | — |

- **和香菜的辨識度（這道最關鍵）：**
  - 九層塔：重新上色成深墨綠＋紫色葉柄，葉片灰階約 0.15（p90 0.15），葉柄約 0.2；形狀是窄長尖葉、全緣（沒有鋸齒和裂片）。
  - 薄荷：重新上色成亮黃綠，灰階 p10 0.67、中位數 0.72；形狀是橢圓皺葉、細鋸齒。
  - 香菜貼圖灰階：亮綠 0.40、深綠 0.32、浸濕 0.21。所以**河粉關卡建議只用亮綠香菜**（cilantro_*_light）：九層塔差 0.25、薄荷差 0.27，兩者都達到 M6 的 ≥0.25。若用深綠或浸濕香菜，九層塔的亮度差會不足（只剩 0.06–0.17），這時只能靠形狀區分，或請程式的 CilantroContrast 描邊加強。
  - 灰階對照圖：art/source/pho/preview_parts_gray.png（上排彩色、下排灰階，最右是亮綠香菜）。
- 修色：牛肉片中心的粉紅太亮，已降飽和成灰褐帶淡粉（對照真實照片）；檸檬角原本太鮮黃綠，已降飽和；河粉偏暖白。
- 建議密度：牛肉片 1.05、河粉團 1.02（湯裡半沉）、檸檬角 0.95、九層塔／薄荷 0.6（浮在湯面）、豆芽 0.8。

### 蚵仔麵線食物（oyster_misua，第 2 部分，2026-11-27）
- 參考圖：art/source/oyster_misua/ref_misua_clump.png；原始檔 tripo_misua_clump.glb
- 使用點數：3D 35 ＋ 貼圖 20 = 55 點（參考圖在免費額度內 0 點）；其餘 3 個用 Blender 改，0 點

| 物件 ID | 中文名 | 管道 | 尺寸（cm） | 三角面／貼圖 | 碰撞 | 掛點 | 浮力點 | Model Info 生成時間 |
|---|---|---|---|---|---|---|---|---|
| food_misua_clump_a | 麵線團 A | Tripo | 5.7×4.9×1.6 | 2,974／512² | 凸包 ×1 | `Anchor_MisuaClump_Top_01`、`_Bottom_01` | 6 | 2026-11-27 21:21:11 |
| food_misua_clump_b | 麵線團 B | Blender：A 非等比縮放、轉 70° | 4.1×4.4×1.9 | 2,974 | 凸包 ×1 | 同上 | 6 | 同 A |
| food_oyster_b | 蚵仔 B | Blender：A 鏡像、縮 0.85、微彎、轉 40° | 2.5×2.4×1.1 | 2,971 | 凸包 ×1 | `Anchor_Oyster_Top_01`、`_Bottom_01` | 4 | 同 food_oyster_a |
| food_intestine_b | 大腸段 B（短胖） | Blender：A 沿管軸縮 0.72、徑向放大 1.08 | 2.0×1.9×2.0 | 2,930 | 凸包 ×4（`food_intestine_b_wall1`–`4-convcolonly`，中空） | `Anchor_Intestine_Top_01`、`_Bottom_01`、`_Inside_01` | 4 | 同 food_intestine_a |

- 麵線團貼圖：Tripo 原本是橘紅色，對照真實照片改成淡褐棕。
- 建議密度：麵線團 1.03（勾芡濃湯裡半沉）。
