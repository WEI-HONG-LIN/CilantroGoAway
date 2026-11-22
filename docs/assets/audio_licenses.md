# 音效授權紀錄

每個外部音效或音樂素材一筆：檔名、來源、作者、授權條款、是否可商用。授權不明的素材不使用。

## M6 程序生成音效（自製，無外部素材）

| 檔名 | 來源 | 作者 | 授權 | 可商用 |
|---|---|---|---|---|
| `audio/sfx/land_<meat/noodle/leaf/default>_<table/ceramic/food>_<01–03>.wav`（36 個） | `audio/source/sfx_build_m6.py` 程序生成（Python 標準函式庫合成：低頻撞擊＋濾波噪音＋落點共鳴分音） | 本專案（Claude，遊戲邏輯程式 session） | 自製，專案所有 | 是 |
| `audio/sfx/discard_last.wav` | 同上：以既有 `discard.wav` 疊加升五度、升八度兩聲與閃亮尾音 | 本專案 | 同 `discard.wav` 的授權（audio-staging 交件時的紀錄） | 同 `discard.wav` |

- 響度：落地音效最響 50 ms 約 -19 dBFS（葉菜 -23），遊戲中再乘 0.7（-3 dB）；「叮」`discard.wav` 約 -14.8 dBFS，落地最大聲時仍比「叮」小 7 dB 以上（企劃書 4.4 要求至少 3 dB）。
- 起音：36 個落地音效與 `grab_chopsticks`、`grab_tweezers`、`scoop` 起音都 ≤ 10 ms（量測：0.1–7.5 ms），不需要裁切。

### M6 觸發規則（音效觸發表合併後併入）

| 事件 ID | 觸發 | 備註 |
|---|---|---|
| `grab_chopsticks`／`grab_tweezers`／`scoop` | 改由 `ToolController.cilantro_plucked(piece, tool_id)` 觸發（命中鎖定的同一個畫格） | ±3% 音高 |
| `discard` | 香菜飛進棄置碟、計數更新時；4 秒內連續挑除每次升一個半音，最多 4 次，超過 4 秒歸零 | |
| `discard_last` | 最後一株的「叮」（長版）；缺檔退回 `discard` | 新增 |
| `land_<材質>_<落點>` | 食物落地。材質取自物理材質 `resources/physics_materials/food_<材質>.tres`；落點用碰撞對象（或上層節點）的群組：`land_table`（桌面）、`land_ceramic`（碗、盤、醬碟、暫放盤）；FoodItem／FixedFood（飯）＝ food。落進湯裡不播（由 `splash` 處理）。變體 `_01`–`_03` 不連續重複同一個，±5% 音高，音量 = 撞擊強度 × 0.7 | 新增；缺檔退回 `land_<材質>` → `land` |
