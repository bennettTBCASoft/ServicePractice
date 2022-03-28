# Service

### Service 介紹
> Activity 離開畫面後會進入停止狀態，此時Activity無法被控制，除非透過執行緒處理相關控制，但如果應用程式完全關閉，那執行緒也gg，此時開發者需使用『Service』處理應用程式消失後要繼續執行的特定任務。

> **Service** 是應用程式的元件之一，它用於**背景處理與使用者介面無關的長時間任務**，即使切換到其他的應用程式也會繼續執行，因此能在應用程式關閉後執行特定的任務，例如：訊息通知、資料下載或音樂播放等...

### 建立 Service
1. File -> New -> Service -> Service
2. 修改 Service 的 Class Name 後，點選 Finish 按鈕
3. Android Studio 會自動產生 Service 所需要的檔案，在 AndroidManifest.xml 也會自動增加 service 的資訊


### 啟動 Service
- 在 Activity 啟動 Service ，可使用 Intent 傳入 **startService() 方法**
    `startService(Intent(this, MyService::class.java))`
    > Intent 內部傳入啟動與被啟動者，即當前 Activity(this) 與 Service(MyService::class.java)
- 在 Activity 關閉 Service ，可使用 Intent 傳入 **stopService() 方法**，
    `stopService(Intent(this, MyService::class.jaba))`
    > Intent內部傳入停止與被停止者，即當前 Activity(this) 與 Service(MyService::class.java)


### OnStartCommand()方法
- 介紹
> Service 被啟動後會執行 onCreate()方法，並自動呼叫 **onStartCommand() 方法**，我們可以將要執行的程式撰寫在 **onStartCommand() 方法**中，而當Service需要結束時，呼叫 **stopSelf() 方法**讓他結束程序，此時會進入onDestroy() 的環節。
> onStartCommand() 方法是Service最重要的執行階段，它會告訴系統如何重啟Servoce，如異常是否要重新啟動。而執行中的Service如果又接收到Activity發出startService()的請求，Service會執行onStartCommand()，而不會再次執行onCreate()。換言之，onStartCommand()扮演著**接受外來請求並操作 Service 的角色**

- onStartCommand()
1. 第一個參數 **Intent** 可接收由Activity啟動時夾帶的資訊
2. 第二個參數 **flags** 表示啟動服務的方式
3. 第三個參數 **startId** 為啟動的識別標籤
4. 返回值：需要回傳整數，且必須是以下三種常數之一


| 返回常數 | 解釋 |
| -------- | -------- |
| START_NOT_STICKY     | 若Service被終止時，便結束服務不再建立。     |
| START_STICKY     | 若Service被終止時，系統會嘗試重啟，並再次執行onStartCommand()，但不會重傳Intent的資料     |
| START_REDELIVER_STICKY     | 與上面不同的是，此方法Intent的資料會被重傳     |



###### tags: `kotlin` `Service`
