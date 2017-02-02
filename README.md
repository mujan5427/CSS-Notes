## Table of Contents

[Introduction](#introduction)

  1. [What is CSS](#what-is-css)

[Style Sheets](#stylesheets)

  1. [樣式剖析]()
  2. [樣式表的存在方式]()

[Selectors](#selector)

[Style Inheritance](#style-inheritance)

[The Cascade](#the-cascade)

[Box Model](#box-model)

[Layouts](#layouts)

[Advanced CSS](#advanced-css)

[Reference Information](#reference-information)

<br />

## Introduction

<a name="what-is-html"></a>
What is CSS ?

  * **階層樣式表 (_Cascading Style Sheets_)**：簡稱 CSS，藉由它來讓以 HTML 為根基的網頁變好看

**[⬆ back to top](#table-of-contents)**

<br />
<br />

## Style Sheets

<a name=""></a>
樣式剖析

  * 一個樣式定義了頁面上一個元素的外觀，它只是一個規則用來告知瀏覽器，該如何呈現網頁上的一些東西

  * 樣式主要由兩個部分組成：

      - **選擇器 (_Selector_)**：瀏覽器要呈現的網頁元素

      - **宣告區塊 (_Declaration Block_)**：元素實際上的呈現方式，以 `{` 開始，`}` 結束

        - **宣告 (_Declaration_)**：宣告區塊中，可添加一至多個 **宣告**，以 `;` 結尾

        - **屬性 (_Property_)**：各種格式的選項

        - **值 (_Value_)**：屬性的值

    ![CSS Style Example](./assets/images/css-style-example.png)

**[⬆ back to top](#table-of-contents)**

<br />
<br />

<a name=""></a>
樣式表的存在方式

  * 樣式表有三種方式可載入於頁面：

    - 內部：屬於網頁頁面程式碼的一部分，存在 `<head>` 區塊的 `<style>` 標籤中

      ex :

      ```html
      <html>
        <head>
          <style>

          h1 {
            color: #FF7643;
            font-family: Arial;
          }

          p {
            color: red;
            font-size: 1.5em;
          }

          </style>
        </head>

        <body>

          <!-- The rest of your page follows... -->

        </body>
      </html>
      ```

    - 外部：就是一個副檔名為 `.css` 的樣式表檔案，透過 `<link>` 標籤可以載入指定的樣式表

      ex :

      ```html
      <link rel="stylesheet" href="css/styles.css">
      ```

    - 行內：即是將樣式撰寫於 HTML 標籤的 `style` 屬性之中

      ex :

      ```html
      <h1 style="color: #6A94CC;">
      ```

**[⬆ back to top](#table-of-contents)**

<br />
<br />

## Selectors

  * 透過選擇器 (_selectors_) 告知 CSS 想要選定哪個元素

  * **類型選擇器 (_Type or Element Selectors_)**：選定頁面上每一個符合該類型的標籤

    ex :

    ```css
    /* 選定該頁面的每一個 <h2> 標籤 */

    h2 {
      color: #000000;
      margin-bottom: 0;
    }
    ```

  * **類別選擇器 (_Class Selectors_)**：選定頁面上每一個標籤的 `class` 屬性中，擁有該類別者

    - 名稱必須以 `.` 開頭

    - `.` 之後必須是字元

    - 名稱只允許使用字元、數字、連字符號 和 底線

    - 名稱有區分大小寫

    - 一個標籤，可賦予多個類別

    ex :

    ```html
    <button class="btn add">Add</button>
    ```

    ```css
    /* 選定該頁面上每一個標籤的 class 屬性中，擁有 .btn 類別者 */

    .btn {
      border-radius: 5px;
    }

    .add {
      background-color: green;
    }
    ```

  * **ID 選擇器 (ID Selectors)**：選定頁面上標籤的 `id` 屬性中，擁有該 ID 者

    ex :

    ```html
    <div id="banner">
    ```

    ```css
    /* 選定頁面上標籤的 `id` 屬性中，擁有該 ID 者 */

    #banner {
      background: #CC0000;
      height: 300px;
      width: 720px;
    }
    ```

  * **群組選擇器 (_Grouping Selectors_)**：選定頁面上指定的群組標籤，可以使用任何有效的選擇器

    ex :

    ```css
    h1, h2, h3, h4, h5, h6 {
      color: #F1CD33;
    }

    /* 各種不同類型的選擇器混搭 */

    h1, p, .copyright, #banner {
      color: #F1CD33;
    }
    ```

  * **全局選擇器 (_Universal Selector_)**：選定頁面上所有的標籤，也可用於後裔選擇器

    ex :

    ```css
    * {
      padding: 0;
      margin: 0;
    }

    /* 選定 .banner 標籤之後的所有後裔標籤 */

    .banner * {
      float: left;
      color: #FFFFFF;
    }
    ```

  * **後裔選擇器 (_Descendant Selector_)**：選定頁面上指定的後裔標籤，可以使用任何有效的選擇器

    ex :

    ```css
    /* 選定 li 標籤，的後裔標籤 a */

    li a {
      font-family: Arial;
    }

    /* 選定 .intro 標籤，的後裔標籤 a */
    .intro a {
      color: yellow;
    }
    ```

  * **屬性選擇器 (_Attribute Selector_)**：選定頁面上擁有該屬性的標籤

    ex :

    ```css
    /* 選取帶有 title 屬性的 <img> 標籤 */

    img[title] {
      color: red;
    }

    /* 選取 href 屬性為 "http://www.cafesoylentgreen.com" 的 <a> 標籤 */

    a[href="http://www.cafesoylentgreen.com"] {
      color: green;
      font-weight: bold;
    }

    /* 選取 type 屬性為 "text" 的 <input> 標籤 */

    input[type="text"] {
      color: black;
    }

    /* 選取 href 屬性開頭為 "https://" 的 <a> 標籤 */

    a[href^="https://"] {
      font-size: 16px;
    }

    /* 選取 href 屬性開頭為 ".pdf" 的 <a> 標籤 */

    a[href$=".pdf"] {
      font-weight: 400;
    }

    /* 選取 src 屬性包含 "headshot" 字元的 <img> 標籤 */

    img[src*="headshot"] {
      margin-left: 10px;
    }
    ```

  * **子選擇器 (_Child Selectors_)**：選取指定的子元素標籤，使用 `>` 表示其關係

    ex :

    ```css
    /* 選取 <body> 標籤中所有為子元素的 <h1> 標籤 */

    body > h1 {
      color: #CCCCCC;
    }
    ```

  * **鄰近兄弟選擇器 (_Adjacent Siblings Selectors_)**：選取指定兄弟元素標籤，使用 `+` 表示其關係

    ex :

    ```css
    /* 選取兄弟元素為 <h2> 的 <p> 標籤 */

    h2 + p {
      margin: 0 10px 10px 0;
    }
    ```

  * **通用兄弟選擇器 (_General Sibling Selectors_)**：選取相同層級的所有兄弟元素標籤，使用 `~` 表示其關係

    ex :

    ```css
    /* 選取所有是 <h2> 的兄弟標籤的 <p> 標籤 */

    h2 ~ p {
      margin: 0 10px 10px 0;
    }
    ```

  * **擬類別 (_Pseudo-Classes_)**：能根據和使用者的互動狀態，來套用不同樣式

    ex :

    ```css
    /* 在使用者游標移過 <a> 標籤時，套用樣式 */

    a:hover {
      color: yellow;
      font-weight: 400;
    }
    ```

  * **擬元素 (_Pseudo-Elements_)**：能根據特定的規則，來套用不同樣式

    > 擬元素前綴使用 `::`，擬類別則使用 `:`

    ex :

    ```css
    /* 選取 <p> 標籤的第一個字元，套用樣式 */

    p::first-letter {
      color: #ff0000;
      font-size: xx-large;
    }
    ```

    > 更多可供使用的擬類別 及 擬元素，請參考 [MDN CSS Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference#Selectors)

**[⬆ back to top](#table-of-contents)**

<br />
<br />

## Style Inheritance

  * 祖先元素擁有的屬性，傳遞到後裔元素身上，就稱為繼承 (_Inheritance_)

  * CSS 中不是所有的屬性，都擁有繼承的特性

  > 可在 [MDN Keyword Index](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference#Keyword_index) 中查詢，屬性可繼承

**[⬆ back to top](#table-of-contents)**

<br />
<br />

## The Cascade

  * 管控屬性間互相作用以及衝突時處理的優先權，稱為疊層 (_Cascade_)

  * 累加繼承樣式：繼承一群祖先元素的樣式，而產生的新樣式

    ex :

    ```html
    <body>
      <p>Hi everyone, I'm <strong>Justin</strong></p>
    </body>
    ```

    ```css  
    body {
      font-family: Verdana, Arial;
    }
    p {
      color: #F30000;
    }
    strong {
      font-size: 24px;
    }

    /* <strong> 繼承祖先元素的屬性 font-family、color */

    strong {
      font-family: Verdana, Arial;
      color: #F30000;
      font-size: 24px;
    }
    ```

  * 最鄰近祖先勝出：同一個屬性被多個祖先重複套用

    ex :

    ```html
    <!-- <strong> 標籤的文字內容顏色會是綠色 -->

    <body>
      <p>Hi everyone, I'm <strong>Justin</strong></p>
    </body>
    ```

    ```css
    body {
      color: red;
    }
    p {
      color: green;
    }
    ```

  * 直接套用者勝出：直接套用在標籤上的屬性，會覆蓋掉其他來自祖先元素的相同屬性

    ex :

    ```html
    <!-- <strong> 標籤的文字內容顏色會是藍色 -->

    <body>
      <p>Hi everyone, I'm <strong>Justin</strong></p>
    </body>
    ```

    ```css
    body {
      color: red;
    }
    p {
      color: green;
    }
    strong {
      color: blue;
    }
    ```

  * 優先度最高者勝出：單一標籤，同時被多重樣式套用，瀏覽器將計算出樣式的優先度後，才進行套用

    ex :

    ```html
    <!-- <p> 標籤的文字內容，將會套用藍色 -->

    <body>
      <p id="name" class="intro">Hi everyone, I'm Justin</p>
    </body>
    ```

    ```css

    /* 標籤選擇器 => 1 分 */

    p {
      color: red;
    }

    /* 類別選擇器 => 10 分 */

    .intro {
      color: green;
    }

    /* ID 選擇器 => 100 分 */

    #name {
      color: blue;
    }
    ```

  * 優先度計算

      - 標籤選擇器：1 分

      - 擬元素：1 分

      - 類別選擇器：10 分

      - 屬性選擇器：10 分

      - 擬類別：10 分

      - ID 選擇器：100 分

      - 行內樣式：1000 分

      - 後裔選擇器：將上述各種類型的選擇器分數加總後，就是它的分數

    ![selector's specificity](./assets/images/selector's-specificity.png)

  * 位置順序最後的勝出：不同樣式選定相同元素，且優先度相同的情況，位置在最後面的樣式會被採用

    ex :

    ```html
    <!-- <a> 標籤的文字內容將會套用 .byline a 樣式 -->

    <p class="byline">Written by <a class="email" href="mailto:jean@cosmofarmer.com">Jean Graine de Pomme</a></p>
    ```

    ```css
    p .email {
      color: blue;
    }

    .byline a {
      color: red;  
    }
    ```

  * 推翻優先度：使用 `!important` 可以強制指定屬性的優先度為最高

    ex :

    ```html
    <!-- <a> 標籤的文字內容將會套用 p .email 樣式 -->

    <p class="byline">Written by <a class="email" href="mailto:jean@cosmofarmer.com">Jean Graine de Pomme</a></p>
    ```

    ```css
    /* 下列兩個樣式優先度計算後都是 11 分，但是擁有 `!important` 的屬性優先度會是最高，因此它會被採用 */

    p .email {
      color: blue !important;
    }

    .byline a {
      color: red;  
    }
    ```

**[⬆ back to top](#table-of-contents)**

<br />
<br />

## Box Model

  * **區塊模型 (_Box Model_)**：包含了標籤的內容、內距、邊線、外距

    ![Box Model Example](./assets/images/box-model.png)

  * 外距會在元素周圍增加空白區域，讓各元素之間保持距離

  * 外距、內距屬性值的單位，如果是 `%` 瀏覽器則會根據外層元素的寬度來計算間距寬度

    > 外層元素即為包覆在指定元素向外一層的元素，在沒有設定寬度的外層元素中則會根據瀏覽器視窗大小改變

  * 外距、內距簡寫寫法如下：

    ex :

    ```css
    /* 四邊都不同：上、右、下、左 */

    .box {
      padding: 0 10px 10px 20px;
    }

    /* 上下邊和左右邊：上和下、左和右 */

    .box {
      padding: 10px 20px;
    }

    /* 左右邊相同，上下邊不同：上、左和右、下 */

    .box {
      padding: 5px 20px 8px;
    }

    /* 四邊都相同 */

    .box {
      padding: 10px;
      margin: 0;
    }
    ```

    > 屬性值為 0，單位可以不寫

  * 外距、內距屬性值可以是負數

    ex :

    ```css
    .box {
      padding: -10px;
      margin: -5%;
    }
    ```

  * 行內元素 (_Inline Elements_) 只有左右內、外距，不能使用上下內、外距

  * 行內元素可以使用 `display` 屬性，改變成區塊等級元素、行內區塊...等等

  * 邊線簡寫寫法如下：

    ```css
    /* border 屬性值的順序不會影響結果 */

    .box {
      border: 4px solid rgb(255, 0, 0);
    }

    .box {
      border: solid rgb(255, 0, 0) 4px;
    }

    /* 為個別邊線套用樣式 */

    .box {
      border: 2px solid red;
      border-bottom: 4px dashed #333333;
    }

    /* 可以使用 none 屬性值，取消邊線 */

    .box {
      border: 2px solid red;
      border-bottom: none;
    }
    ```

  * 內容區塊 (_Content Area_) 的寬、高，可以透過 width 和 height 屬性設定

    ex :

    ```css
    .box {
      width: 50px;
      height: 80px;
    }
    ```

  * 預設的區塊模型實際的寬度計算為，外距、邊線、內距和內容區塊寬度的總和

    ex :

    ```css
    /* 寬度總和為 160px */

    .box {
      width: 100px;
      padding: 15px;
      border-width: 5px;
      margin: 10px;
    }
    ```

  * 改變瀏覽器計算元素寬度的方式，可以使用 `box-sizing` 屬性，屬性值如下：

    - content-box：瀏覽器預設的模式

    - padding-box：瀏覽器會將內距的寬度納入到內容區塊

      ex :

      ```css
      /* 元素寬度總和為 100px，其中內容區塊為：60px (100px-20px-20px) */

      .box {
        box-sizing: padding-box;
        width: 100px;
        padding: 0 20px;
      }
      ```

    - border-box：瀏覽器會將內距、邊線的寬度納入到內容區塊

      ex :

      ```css
      /* 元素寬度總和為 100px，其中內容區塊為：50px (100px-20px-20px-5px-5px) */

      .box {
        box-sizing: padding-box;
        width: 100px;
        padding: 0 20px;
        border: 5px solid blue;
      }
      ```

  * 內容區塊大於樣式所設定的寬高時，內容區塊中的內容會溢出 box 區域，可使用 `overflow` 屬性控制

    - visible：瀏覽器的預設設定，內容會溢出 box 區域

    - scroll：增加捲軸在元素中，使內容不會溢出 (捲軸永遠顯示)

    - auto：同 scroll，但捲軸只在需要時顯示

    - hidden：隱藏所有溢出 box 的內容

  * 設定元素的寬、高最大值和最小值

    - max-width

    - min-width

    - max-height

    - min-height


**[⬆ back to top](#table-of-contents)**

<br />
<br />

## Reference Information

CSS：The Missing Manual, 4E Traditional Chinese (Author：David Sawyer McFarland)

<br />
