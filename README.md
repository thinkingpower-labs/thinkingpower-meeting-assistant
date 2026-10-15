# 思惟力量會議助手

Windows 會議錄音、完整音檔分段轉錄與摘要工具。基於 [Meetily 社區版](https://github.com/Zackriya-Solutions/meetily) 修改，**非 Meetily / Zackriya Solutions 官方發行版本**。

## 思惟力量與聯繫方式

- 公司網站：[思惟力量](http://www.thinkingpower.com.tw)
- 聯繫信箱：[service@thinkingpower.com.tw](mailto:service@thinkingpower.com.tw)
- 軟體「關於」頁面亦提供以上連結，目前未加入收款或贊助資訊。

## 下載與第一次使用

目前版本：**0.4.2 本機驗證預覽版**。請到 [Releases](https://github.com/thinkingpowerai-ux/thinkingpower-meeting-assistant/releases) 下載 `thinkingpower-meeting-0.4.2.zip`，完整解壓至可寫入資料夾。

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

## 驗證與限制

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
