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

## Reference Information

CSS：The Missing Manual, 4E Traditional Chinese (Author：David Sawyer McFarland)

<br />
