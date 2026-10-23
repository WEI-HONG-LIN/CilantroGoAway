# 《香菜退散！》Cilantro Hunter

Godot 4.5（GDScript、Jolt Physics）的 3D Q 版休閒尋物遊戲：玩家把料理中的食物拿起、翻面，找出香菜並用筷子、鑷子或湯匙挑掉。食物放下時遵循物理；湯有浮力、漣漪與攪動。先做 PC 滑鼠版 MVP。

## 文件（唯一的正式版本都在這個 repo）

| 內容 | 位置 |
|---|---|
| 企劃書（玩法規則，目前 v1.1） | `香菜退散_Godot遊戲企劃書.md` |
| 決策紀錄 | `docs/decisions.md` |
| 所有角色必守的規範 | `docs/roles/00_共同規範.md` |
| 各角色的目標與規範 | `docs/roles/01_製作人.md` … `08_測試遊玩QA.md` |
| Tripo3D 建模流程與 prompt | `docs/pipeline/` |
| v1.0 分析紀錄（已全部定案） | `docs/企劃分析與待確認事項.md` |

文件和你的記憶或對話內容不一致時，以 repo 裡的文件為準。規格沒寫到的事，先問，不要自己假設。

## 角色

本專案由多個 Claude Code session 分別扮演不同的開發角色。開始工作前：

1. 確認你這次的角色（使用者會在第一句話指定，或以 `--agent` 啟動）。沒有指定就先問。
2. 讀 `docs/roles/00_共同規範.md` 和自己的角色文件，照裡面的規範工作。
3. `git pull origin main`，拿到其他角色最新合併的成果。

| 角色 | Agent 名稱 | 負責修改的位置 |
|---|---|---|
| 01 製作人 | `producer` | `docs/decisions.md`、`docs/backlog.md`、`docs/reports/` |
| 02 遊戲企劃 | `game-designer` | `香菜退散_Godot遊戲企劃書.md`、`docs/specs/` |
| 03 關卡設計 | `level-designer` | `resources/levels/`、`docs/levels/` |
| 04 3D 美術 | `artist-3d` | `art/`、`shaders/`、`docs/pipeline/` |
| 05 UI／UX 設計 | `ui-ux-designer` | `scenes/ui/`、`scripts/ui/`、`art/ui/` |
| 06 遊戲邏輯程式 | `gameplay-programmer` | `project.godot`、`scenes/`（`ui/` 除外）、`scripts/`（`ui/` 除外）、`resources/`（`levels/` 除外）、`tests/` |
| 07 音效設計 | `sound-designer` | `audio/` |
| 08 測試遊玩 | `qa-tester` | `docs/qa/` |

**只修改自己負責的位置。** 需要別的角色改東西時，寫在 PR 描述的「需要誰接手」，或在 `docs/` 的對應文件提出，不要直接改別人的檔案。

## Git 規則

- 不要直接推到 `main`。每個任務開一個分支：`role/<agent 名稱>-<任務>`，例如 `role/gameplay-programmer-m0-physics`。
- 一個分支只做一件事；完成後開 PR 到 `main`，PR 描述使用 `00_共同規範.md` 的「交付」格式。
- 開工前與開 PR 前都先 `git pull origin main`（或 rebase），減少衝突。
- 二進位資產（模型、圖片、音效、字型等）由 `.gitattributes` 自動交給 Git LFS 管理，第一次使用前要在電腦上執行一次 `git lfs install`；`.godot/` 不進版控（見 `.gitignore`）。
- 只留在本機、不上傳的檔案放在 `art/_local/`，例如 Tripo 原始下載檔、試做的參考圖、草稿。

## 目前進度

M0 技術驗證（物理放下與浮力原型）尚未開始。里程碑見企劃書 9.2。
