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
- 後處理：<待補>
- Blender 修改：尚未清理
- 最終三角面數／貼圖：<待補>
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
- Blender 修改：尚未清理；底部有筋的溝但沒有筋的顏色，可接受，清理時壓平
- 最終三角面數／貼圖：<待補>
- 使用點數：<待補>
- 授權：Tripo Pro（可商用；使用者確認 2026-10-23）。證明：訂閱收據＋生成紀錄截圖，存本機 `art/source/licenses/tripo/`


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
- 三角面數：712／372／1,228；材質各 2 個（主色＋藍色）
- 動畫：筷子、鑷子各有 `grip`（12 格）
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
