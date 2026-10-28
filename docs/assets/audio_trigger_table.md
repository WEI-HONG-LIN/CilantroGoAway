# 音效觸發表

音效檔名就是事件 ID：`audio/sfx/<事件ID>.wav`（音效設計決定，依決策 D-20261023-03 的命名權責）。之後支援變體時用 `<事件ID>_01.wav`、`_02.wav`。程式播放時會隨機偏移音高 ±5%。

規格：16-bit、44.1 kHz、單聲道 wav；峰值 ≤ -1 dBFS；響度用 ITU-R BS.1770（LUFS）量測。

| 事件 ID | 觸發時機 | 匯流排 | 長度 | 響度 | 聲音 |
|---|---|---|---:|---:|---|
| `ui_click` | 按下任何木牌按鈕 | SFX（建議 UI） | 0.12 秒 | -20.0 LUFS | 木牌輕敲「叩」 |
| `ui_pause` | 打開暫停選單 | SFX（建議 UI） | 0.44 秒 | -21.0 LUFS | 柔和下降兩音 |
| `tool_switch` | 切換餐具 | SFX | 0.22 秒 | -21.0 LUFS | 餐具輕碰「喀啦」 |
| `ui_sign_drop` | 選關「售完」木牌開始晃動時（level_select.gd `_play_tag_drops()`，每塊木牌 tween_interval 結束時） | SFX（建議 UI） | 1.14 秒 | -21.0 LUFS | 售完木牌晃三下後掉落（從開始晃動時播放） |
| `food_pickup` | 拿起食物（點擊檢查或開始搬動） | SFX | 0.07 秒 | -21.0 LUFS | 輕「啵」 |
| `land` | 食物落地，找不到細分材質時 | SFX | 0.12 秒 | -21.0 LUFS | 通用軟落地（退回用） |
| `land_meat` | 肉類落地，音量依撞擊強度 | SFX | 0.11 秒 | -21.0 LUFS | 肉塊落地，軟軟的「噗」 |
| `land_noodle` | 麵條落地，音量依撞擊強度 | SFX | 0.13 秒 | -21.0 LUFS | 麵條濕軟「啪噠」 |
| `land_leaf` | 葉菜落地，音量依撞擊強度 | SFX | 0.15 秒 | -25.0 LUFS | 葉菜落地，很輕的「沙」 |
| `drop_rejected` | 放不下（落點被擋住） | SFX | 0.23 秒 | -23.0 LUFS | 溫和低音「嘟嘟」 |
| `grab_chopsticks` | 筷子夾住香菜 | SFX | 0.13 秒 | -20.0 LUFS | 木筷清脆「喀」 |
| `grab_tweezers` | 鑷子夾住香菜 | SFX | 0.22 秒 | -22.0 LUFS | 鑷子小「叮」（壓低高頻） |
| `scoop` | 湯匙撈起 | SFX | 0.35 秒 | -21.0 LUFS | 舀水「咕嚕」 |
| `discard` | 香菜飛進棄置碟（`cilantro_removed`） | SFX | 0.69 秒 | -18.0 LUFS | 清脆「叮！」挑除成功 |
| `misgrab` | 誤夾蔥花或食物本體 | SFX | 0.32 秒 | -23.0 LUFS | 溫和滑掉「咻」 |
| `slip` | 碎葉從筷子滑掉 | SFX | 0.16 秒 | -24.0 LUFS | 碎葉滑掉「滋溜」 |
| `splash` | 東西掉進湯裡（`object_splashed`），音量依速度 | SFX | 0.34 秒 | -20.0 LUFS | 「噗通」 |
| `stir` | 攪動中每 0.5 秒最多一次，音量依強度 | SFX | 0.45 秒 | -25.0 LUFS | 水流「唰」 |
| `hint_sniff` | 提示煙霧出現 | SFX | 0.36 秒 | -24.0 LUFS | 嗅嗅兩聲 |
| `hint_bubble` | 提示的香菜沉在湯底時，和 hint_sniff 一起播 | SFX | 0.47 秒 | -23.0 LUFS | 咕嘟冒泡 |
| `tip_show` | 教學紙條出現（音量 0.6） | SFX（建議 UI） | 0.22 秒 | -24.0 LUFS | 紙條「唰」 |
| `tip_check` | 教學紙條打勾 | SFX（建議 UI） | 0.42 秒 | -22.0 LUFS | 筆劃一勾＋小叮 |
| `level_clear` | 最後一株香菜挑完（`level_completed`） | SFX | 2.13 秒 | -17.0 LUFS | 木琴上行小號角＋閃亮鐘聲 |
| `star` | 結算星星落下（每顆一次） | SFX（建議 UI） | 0.49 秒 | -20.0 LUFS | 星星「叮」 |
| `stamp` | 結算蓋章 | SFX（建議 UI） | 0.25 秒 | -18.0 LUFS | 木章「咚」 |

## 音樂

| ID | 時機 | 匯流排 | 狀態 |
|---|---|---|---|
| `audio/music/menu.ogg` | 主選單與選關 | Music | 來源待定 |
| `audio/music/level.ogg` | 關卡循環 | Music | 來源待定 |
