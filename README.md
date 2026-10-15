# 思惟力量會議助手

Windows 會議錄音、完整音檔分段轉錄與摘要工具。基於 [Meetily 社區版](https://github.com/Zackriya-Solutions/meetily) 修改，**非 Meetily / Zackriya Solutions 官方發行版本**。

## 思惟力量與聯繫方式

- 公司網站：[思惟力量](http://www.thinkingpower.com.tw)
- 聯繫信箱：[service@thinkingpower.com.tw](mailto:service@thinkingpower.com.tw)
- 軟體「關於」頁面亦提供以上連結，目前未加入收款或贊助資訊。

## 0.4.3 原始碼更新（2026-10-15）

**[下載 0.4.3 完整包（含 FFmpeg）](https://github.com/thinkingpowerai-ux/thinkingpower-meeting-assistant/releases/download/v0.4.3/thinkingpower-meeting-0.4.3.zip)**

先關閉舊版，完整解壓至新資料夾，執行 `meetily.exe`。`ffmpeg.exe` 已放在主程式旁，不必執行準備腳本。需要 Windows x64 與 WebView2；AI 模型另於程式中下載，雲端 Key 由每位使用者自行設定。測試範圍及限制見下方。

[版本說明與 SHA256](https://github.com/thinkingpowerai-ux/thinkingpower-meeting-assistant/releases/tag/v0.4.3)。Repo 的 `modified-source.zip` 為同版本修改原始碼。

- 停止收音後先排空音訊佇列、完成原音保存，再執行完整音檔分段轉錄。
- 錄音期間不再執行即時 Whisper，避免同一段音訊重複辨識。
- 保留停止時最後不足一個處理區塊的音訊；保存錯誤明確回報，不自動開始轉錄。
- FFmpeg 找不到時於開始錄音前提示，不再於錄音流程中隱性下載；優先尋找主程式旁的 ffmpeg.exe。
- 整包附 FFmpeg 執行檔、GPLv3 授權、上游 README 及 FFmpeg 8.0.1 來源碼；第三方連結函式庫來源資料完整性仍待獨立核對，不宣稱整包全為 MIT。

驗證：前端與 Windows 原生建置通過；260 項測試通過、5 項略過、1 項因無播放裝置未執行。另以預備包的 FFmpeg 通過 4 項保存／合併測試。開發機 15 秒合成音訊保存加解碼檢查約 0.81 秒，**不是 AI 轉錄耗時，也不是筆電效能測試**。

未完成：本次真人麥克風停止與播放驗收、Acer 筆電實測、1 小時比較、雲端實際呼叫、新版截圖 Word 手冊。舊手冊中的即時轉錄及 FFmpeg 準備說明不代表 0.4.3 流程。

正常停止才可確認已完成保存。當機／強制關閉只能嘗試復原已落盤檢查點；未寫入音訊及磁碟錯誤無法保證保全。

## 0.4.2 舊版下載與第一次使用

舊版 Windows 下載：**0.4.2 本機驗證預覽版**。請到 [Releases](https://github.com/thinkingpowerai-ux/thinkingpower-meeting-assistant/releases) 下載 `thinkingpower-meeting-0.4.2.zip`，完整解壓至可寫入資料夾。

1. 閱讀包內「先閱讀.txt」及附實際畫面的 Word 操作手冊。
2. 使用 Windows x64 與 WebView2 執行階段。執行 `Prepare-FFmpeg.ps1` 從固定上游下載並核對 SHA256；FFmpeg 不隨本包散布。若系統限制腳本，請依「先閱讀.txt」手動準備，不要停用安全防護。
3. 執行 `meetily.exe`。本機模型需另外下載；本包不含 Whisper、Qwen、Gemma 權重。
4. 設定語音轉錄與摘要服務。雲端服務使用每位使用者自己的 API Key，ChatGPT 訂閱不包含 API 費用。
5. 先用非敏感短錄音驗證，再處理正式會議。

## 功能

- 實體／線上會議、匯入音檔；可選擇錄製視窗或只錄聲音。
- 保留原音 → 完整音檔分段轉錄 → 儲存逐字稿 → 選擇自動摘要。
- 分別選擇轉錄及摘要服務，支援本機／雲端混搭；可重試摘要而不重跑已完成的轉錄。
- 原音播放、時間點對照、TXT / Markdown 匯出、繁體中文操作介面。
- Windows DPAPI 保護服務 Key；單一服務共用連線設定，不同服務分開設定。

設定納入內建 AI、Claude、自訂 OpenAI 相容伺服器、Groq、Ollama、OpenAI、OpenRouter。**列入設定不代表所有服務都能接收音訊，也不代表已通過真實 API 驗收。**語音選單依支援能力與端點驗證限制，Claude / Ollama 為文字摘要用途。

## 0.4.2 歷史驗證與限制

- 已通過 258 項程式測試（5 項略過），前端建置，以及模擬服務錯誤／跨服務流程。
- 31.10 秒合成中文音檔：Small CPU 轉錄約 30.82 秒；另一次本機摘要測試約 62.91 秒。這些不是一小時效能或完整流程合計時間。
- 已驗證本機逐字稿與自動摘要、原音雜湊保存、關閉重開、匯出；使用者確認播放有聲。發布前已重新啟動執行檔。
- **所有雲端服務、Ollama 均尚未完成實際呼叫驗證**；未執行付費或一小時比較，沒有實際雲端帳單資料。
- 本次啟動仍未偵測到麥克風，最新版真人收音、畫面與音訊同步、乾淨電腦全新安裝、GPU 加速尚未完成實機驗收。
- 辨識可能有錯字；摘要可能推測負責人或期限，需對照原音。正常保存成功不保證當機、強制關閉或磁碟錯誤時完全不遺失音訊。

## 原始碼與修改

`modified-source.zip` 是本次經清理的完整修改原始碼快照，解壓後為 `source/`，包含前端、Rust/Tauri 後端、鎖檔與建置腳本。使用其中的 README 與 frontend/package.json 查閱開發指令。需自行準備 Node/pnpm、Rust MSVC、CMake/LLVM 及相應原生依賴；尚未在乾淨電腦重新建置驗證。

此公開倉庫從乾淨快照建立，沒有上傳私人工作目錄或本機 Git 歷史。可自由依 MIT 修改本專案程式；第三方套件、素材、模型仍依各自授權。

## 授權與資料保護

保留原作者 Copyright (c) 2024 Zackriya Solutions 及完整 [MIT 授權](LICENSE.md)。修改部分 Copyright (c) 2026 思惟力量 contributors，同樣採 MIT。完整第三方授權、相依套件清單及所需來源碼附於下載包，見 [NOTICE.md](NOTICE.md)。

公開包不包含使用者錄音、逐字稿、資料庫、API Key 或測試憑證；操作手冊使用合成示範資料。執行後的個人資料存於 Windows 使用者資料夾，請勿將已使用的資料夾整包公開。提交問題時請先移除音檔、Key、個資與敏感逐字稿。
