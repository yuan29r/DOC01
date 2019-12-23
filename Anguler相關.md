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
ng serve --open
```  

ng serve當您更改這些文件時，該命令將啟動服務器，監視您的文件並重建應用程序。  
該--open（或只是-o）選項會自動打開你的瀏覽器 http://localhost:4200/
