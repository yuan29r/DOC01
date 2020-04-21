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

## 透過 Angular CLI 建立 Component

可以使用 VSCode 下方的終端機 (按下 Ctrl + ` 開啟)，值得注意的是 Angular CLI Component 類型不只有一種，可以輸入以下指令查看它可以幫我們產生哪些 Component 範本：
```CLI-help
ng generate -h
or
ng g -h
以上兩種，指令結果是一樣的
```

執行後可以得知它還能幫我們產生以下這些 Component 範本

>Generates and/or modifies files based on a schematic.</br>
>usage: ng generate <schematic> [options]</br>
>- arguments:</br>
>   - **schematic**</br>
>    The schematic or collection:schematic to generate.</br>
>   - **options:**</br>
>     - _--defaults_</br>
>    When true, disables interactive input prompts for options with a >default.</br>
>     - _--dry-run (-d)_</br>
>    When true, runs through and reports activity without writing out results.</br>
>     - _--force (-f)_</br>
>    When true, forces overwriting of existing files.</br>
>     - _--help_</br>
>    Shows a help message for this command in the console.</br>
>     - _--interactive_</br>
>    When false, disables interactive input prompts.</br>
</br>
>   - **Available Schematics:**</br>
>     - Collection "@schematics/angular" (default):</br>
>       - appShell</br>
>       - application</br>
>       - class</br>
>       - component</br>
>       - directive</br>
>       - enum</br>
>       - guard</br>
>       - interceptor</br>
>       - interface</br>
>       - library</br>
>       - module</br>
>       - pipe</br>
>       - service</br>
>       - serviceWorker</br>
>       - webWorker</br>

如果要透過 Angular CLI 建立 Component ，並且把這個元件加到 AppComponent 下，以下指令擇一即可。

```component
完整指令
ng generate component myFirstCompoent

簡寫指令
ng g c myFirstCompoent
g:generate簡寫
c:component簡寫
```

建立module and route，這些預先建立有好處，在module_name內容會註冊route模組，之後再建立component時，會自己把元件都註冊到module_name，所以建議可以先建立這個在建立元件。

```一次建立module and route
建立module and route
ng g m module_name --routing=true
g:generate簡寫
m:module簡寫
--routing=true 這是請他順便建立route檔
```

- route內容設定小提醒
  - path:''  //代表當url為空的時候，則預設要開啟哪一個component。
  - path:'**'  //代表當url的內容不再設定的路由內容當中，或是任意輸入的時候，則預設要開啟哪一個component。

>其中這部分有一個很需要注意的地方：
由於我們的routes是宣告為一個陣列，也就是說他會從第0筆開始去做mapping，如果失敗則往下一個進行，因此path:'**'千萬不能擺放在第0筆的位置，否則你怎麼輸入都只會開啟預設的那個component。  

## 繫結語法：概覽

繫結的型別可以根據資料流的方向分成三類： 從資料來源到檢視、從檢視到資料來源以及雙向的從檢視到資料來源再到檢視。

| 資料方向 ( Data direction )  | 語法 ( Syntax )   | 繫結型別 ( Type )     |
| :---------------------------------- | :------------------- |:---------------|
| 單向 One-way</br>從資料來源到檢視 </br>from data source to view target | {{expression}}</br>[target]="expression"</br>bind-target="expression" | 插值 [Interpolation]</br>屬性 [Property]</br>屬性 [Attribute]</br>CSS 類 [Class]</br>樣式 [Style] |
| 從檢視到資料來源的單向繫結</br>One-way from view target to data source | (target)="statement"</br>on-target="statement"                 | 事件 [Event] |
| 雙向 </br>Two-way                  | [(target)]="expression"</br>bindon-target="expression"                  | 雙向 [Two-way]  |

譯註：由於 HTML attribute 和 DOM property 在中文中都被翻譯成了"屬性"，無法區分。

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
例如，當瀏覽器渲染 ```<input type="text" value="Bob">``` 時，它將建立相應 DOM 節點， 它的 value 這個 property 被初始化為 "Bob"。

當用戶在輸入框中輸入 "Sally" 時，DOM 元素的 value 這個 property 變成了 "Sally"。 但是該 HTML 的 value 這個 attribute 保持不變。如果你讀取 input 元素的 attribute，就會發現確實沒變： input.getAttribute('value') // 返回 "Bob"。
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

## 元件之間的互動

### @Input

VScode如果有出現 "the directive input property should not be renamed" 類似訊息時，可以用兩種方式讓這個訊息不提示。

```input關閉錯誤提醒
方法一：
tslint.json檔案，關閉規則
"no-input-rename": false

方法二：
// lint:disable-next-line:no-input-rename
@Input('appAvatarColor') name: string;
```

下圖是官方範例截圖出來畫畫線  

![@input圖解說明](https://github.com/yuan29r/DOC01/blob/master/ngPic/input01.jpg "@input圖解說明")

### 透過 setter 截聽輸入屬性值的變化

下圖是官方範例截圖出來畫畫線  

![setter圖解說明](https://github.com/yuan29r/DOC01/blob/master/ngPic/setter01.jpg "setter圖解說明")

### 透過ngOnChanges()來截聽輸入屬性值的變化

下圖是官方範例截圖出來畫畫線  
當需要監視多個、互動式輸入屬性的時候，本方法比用屬性的 setter 更合適。
監測輸入屬性 major 和 minor 的變化，並把這些變化編寫成日誌以報告這些變化。

![setter圖解說明](https://github.com/yuan29r/DOC01/blob/master/ngPic/ngOnChanges01.jpg "setter圖解說明")

### 父元件監聽子元件的事件

子元件暴露一個 EventEmitter 屬性，當事件發生時，子元件利用該屬性 emits(向上彈射)事件。父元件繫結到這個事件屬性，並在事件發生時作出迴應。
子元件的 EventEmitter 屬性是一個輸出屬性，通常帶有@Output 裝飾器，就像在 VoterComponent 中看到的。

![emit圖解說明](https://github.com/yuan29r/DOC01/blob/master/ngPic/emit01.jpg "emit圖解說明")

### 父元件與子元件透過本地變數互動

父元件不能使用資料繫結來讀取子元件的屬性或呼叫子元件的方法。但可以在父元件範本裡，新建一個本地變數來代表子元件，然後利用這個變數來讀取子元件的屬性和呼叫子元件的方法

![child-via-local-variable01圖解說明](https://github.com/yuan29r/DOC01/blob/master/ngPic/child-via-local-variable01.jpg "child-via-local-variable01圖解說明")

### 父元件呼叫@ViewChild()

本地變數方法是個簡單便利的方法。但是它也有侷限性，因為父元件-子元件的連線必須全部在父元件的範本中進行。父元件本身的程式碼對子元件沒有訪問權。

如果父元件的類需要讀取子元件的屬性值或呼叫子元件的方法，就不能使用本地變數方法。

當父元件類需要這種訪問時，可以把子元件作為 ViewChild，注入到父元件裡面。

由本地變數切換到 ViewChild 技術的唯一目的就是做示範。

![Viewchild圖解說明](https://github.com/yuan29r/DOC01/blob/master/ngPic/Viewchild01.jpg "Viewchild圖解說明")

### 父元件和子元件透過服務來通訊

父元件和它的子元件共享同一個服務，利用該服務在元件家族內部實現雙向通訊。

該服務例項的作用域被限制在父元件和其子元件內。這個元件子樹之外的元件將無法訪問該服務或者與它們通訊。

這個 MissionService 把 MissionControlComponent 和多個 AstronautComponent 子元件連線起來。

MissionControlComponent 提供服務的例項，並將其共享給它的子元件(透過 providers 元資料陣列)，子元件可以透過建構函式將該例項注入到自身。

![service injectable圖解說明](https://github.com/yuan29r/DOC01/blob/master/ngPic/injectable01.jpg "service injectable圖解說明")

### 透過 ngModel 追蹤修改狀態與有效性驗證

在表單中使用 ngModel 可以獲得比僅使用雙向資料繫結更多的控制權。它還會告訴你很多資訊：使用者碰過此控制元件嗎？它的值變化了嗎？資料變得無效了嗎？

NgModel 指令不僅僅追蹤狀態。它還使用特定的 Angular CSS 類來更新控制元件，以反映當前狀態。 可以利用這些 CSS 類來修改控制元件的外觀，顯示或隱藏訊息。

| 狀態                 | 為真時的 CSS 類 (Class if true)    | 為假時的 CSS 類 (Class if false)        |
| :------------------- | ------------------- |---------------|
| 控制元件被訪問過。</br>The control has been visited.  | ng-touched | ng-untouched |
| 控制元件的值變化了。</br>The control's value has changed.    | ng-dirty    | ng-pristine  |
| 控制元件的值有效。</br>The control's value is valid.   | ng-valid         | ng-invalid    |

## 多專案實作

建立一個沒有應用程式結構的專案

```建立新專案
**ng new ngDemoProjects --create-application=false --routing false --style css**
or
**ng new ngDemoProjects --createApplication="false"**(注意大小)

這兩個指令件出來的結果是一樣的
```

切換資料夾ngDemoProjects

```切換資料夾
**cd ngDemoProjects**
```

建立應用程式demo1 ( 建立應用程式時，專案預設會建立在 ./projects 目錄下！)

```建立應用程式demo1
**ng g application demo1 --routing**
```

建立 Angular Library 函式庫專案

```建立函式庫專案
**ng g library yuan-lib01 --prefix=yuan**
```

使用 npm run build 或 ng build 就會自動建置angular.json理預設=>"defaultProject": "demo1" ，因此預設會建置這個專案

```建置這個專案
ng build
```

如果還有其他專案想要建置可以這樣子寫 ng build demo2 或 ng build --project demo2

```建置其他專案
ng build yuan-lib01
```

專案根目錄下的 tsconfig.json 檔案，裡面有個 "paths" 區段設定，替 TypeScript 的編譯器指出 import 路徑的別名

```tsconfig
"paths": {
      "yuan-lib01": [
        "dist/yuan-lib01/yuan-lib01",
        "dist/yuan-lib01"
      ]
    }
```

也就是說，在這個 monorepo 專案中，任何一個子專案都可以透過 yuan-lib01' 來 import 函式庫中的任何模組或服務元件：

```import lib
**import { YuanLib01Module } from 'yuan-lib01';**
```

## cookie 套件

[ngx-cookie-service安裝](https://www.npmjs.com/package/ngx-cookie-service)

```ngx-cookie-service
npm install ngx-cookie-service
or
npm i ngx-cookie-service
```

### 注意

Angular 9 IVY Ready service for cookies. Originally based on the ng2-cookies library.

For versions <9, please use 2.3.0 version of library.

## moment and ngx-moment 套件安裝

[moment日期時間套件](https://github.com/urish/ngx-moment)

```moment安裝
npm install --save moment ngx-moment
```

使用時需要 import * as moment from 'moment';
ngx-moment是基於moment上做延伸開發的，所以import需要注意moment也需要

## CKEditor 5 安裝

[CKEditor 官方文件教學](https://ckeditor.com/docs/ckeditor5/latest/builds/guides/integration/frameworks/angular.html)

```CKEditor 5
安裝CK5
npm install --save @ckeditor/ckeditor5-angular
安裝設定配置
npm install --save @ckeditor/ckeditor5-build-classic
npm install --save @ckeditor/ckeditor5-build-decoupled-document
```

現在，添加CKEditorModule到其組件將使用<ckeditor>其模板中的組件的模塊。

```CKEditorModule
import { CKEditorModule } from '@ckeditor/ckeditor5-angular';

@NgModule( {
    imports: [
        CKEditorModule,
        // ...
    ],
    // ...
} )
```

將編輯器版本導入到Angular組件中，並將其分配給一個public屬性，以使其可從模板訪問：

```編輯器版本導入
import * as ClassicEditor from '@ckeditor/ckeditor5-build-classic';

@Component( {
    // ...
} )
export class MyComponent {
    public Editor = ClassicEditor;
    // ...
}
```

最後，使用ckeditor模板中的標記運行富文本格式編輯器：

```開始用編輯器
<ckeditor [editor]="Editor" data="<p>Hello, world!</p>"></ckeditor>
```
### 支持的@Input屬性

@InputAngular的CKEditor 5 RTF編輯器組件支持以下屬性：

#### editor (required)

The [Editor](https://ckeditor.com/docs/ckeditor5/latest/builds/guides/integration/basic-api.html) which provides the static [create()](https://ckeditor.com/docs/ckeditor5/latest/api/module_core_editor_editor-Editor.html#static-function-create) method to create an instance of the editor:

```editor
<ckeditor [editor]="Editor"></ckeditor>
```

#### EditorConfig

[EditorConfig 官方文件教學](https://ckeditor.com/docs/ckeditor5/latest/api/module_core_editor_editorconfig-EditorConfig.html)

```EditorConfig 範例
<ckeditor [config]="{ toolbar: [ 'heading', '|', 'bold', 'italic' ] }" ...></ckeditor>
```

#### data

The initial data of the editor. It can be a static value:

```ckeditor data
<ckeditor data="<p>Hello, world!</p>" ...></ckeditor>
```

或共享父組件的屬性(shared parent component's property)

```shared parent component's property
@Component( {
    // ...
} )
export class MyComponent {
    public editorData = '<p>Hello, world!</p>';
    // ...
}
```

``` html
<ckeditor [data]="editorData" ...></ckeditor>
```

#### tagName

```指定tagName
將在其上創建富文本編輯器的HTML元素的標籤名稱。
默認標記為<div>。
<ckeditor tagName="textarea" ...></ckeditor>
```

#### disabled

控制編輯器的只讀狀態：


```disabled
@Component( {
    // ...
} )
export class MyComponent {
    public isDisabled = false;
    // ...
    toggleDisabled() {
        this.isDisabled = !this.isDisabled
    }
}
```

``` disabled html:
<ckeditor [disabled]="isDisabled" ...></ckeditor>

<button (click)="toggleDisabled()">
    {{ isDisabled ? 'Enable editor' : 'Disable editor' }}
</button>
```

#### watchdog

[ContextWatchdog](https://ckeditor.com/docs/ckeditor5/latest/api/module_watchdog_contextwatchdog-ContextWatchdog.html)該類的實例負責為多個編輯器實例提供相同的上下文，並在發生崩潰時重新啟動整個結構。

```watchdog
import CKSource from 'path/to/custom/build';

const Context = CKSource.Context;
const Editor = CKSource.Editor;
const ContextWatchdog = CKSource.ContextWatchdog;

@Component( {
    // ...
} )
export class MyComponent {
    public editor = Editor;
    public watchdog: any;
    public ready = false;

    ngOnInit() {
        const contextConfig = {};

        this.watchdog = new ContextWatchdog( Context );

        this.watchdog.create( contextConfig )
            .then( () => {
                this.ready = true;
            } );
    }
}
```

```watchdog html
<div *ngIf="ready">
    <ckeditor [watchdog]="watchdog" ...></ckeditor>
    <ckeditor [watchdog]="watchdog" ...></ckeditor>
    <ckeditor [watchdog]="watchdog" ...></ckeditor>
</div>
```

### 支持的@Output屬性

@OutputAngular的CKEditor 5 RTF編輯器組件支持以下屬性：

#### ready

編輯器準備就緒時觸發。它與[editor#ready](https://ckeditor.com/docs/ckeditor5/latest/api/module_core_editor_editor-Editor.html#event-ready)事件相對應。
它與編輯器實例一起觸發。

請注意，可能多次調用此方法。除了初始化外，崩潰後重新啟動編輯器時也會調用它。不要在內部保留對編輯器實例的引用，因為在重新啟動的情況下它將更改。相反，您應該使用watchdog.editor屬性。

#### change

當編輯器的內容更改時觸發。它與[editor.model.document#change:data](https://ckeditor.com/docs/ckeditor5/latest/api/module_engine_model_document-Document.html#event-change:data)事件相對應。
它使用包含編輯器和CKEditor 5 change:data事件對象的對象觸發。

```change html
<ckeditor [editor]="Editor" (change)="onChange($event)"></ckeditor>
```

```ChangeEvent
import * as ClassicEditor from '@ckeditor/ckeditor5-build-classic';
import { ChangeEvent } from '@ckeditor/ckeditor5-angular/ckeditor.component';

@Component( {
    // ...
} )
export class MyComponent {
    public Editor = ClassicEditor;

    public onChange( { editor }: ChangeEvent ) {
        const data = editor.getData();

        console.log( data );
    }
    ...
}
```

#### blur

當編輯器的編輯視圖模糊時觸發。它與[editor.editing.view.document#blur](https://ckeditor.com/docs/ckeditor5/latest/api/module_engine_view_document-Document.html#event-event:focus)事件相對應。
它使用包含編輯器和CKEditor 5 blur事件數據的對象觸發。

#### focus

聚焦編輯器的編輯視圖時觸發。它與[editor.editing.view.document#focus](https://ckeditor.com/docs/ckeditor5/latest/api/module_engine_view_document-Document.html#event-event:focus)事件相對應。
它使用包含編輯器和CKEditor 5 focus事件數據的對象觸發。

#### error

當編輯器崩潰時觸發（在編輯器初始化期間崩潰）。編輯器崩潰後，內部看門狗機制將重新啟動編輯器並觸發ready事件。

## Chart.js and ng2-charts 套件安裝

Chart.js是一個流行的JavaScript圖表庫，ng2圖表是Angular 2 的包裝器，可以輕鬆地將Chart.js整合到Angular中。

```ng2-charts charts.js
npm install ng2-charts chart.js --save
```

[ng2-charts](https://valor-software.com/ng2-charts/#/GeneralInfo)

charts example in Angular.

ng g c bar-chart

ng g c bubble-chart

ng g c line-chart

ng g c pie-chart

ng g c radar-chart

ng g c doughnut-chart

### chartjs-plugin-datalabels 安裝

[相關參考chartjs-plugin-datalabels官方說明](https://chartjs-plugin-datalabels.netlify.app/guide/getting-started.html#installation)

```chartjs-plugin-datalabels
npm install chartjs-plugin-datalabels --save
```