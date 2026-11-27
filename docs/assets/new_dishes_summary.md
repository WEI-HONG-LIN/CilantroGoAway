# 五道新料理建模總清單（3D 美術，2026-11-27）

> dish_id 都是暫定名（meatball_soup／century_egg_tofu／gua_bao／oyster_misua／pho），物件 ID 與掛點名稱是 3D 美術的提案，待遊戲企劃確認。
> 模型、原始檔、預覽圖都只在本機（決策 D-20261023-02）；逐項資產紀錄見 `docs/assets/asset_log.md` 的「新料理」各節。
> 每道料理的預覽＋真實照片對照：`art/source/<dish_id>/preview_compare.png`（本機）。

## 1. 點數

| 日期 | 料理 | Tripo 物件 | 點數 |
|---|---|---|---:|
| 11-22 | 貢丸湯 | 貢丸、油蔥酥 | 190 |
| 11-22 | 皮蛋豆腐 | 皮蛋塊 A、B | 150 |
| 11-22 | 刈包 | 刈包皮、三層肉 A、B、酸菜（三層肉參考圖重抽 1 次） | 380 |
| 11-22 | 蚵仔麵線（1） | 蚵仔 A、大腸 A | 190 |
| 11-27 | 越南河粉 | 牛肉片、河粉團、檸檬角、九層塔、薄荷（參考圖免費） | 275 |
| 11-27 | 蚵仔麵線（2） | 麵線團 A（參考圖免費） | 55 |
| | **合計** | 18 個 Tripo 模型 | **1,240** |

- 11-22 那期點數（950）用掉 910，剩 40 點過期；11-23 重置為 3,000，目前剩 **2,670** 點。
- 每個 Tripo 模型：P1.0 35 ＋ 貼圖 20 = 55 點；GPT Image 2 一批 2 張 40 點（11-27 在免費額度內 0 點）。
- 第 2 種造型、切半、碎塊盡量用 Blender 從同一個 Tripo 模型改，共省下約 12 個模型（約 660 點）。

## 2. 模型清單（`art/models/<dish_id>/`）

| 料理 | 可互動食物 | 誘餌 | 裝飾／容器 |
|---|---|---|---|
| 貢丸湯 meatball_soup | food_meatball_whole、food_meatball_half（Blender 切）、food_fried_shallot | decoy_celery_a／b／c | bowl_meatball_soup（14 cm） |
| 皮蛋豆腐 century_egg_tofu | food_century_egg_wedge_a／b／c（c 是 Blender）、food_tofu_block、food_bonito_flake_a／b／c | — | deco_sauce_film、plate_century_egg_tofu（圓角長方） |
| 刈包 gua_bao | food_gua_bao_bun（合起來）、food_gua_bao_bun_bottom＋_top（可打開）、food_pork_belly_a／b、food_peanut_powder | decoy_suan_cai_a／b／c | plate_gua_bao（20 cm） |
| 蚵仔麵線 oyster_misua | food_oyster_a／b、food_intestine_a／b（中空）、food_misua_clump_a／b、food_garlic_paste | — | deco_misua_strands_a／b／c、bowl_oyster_misua（13 cm） |
| 越南河粉 pho | food_pho_beef_a／b、food_pho_noodle_a／b、food_lime_wedge、food_bean_sprout_a／b／c | decoy_thai_basil_a／b、decoy_mint_a／b | bowl_pho（21 cm） |

所有可互動物件：1 單位 = 10 cm、原點在底部中心、≤ 3,000 三角面（葉子 ≈ 600）、`-convcolonly` 凸包碰撞、`Anchor_*` 掛點；會進湯的物件有 `Buoyancy_*`。容器用 `tableware.blend` 的共用回紋貼圖，碰撞 `-colonly`。

## 3. 需要接手的事項

### 06 遊戲邏輯程式
1. **匯入與組裝**：每個 `.glb` 做成 FoodItem 場景；把 `-convcolonly` 搬到 RigidBody 底下。**大腸（food_intestine_a／b）有 4 片管壁凸包**，要全部放在同一個 RigidBody 下，中間的洞才會是空的（香菜可塞入，掛點 `Anchor_Intestine_Inside_01` 在洞中央）。
2. **刈包可打開**：`food_gua_bao_bun_top` 的原點就在鉸鏈線；放在 `food_gua_bao_bun_bottom` 的 `Hinge` 位置，繞 Hinge 的軸轉正角度就會翻開（預覽用 115°）。建議共用 2-1 的夾開／翻開機制；不需要打開的關卡用合起來的 `food_gua_bao_bun`。
3. **蚵仔麵線需要不透明的勾芡濃湯 shader**（湯色約 sRGB (140,100,64)，可攪動、物件沉下去看不到），和現有半透明清湯不同；沉底的蚵仔／大腸要靠提示或撈起。
4. **柴魚片（food_bonito_flake_*）要高阻力、低密度**（建議 0.4，落下要飄），避免像硬片一樣彈跳。
5. **葉子誘餌（九層塔、薄荷、芹菜末、酸菜）**：建議密度 0.6–0.8，浮在湯面。
6. 建議密度一覽（資產紀錄裡每道都有）：貢丸 1.05、油蔥酥 0.5、皮蛋 1.1、豆腐 1.05、刈包皮 0.5、三層肉 1.0、蚵仔 1.05、大腸 1.0、麵線團 1.03、牛肉片 1.05、河粉團 1.02、檸檬角 0.95。

### 03 關卡設計
1. **越南河粉關卡只用亮綠香菜（cilantro_*_light）**：
   - 香菜貼圖灰階：亮綠 0.40、深綠 0.32、浸濕 0.21。
   - 九層塔（深墨綠＋紫柄）灰階約 0.15，薄荷（亮黃綠）約 0.72。
   - 用亮綠香菜時兩者亮度差 0.25／0.27，達到 M6 的 ≥ 0.25；用深綠或浸濕香菜時九層塔只差 0.06–0.17，只能靠形狀（窄長全緣葉 vs 扇形裂葉）或 CilantroContrast 描邊。
   - 灰階對照：`art/source/pho/preview_parts_gray.png`（本機）。
2. 掛點：各物件的 `Anchor_*` 都是 3D 美術先放的提案，需要依掛點需求表調整時再告訴 3D 美術。
3. 香菜藏點建議：大腸洞內（Inside 錨點）、刈包內面（BunBottom／BunTop_Inside）、豆腐頂面、麵線團頂。

### 02 遊戲企劃
1. 確認 dish_id、物件 ID、掛點名稱，並登記到企劃書 3.1。
2. **酸菜刻意偏離寫實**：真實酸菜是深橄欖綠細絲，和香菜灰階太接近，所以做成淡黃橄欖色的碎塊堆（灰階 0.69）。若要寫實的深綠色，需要另訂區分方式。
3. **皮蛋蛋黃**用深石板灰（不帶綠）、奶油色外圈，避免和香菜混淆。
4. 新誘餌：芹菜末（貢丸湯）、酸菜（刈包）、九層塔、薄荷（越南河粉）；是否列入企劃書誘餌清單請決定。
5. 半顆貢丸、切開的皮蛋都是切面朝下擺放（物理較穩），玩家要翻面才看得到切面。

### 08 測試遊玩 QA
- 以上都只在 Blender 預覽驗證過，**還沒放進 Godot 測物理與辨識度**（3 高度 × 3 角度落下、灰階截圖）。程式組裝後需要跑一次 M6 的 legibility_check。
