# Angular 相關學習

要部署您的應用程序，您必須對其進行編譯，然後將JavaScript，CSS和HTML託管在Web服務器上。內置的Angular應用程序具有很高的可移植性，可以在任何環境中生活或可以由任何技術提供服務，例如Node，Java，.NET，PHP等。

## 建置

透過CMD安裝

```install
npm install -g @angular/cli
```

建立一個新專案  
**這專案建立其實就像建一個資料夾一樣，所以會建議你切換到你要的位置後再建立專案**

```建立專案
ng new my-project-name
```  

建置我們雲端下載下來的資料，將/src文件夾替換為StackBlitz下載的文件夾，然後執行構建。  
[github下載，我看官方練習的範例檔](https://github.com/yuan29r/angular-gr6oy9)  
建置時，要注意要在你的專案資料夾下，才能下指令建置喔！

```建置
ng build --prod
```

這將產生您需要部署的文件。

> 如果以上ng build命令引發有關缺少軟件包的錯誤，請將缺失的依賴項附加到本地項目的package.json文件中，以匹配下載的StackBlitz項目中的依賴項。

## 運行應用程序

1.轉到工作區文件夾。  
2.使用ng serve帶有--open選項的CLI命令啟動服務器。

```serve
cd 專案資料夾
ng serve --open 或 ng serve -o
```  

## 繫結語法：概覽

繫結的型別可以根據資料流的方向分成三類： 從資料來源到檢視、從檢視到資料來源以及雙向的從檢視到資料來源再到檢視。

| 資料方向 ( Data direction )  | 語法 ( Syntax )   | 繫結型別 ( Type )     |
| :---------------------------------- | :------------------- |:---------------|
| 單向 One-way</br>從資料來源到檢視 </br>from data source to view target | {{expression}}</br>[target]="expression"</br>bind-target="expression" | 插值 [Interpolation]</br>屬性 [Property]</br>屬性 [Attribute]</br>CSS 類 [Class]</br>樣式 [Style] |
| 從檢視到資料來源的單向繫結</br>One-way from view target to data source | (target)="statement"</br>on-target="statement"                 | 事件 [Event] |
| 雙向 </br>Two-way                  | [(target)]="expression"</br>bindon-target="expression"                  | 雙向 [Two-way]  |

譯註：由於 HTML attribute 和 DOM property 在中文中都被翻譯成了“屬性”，無法區分。

**除了插值之外的繫結型別，在等號左邊是目標名， 無論是包在括號中 ([]、()) 還是用字首形式 (bind-、on-、bindon-) 。**

### HTML attribute 與 DOM property 的對比

要想理解 Angular 繫結如何工作，重點是搞清 HTML attribute 和 DOM property 之間的區別。  

attribute 是由 HTML 定義的。property 是由 DOM (Document Object Model) 定義的。

- 少量 HTML attribute 和 property 之間有著 1:1 的對映，如 id。
- 有些 HTML attribute 沒有對應的 property，如 colspan。  
- 有些 DOM property 沒有對應的 attribute，如 textContent。  
- 大量 HTML attribute 看起來對映到了 property…… 但卻不像你想的那樣！  

最後一類尤其讓人困惑…… 除非你能理解這個普遍原則：  
attribute 初始化 DOM property，然後它們的任務就完成了。property 的值可以改變；attribute 的值不能改變。  
例如，當瀏覽器渲染 ```<input type="text" value="Bob">``` 時，它將建立相應 DOM 節點， 它的 value 這個 property 被初始化為 “Bob”。

當用戶在輸入框中輸入 “Sally” 時，DOM 元素的 value 這個 property 變成了 “Sally”。 但是該 HTML 的 value 這個 attribute 保持不變。如果你讀取 input 元素的 attribute，就會發現確實沒變： input.getAttribute('value') // 返回 "Bob"。
HTML 的 value 這個 attribute 指定了初始值；DOM 的 value 這個 property 是當前值。

disabled 這個 attribute 是另一種特例。按鈕的 disabled 這個 property 是 false，因為預設情況下按鈕是可用的。 當你新增 disabled 這個 attribute 時，只要它出現了按鈕的 disabled 這個 property 就初始化為 true，於是按鈕就被禁用了。

新增或刪除 disabled 這個 attribute 會禁用或啟用這個按鈕。但 attribute 的值無關緊要，這就是你為什麼沒法透過 ```<button disabled="false">仍被禁用</button>``` 這種寫法來啟用按鈕。  

設定按鈕的 disabled 這個 property（如，透過 Angular 繫結）可以禁用或啟用這個按鈕。這就是 property 的價值。  

就算名字相同，HTML attribute 和 DOM property 也不是同一樣東西。

***在 Angular 的世界中，attribute 唯一的作用是用來初始化元素和指令的狀態。 當進行資料繫結時，只是在與元素和指令的 property 和事件打交道，而 attribute 就完全靠邊站了。***

## 繫結目標

| 繫結型別 type                  | 目標 target            | 範例          |
| :------------------- | :------------------- |:---------------|
| 屬性</br>Property  | 元素的 property</br>元件的 property</br>指令的 property | \<img [src]="heroImageUrl"></br>\<app-hero-detail [hero]="currentHero"><\/app-hero-detail></br>\<div [ngClass]="{'special': isSpecial}"><\/div> |
| 事件</br>Event                | 元素的事件Element event</br>元件的事件Component event</br>指令的事件Directive event   | \<button (click)="onSave()">Save<\/button></br>\<app-hero-detail (deleteRequest)="deleteHero()"><\/app-hero-detail></br>\<div (myClick)="clicked=$event" clickable>click me<\/div>            |
| 雙向          | 事件與 property    | \<input [(ngModel)]="name">    |
| Attribute     | attribute（例外情況）| \<button [attr.aria-label]="help">help<\/button>  |
| CSS 類        | class property      | \<div [class.special]="isSpecial">Special<\/div>              |
| 樣式          | style property      | \<button [style.color]="isSpecial ? 'red' : 'green'">         |

## 生命週期的順序

當 Angular 使用建構函式新建一個元件或指令後，就會按下面的順序在特定時刻呼叫這些生命週期鉤子方法：

| 鉤子 Hook            | 用途及時機 Purpose and Timing                |
| :------------------- | :------------------- |
| ngOnChanges()  | 當 Angular（重新）設定資料繫結輸入屬性時響應。 該方法接受當前和上一屬性值的 SimpleChanges 物件</br>在 ngOnInit() 之前以及所繫結的一個或多個輸入屬性的值發生變化時都會呼叫。 |
| ngOnInit()                 | 在 Angular 第一次顯示資料繫結和設定指令/元件的輸入屬性之後，初始化指令/元件。</br>在第一輪 ngOnChanges() 完成之後呼叫，只調用一次。                 |
| ngDoCheck()                  | 檢測，並在發生 Angular 無法或不願意自己檢測的變化時作出反應。</br>在每個變更檢測週期中，緊跟在 ngOnChanges() 和 ngOnInit() 後面呼叫。                 |
| ngAfterContentInit()         | 當 Angular 把外部內容投影進元件/指令的檢視之後呼叫。</br>第一次 ngDoCheck() 之後呼叫，只調用一次。                   |
| ngAfterContentChecked()      | 每當 Angular 完成被投影元件內容的變更檢測之後呼叫。</br>ngAfterContentInit() 和每次 ngDoCheck() 之後呼叫                  |
| ngAfterViewInit()            | 當 Angular 初始化完元件檢視及其子檢視之後呼叫。</br>第一次 ngAfterContentChecked() 之後呼叫，只調用一次。                   |
| ngAfterViewChecked()         | 每當 Angular 做完元件檢視和子檢視的變更檢測之後呼叫。</br>ngAfterViewInit() 和每次 ngAfterContentChecked() 之後呼叫。                 |
| ngOnDestroy()                | 每當 Angular 每次銷毀指令/元件之前呼叫並清掃。 在這兒反訂閱可觀察物件和分離事件處理器，以防記憶體洩漏。</br>在 Angular 銷毀指令/元件之前呼叫。                   |
