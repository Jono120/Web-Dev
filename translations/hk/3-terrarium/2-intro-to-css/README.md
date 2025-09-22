<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "acb5ae00cde004304296bb97da8ff4c3",
  "translation_date": "2025-08-29T15:07:13+00:00",
  "source_file": "3-terrarium/2-intro-to-css/README.md",
  "language_code": "hk"
}
-->
# 玻璃缸項目第 2 部分：CSS 簡介

![CSS 簡介](../../../../translated_images/webdev101-css.3f7af5991bf53a200d79e7257e5e450408d8ea97f5b531d31b2e3976317338ee.hk.png)  
> 手繪筆記由 [Tomomi Imura](https://twitter.com/girlie_mac) 提供

## 課前測驗

[課前測驗](https://ff-quizzes.netlify.app/web/quiz/17)

### 簡介

CSS，全名為層疊樣式表（Cascading Style Sheets），解決了網頁開發中的一個重要問題：如何讓你的網站看起來更美觀。為應用程式添加樣式不僅能提升其可用性，還能讓其外觀更吸引人；此外，你還可以使用 CSS 創建響應式網頁設計（Responsive Web Design，RWD），讓你的應用程式無論在什麼螢幕尺寸下都能保持良好的顯示效果。CSS 不僅僅是讓應用程式看起來更美觀，它的規範還包括動畫和變形功能，能為你的應用程式實現更複雜的互動效果。CSS 工作組負責維護當前的 CSS 規範，你可以在 [World Wide Web Consortium 的網站](https://www.w3.org/Style/CSS/members)上關注他們的工作。

> 注意，CSS 是一種不斷演進的語言，就像網頁上的其他技術一樣，並非所有瀏覽器都支持最新的規範部分。請隨時參考 [CanIUse.com](https://caniuse.com) 來檢查你的實現。

在本課中，我們將為線上玻璃缸添加樣式，並學習多個 CSS 概念：層疊、繼承、選擇器的使用、定位以及使用 CSS 構建佈局。在此過程中，我們將設計玻璃缸的佈局，並創建實際的玻璃缸。

### 前置條件

你應該已經完成了玻璃缸的 HTML 結構，並準備好進行樣式設計。

> 查看影片

> 
> [![Git 和 GitHub 基礎影片](https://img.youtube.com/vi/6yIdOIV9p1I/0.jpg)](https://www.youtube.com/watch?v=6yIdOIV9p1I)

### 任務

在你的玻璃缸資料夾中，創建一個名為 `style.css` 的新檔案。在 `<head>` 區域中匯入該檔案：

```html
<link rel="stylesheet" href="./style.css" />
```

---

## 層疊

層疊樣式表的核心概念是樣式的“層疊”，即樣式的應用是由其優先級決定的。由網站作者設置的樣式優先於瀏覽器設置的樣式。內聯樣式的優先級高於外部樣式表中的樣式。

### 任務

為你的 `<h1>` 標籤添加內聯樣式 "color: red"：

```HTML
<h1 style="color: red">My Terrarium</h1>
```

然後，將以下代碼添加到你的 `style.css` 檔案中：

```CSS
h1 {
 color: blue;
}
```

✅ 你的網頁應用程式中顯示了哪種顏色？為什麼？你能找到覆蓋樣式的方法嗎？什麼情況下你會想這樣做，或者不這樣做？

---

## 繼承

樣式可以從祖先元素繼承到後代元素，嵌套的元素會繼承其父元素的樣式。

### 任務

將 body 的字體設置為指定字體，並檢查嵌套元素的字體：

```CSS
body {
	font-family: helvetica, arial, sans-serif;
}
```

打開瀏覽器的控制台，進入“元素”標籤，觀察 H1 的字體。它繼承了 body 的字體，這在瀏覽器中有所說明：

![繼承的字體](../../../../translated_images/1.cc07a5cbe114ad1d4728c35134584ac1b87db688eff83cf75985cf31fe0ed95c.hk.png)

✅ 你能讓嵌套樣式繼承不同的屬性嗎？

---

## CSS 選擇器

### 標籤

到目前為止，你的 `style.css` 檔案中只為少數標籤設置了樣式，應用程式看起來有些奇怪：

```CSS
body {
	font-family: helvetica, arial, sans-serif;
}

h1 {
	color: #3a241d;
	text-align: center;
}
```

這種為標籤設置樣式的方法可以控制單一元素，但你需要控制玻璃缸中多個植物的樣式。為此，你需要利用 CSS 選擇器。

### ID

為左側和右側容器添加一些樣式。由於標記中只有一個左側容器和一個右側容器，因此它們被賦予了 ID。使用 `#` 來設置樣式：

```CSS
#left-container {
	background-color: #eee;
	width: 15%;
	left: 0px;
	top: 0px;
	position: absolute;
	height: 100%;
	padding: 10px;
}

#right-container {
	background-color: #eee;
	width: 15%;
	right: 0px;
	top: 0px;
	position: absolute;
	height: 100%;
	padding: 10px;
}
```

在這裡，你使用絕對定位將這些容器放置在螢幕的最左側和最右側，並使用百分比設置其寬度，以便它們可以適應小型行動裝置螢幕。

✅ 這段代碼有些重複，因此不符合“DRY”（Don't Repeat Yourself，不要重複自己）的原則；你能找到更好的方法來設置這些 ID 的樣式嗎？也許可以結合 ID 和類？你需要更改標記並重構 CSS：

```html
<div id="left-container" class="container"></div>
```

### 類別

在上面的例子中，你為螢幕上的兩個唯一元素設置了樣式。如果你希望樣式應用於螢幕上的多個元素，可以使用 CSS 類別。為左側和右側容器中的植物設置樣式。

注意，HTML 標記中的每個植物都有 ID 和類別的組合。這裡的 ID 是供稍後添加的 JavaScript 使用，用於操作玻璃缸植物的位置。而類別則為所有植物提供了統一的樣式。

```html
<div class="plant-holder">
	<img class="plant" alt="plant" id="plant1" src="./images/plant1.png" />
</div>
```

將以下代碼添加到你的 `style.css` 檔案中：

```CSS
.plant-holder {
	position: relative;
	height: 13%;
	left: -10px;
}

.plant {
	position: absolute;
	max-width: 150%;
	max-height: 150%;
	z-index: 2;
}
```

在這段代碼中，值得注意的是相對定位和絕對定位的混合使用，我們會在下一節中詳細介紹。請注意高度是如何以百分比處理的：

你將植物容器的高度設置為 13%，這是一個不錯的數值，確保所有植物都能顯示在每個垂直容器中，而不需要滾動。

你將植物容器向左移動，使植物在容器內更居中。由於圖片有大量透明背景，為了讓它們更容易拖動，需要向左移動以更好地適應螢幕。

然後，植物本身的最大寬度設置為 150%。這樣可以讓它隨著瀏覽器縮小而縮小。嘗試調整瀏覽器大小，植物會保持在容器內，但會縮小以適應。

還值得注意的是 z-index 的使用，它控制元素的相對高度（使植物位於容器之上，看起來像是放在玻璃缸內）。

✅ 為什麼需要同時使用植物容器和植物的 CSS 選擇器？

## CSS 定位

混合使用定位屬性（包括 static、relative、fixed、absolute 和 sticky 定位）可能有些棘手，但如果使用得當，可以很好地控制頁面上的元素。

絕對定位的元素是相對於其最近的已定位祖先進行定位的，如果沒有已定位的祖先，則相對於文檔的 body 進行定位。

相對定位的元素是根據 CSS 指定的方向，從其初始位置進行調整。

在我們的範例中，`plant-holder` 是一個相對定位的元素，位於一個絕對定位的容器內。這種行為的結果是，側邊欄容器被固定在左右兩側，而植物容器則嵌套在側邊欄內，調整自身位置以在側邊欄內垂直排列植物。

> 植物本身也使用了絕對定位，這是為了讓它可以被拖動，你會在下一課中了解更多。

✅ 嘗試切換側邊容器和植物容器的定位類型。會發生什麼？

## CSS 佈局

現在，你將使用所學知識，完全通過 CSS 構建玻璃缸本身！

首先，使用 CSS 將 `.terrarium` div 的子元素設置為圓角矩形：

```CSS
.jar-walls {
	height: 80%;
	width: 60%;
	background: #d1e1df;
	border-radius: 1rem;
	position: absolute;
	bottom: 0.5%;
	left: 20%;
	opacity: 0.5;
	z-index: 1;
}

.jar-top {
	width: 50%;
	height: 5%;
	background: #d1e1df;
	position: absolute;
	bottom: 80.5%;
	left: 25%;
	opacity: 0.7;
	z-index: 1;
}

.jar-bottom {
	width: 50%;
	height: 1%;
	background: #d1e1df;
	position: absolute;
	bottom: 0%;
	left: 25%;
	opacity: 0.7;
}

.dirt {
	width: 60%;
	height: 5%;
	background: #3a241d;
	position: absolute;
	border-radius: 0 0 1rem 1rem;
	bottom: 1%;
	left: 20%;
	opacity: 0.7;
	z-index: -1;
}
```

注意這裡使用了百分比。如果縮小瀏覽器，你可以看到玻璃缸也會縮放。還要注意玻璃缸元素的寬度和高度百分比，以及每個元素如何絕對定位在中心，並固定在視窗底部。

我們還使用了 `rem` 作為圓角半徑的單位，這是一種相對於字體大小的長度。可以在 [CSS 規範](https://www.w3.org/TR/css-values-3/#font-relative-lengths) 中了解更多關於這種相對測量的方法。

✅ 嘗試更改玻璃缸的顏色和透明度與泥土的顏色和透明度。會發生什麼？為什麼？

---

## 🚀挑戰

為玻璃缸的左下角添加一個“氣泡”光澤，使其看起來更像玻璃。你將為 `.jar-glossy-long` 和 `.jar-glossy-short` 添加樣式，使其看起來像反射的光澤。效果如下：

![完成的玻璃缸](../../../../translated_images/terrarium-final.2f07047ffc597d0a06b06cab28a77801a10dd12fdb6c7fc630e9c40665491c53.hk.png)

要完成課後測驗，請參考此學習模組：[使用 CSS 為 HTML 應用程式設計樣式](https://docs.microsoft.com/learn/modules/build-simple-website/4-css-basics/?WT.mc_id=academic-77807-sagibbon)

## 課後測驗

[課後測驗](https://ff-quizzes.netlify.app/web/quiz/18)

## 回顧與自學

CSS 看似簡單，但要為所有瀏覽器和螢幕尺寸完美設計應用程式樣式，仍然面臨許多挑戰。CSS-Grid 和 Flexbox 是為了讓這項工作更結構化、更可靠而開發的工具。通過玩 [Flexbox Froggy](https://flexboxfroggy.com/) 和 [Grid Garden](https://codepip.com/games/grid-garden/) 來學習這些工具。

## 作業

[CSS 重構](assignment.md)

---

**免責聲明**：  
此文件已使用人工智能翻譯服務 [Co-op Translator](https://github.com/Azure/co-op-translator) 翻譯。我們致力於提供準確的翻譯，但請注意，自動翻譯可能包含錯誤或不準確之處。應以原始語言的文件作為權威來源。對於關鍵資訊，建議尋求專業人工翻譯。我們對因使用此翻譯而引起的任何誤解或錯誤解讀概不負責。