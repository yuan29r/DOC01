# Markdown 基本概念

## 標題

```title
# This is heading 1
## This is heading 2
### This is heading 3
#### This is heading 4
```

開頭使用 1-6 個井字號 (#) 來指出標題，對應到 H1 到 H6 的 HTML標題層級。  
在您的主題中，必須**只能有一個第一級標題 (H1)**，顯示為其頁面上的標題。  
如果您的標題以 # 字元作為結尾，則需要在結尾新增額外的 # 字元，以便正確呈現標題。  
例如，# Async Programming in F# #。  
第二級標題將產生頁面上的 TOC，顯示在頁面標題下方的「本文中」區段中。

## 粗體與斜體文字

```粗體
**bold**
```

粗體要2個*：**bold**

```斜體
*italic*
```

斜體用1個*：*italic*  

```粗體加斜體
***bold and italic***
```

粗體加上斜體要用三個*：***bold and italic***  

## 區塊引述

```區塊引述
>我是文字敘述
```  

前面會多一個>，顯示結果如下的效果
> The drought had lasted now for ten million years, and the reign of the terrible lizards had long since ended. Here on the Equator, in the continent which would one day be known as Africa, the battle for existence had reached a new climax of ferocity, and the victor was not yet in sight. In this barren and desiccated land, only the small or the swift or the fierce could flourish, or even hope to survive.  

## 清單

未排序清單

```未排序清單
- List item 1
- List item 2
- List item 3
```  

結果如下：  

- List item 1
- List item 2
- List item 3

若要建立包含在另一個清單中的巢狀清單，**請將子清單項目縮排**。

```巢狀清單
- List item 1
  - List item A
  - List item B
- List item 2
```

結果如下：

- List item 1
  - List item A
  - List item B
- List item 2

已排序清單

若要設定已排序/逐步清單的格式，請使用對應的數字。

```排序清單
1. First instruction
1. Second instruction
1. Third instruction
```  

結果如下：

1. First instruction
1. Second instruction
1. Third instruction

若要建立包含在另一個清單中的巢狀清單，**請將子清單項目縮排**。

```巢狀清單
1. First instruction
   1. Sub-instruction
   1. Sub-instruction
1. Second instruction
```

結果如下：

1. First instruction
   1. Sub-instruction
   1. Sub-instruction
1. Second instruction

## 表格

(|) 表示垂直線  
(-) 建立每一欄的標頭，要顯示多寬也是用這個增減  
(:) 擺放位置表示靠左、靠右、置中(左右各一組冒號)  

```表格
| Fun                  | With                 | Tables          |
| :------------------- | -------------------: |:---------------:|
| left-aligned column  | right-aligned column | centered column |
| $100                 | $100                 | $100            |
| $10                  | $10                  | $10             |
| $1                   | $1                   | $1              |
```

結果如下：

| Fun                  | With                 | Tables          |
| :------------------- | -------------------: |:---------------:|
| left-aligned column  | right-aligned column | centered column |
| $100                 | $100                 | $100            |
| $10                  | $10                  | $10             |
| $1                   | $1                   | $1              |

## 連結

內嵌連結的 Markdown 語法是由超連結文字 [link text] 部分，以及緊接在後面的連結 URL 或檔案名稱 (file-name.md) 部分所組成：

```連結結構表示
[Google](https://www.google.com.tw)
```

結果如下：

[Google](https://www.google.com.tw)

## 程式碼片段

前三個倒引號 ('`') 字元之後的別名定義要使用的語法醒目提示。

```程式碼片段
```名稱
你的code填寫區
```結束也要三個反單
```

區塊裡再塞區塊好像無法正常包覆進去,所以暫時先這樣子寫了，示意而已  
把你的程式碼放在三個反單間就可以形成一個區塊，如下；

```demo
我是程式碼展示區
```

## 參考連結  

[微軟教學-如何使用 Markdown 來撰寫 Docs](https://docs.microsoft.com/zh-tw/contribute/how-to-write-use-markdown)

[適用於 VS Code 的 Docs 編寫套件](https://docs.microsoft.com/zh-tw/contribute/how-to-write-docs-auth-pack)