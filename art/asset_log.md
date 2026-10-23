# 資產紀錄

每個資產一筆，格式見 `docs/pipeline/tripo3d_料理建模流程.md` 第 9 節。標示「待補」的欄位由生成者補上。

### food_beef_chunk_a
- 料理：beef_noodle_soup
- 角色：**風格基準物件**（整個專案的 Q 版質感基準）
- 管道：Tripo 網頁版（Tripo Studio），Pro 方案，Privacy = Sharing Only（見授權）
- 參考圖：`art/source/style_anchor/beef_noodle_soup_beef_chunk_a.png`（待上傳；2026-10-23 11:58 第 5 輪，GPT Image 2，選第 1 張：長方塊、切面兩條細肌腱）
- 參考圖的圖像模型與 prompt：GPT Image 2；prompt 全文見 `docs/pipeline/tripo3d_prompt範本.md` 5.2「牛肉塊 A」
- 參考圖試做歷程（5 輪）：
  1. 初版（cube、tendon stripe）：變成緞帶包起來的方塊，肉色像生肉
  2. 加入 flower shape、inset、amber jelly、mahogany：變成巧克力夾心糖
  3. 以 fibrous、torn-looking 描述（GPT Image 2.5）：寫實濕亮的美食照
  4. 比較 GPT Image 2 與 2.5：2 偏霧面黏土、2.5 偏濕亮；定案用 GPT Image 2
  5. 加 TOY 收尾句、肌腱改為 thin lines：通過（見範本 2.5 的經驗）
- 風格基準圖：本物件就是基準
- 生成方式：圖片生 3D（Smart Mesh 分頁，Generate 3D 從 Image 分頁帶入）
- 3D 模型版本：P1.0 – Fast
- 設定：Topology Triangle、Polycount 3000；第 1 次生成，未使用 Free Retry
- Task ID：無（網頁版 History：2026-10-23 12:10 幾何、12:17 第一次貼圖、Current 第二次貼圖）
- Seeds：網頁版無 seed
- 貼圖：幾何完成後按 Texture（20 點）上了 2 次；PBR／Remove Lighting／品質的實際設定與第二次的差異：待補
- 匯出：GLB、貼圖 512；檔案 `art/source/beef_noodle_soup/`（待上傳，建議檔名 `food_beef_chunk_a_tex1.glb`、`_tex2.glb`、`_geo.glb`）
- 三角面：2980（匯出前預覽顯示）；頂點 1997（含貼圖切縫）
- Blender 修改：尚未清理。待辦：外皮調色（偏橘 → 醬褐）與 AO；切面推到齊平外皮；底面確認平整；比例縮到 4×3×2.5 cm（0.4×0.3×0.25 單位）；原點到底部中心；凸包碰撞 `-convcolonly`；重心；`Anchor_BeefChunk_*`；`Buoyancy_*`
- 使用點數：P1.0 幾何 35 + Texture 20 × 2 次（第二次待確認）＋ 參考圖點數（待補）
- 授權：Tripo Pro 方案；生成時 Privacy 為 Sharing Only（公開分享）。商業使用權待核對 `www.tripo3d.ai` 的條款；**放進正式遊戲前必須解決**（改用私人生成或確認條款）
