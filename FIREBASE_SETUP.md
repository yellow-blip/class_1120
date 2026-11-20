# Firebase Google 登入與 Firestore

`index.html` 使用 Firebase 專案 `daymark-efc26`，透過 Firebase Authentication 的 Google provider 登入。Cloud Firestore 的 `(default)` Standard 資料庫已建立於 `asia-east1 (Taiwan)`，目前使用 Spark 方案。

Firestore 規則目前限制登入者只能讀寫自己的路徑：`users/{uid}/events/{eventId}` 與 `users/{uid}/tasks/{taskId}`。規則依應用程式預期資料路徑設定；正式對外分享前，請再依實際欄位與使用情境檢視及驗證。

登入後，頁面會載入該帳號的行程與任務；新增、編輯、變更任務完成狀態會保存至 Firestore。登出時顯示的是頁面內範例資料，不會同步至雲端。新帳號的資料庫子集合一開始為空，第一次新增資料後才會出現在 Firestore。

Firebase Web App config 位於前端，屬公開設定；請在 Google Cloud/Firebase 將 API key 限制為允許的網站來源。若在本機測試，請透過 HTTP 開發伺服器開啟網站，並在 Firebase Authentication 的 Authorized domains 加入 `localhost`；不要使用 `file://`。