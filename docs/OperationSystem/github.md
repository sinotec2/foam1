---
layout: default
title: GitHub
parent:   Operation System
grand_parent: Utilities
tags: GitHub git
---

{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC 
{:toc}

---
此處介紹常用的unix指令、串連之內容別名、以簡化查詢過程。

# Github

## [GitHub][gh]簡介

- 雖然[GitHub][gh]平台大量提供了有關程式碼的支援，包括版本管理、協作系統、論壇、以及程式說明的發布網站([github pages][ghpg])等等，但也有不少人運用在一般性網誌的發布、程式教學的互動平台。
- 因為是社群媒體網站，發布內容還是以社群可能會有興趣的項目為主。
- 各國官方程式碼的公開平台，很多也是選擇在[GitHub][gh]發布，其中包括美國環保署、大氣研究聯盟等等。
- 除了[github pages][ghpg]之外，也開發了[Git Book][gbook]系統，免費提供讓個人使用，讓使用者可以發布整本書的內容。

### [GitHub][gh]的使用

1. 登錄會員
1. 創建新的目錄(Repository)、設定開放對象、複製網址（假設名稱為notes）
1. 貼在本地GitHub DeskTop、創建本地相對應目錄
1. 開啟[VS Code][vsc_wiki]進行檔案或目錄新增、編寫
1. 上推至[GitHub][gh]

### 公開網頁[github pages][ghpg]之創建

1. 點進前述步驟2.所建立的[GitHub][gh] notes目錄
1. 按下齒輪 Settings頁面，在左側點進Pages頁面，選擇一個分支(branch)名稱,如main
,並在root處鍵入新io網頁的名稱（如`docs`）,按下save之後，系統將會建立https://USERNAME.github.io/notes 網頁
1. 複製網頁模版到本地暫存目錄、貼到本地Repository目錄，將所有個別帳戶名稱處都修改成正確的url，再將其上推至[GitHub][gh]。
1. [GitHub][gh]將會自行將md碼編譯成html，建立相對應的網頁。
1. 如果前述notes目錄不打算公開，就不必（也不能）設定[github pages][ghpg]
1. 詳參[Just the Docs](https://github.com/just-the-docs/just-the-docs)

### [github pages][ghpg]模版之選擇

- 參考[jekyll主題版本比較評估](https://sinotec2.github.io/FAQ/2022/06/24/NotesAboutPageViews.html#jekyll主題版本比較評估)，以[JTD](https://just-the-docs.github.io/just-the-docs)與[TeXt](https://tianqi.name/jekyll-TeXt-theme/)較為合用。

### 本地git界面的選擇

- [git][git]作為是遠端與本地檔案及版本管理的程式，可以在任何unix-like界面、window命令列上執行，同時也有多個界面軟體可供選擇。如(參[DEVART, 2021, Best Git GUI Clients for Windows](https://blog.devart.com/best-git-gui-clients-for-windows.html))：
  1. [GitHub Desktop](https://desktop.github.com/)
  1. 其他[GUI Clients](https://git-scm.com/downloads/guis) tools
  1. [SmartGit](https://www.syntevo.com/smartgit/)
- 選擇[GitHub Desktop](https://desktop.github.com/)的理由
  1. [VS Code][vsc_wiki]內部的git功能會需要最新的.Net程式與設定，需要更新windown版本，這對本地作業平台的管理是項挑戰。因此[VS Code][vsc_wiki]外部簡易的git GUI有其必要。
  1. GitHub官方維護、發展、推荐
  1. 如果是單一檔案的更新，會自動代出檔案名稱作為更新批次標籤
  1. 記憶體需求量低

### [GitHub][gh]的缺點

- .md檔案可以直接在Repository中呈現，但在公開的Github Pages上呈現會需要編譯部署的時間，複雜的系統可能會花費到5 ～ 10 分鐘以上。
- 下班時間公司會關閉[GitHub][gh]部分功能、不能進行檔案更新上載。對於長時間工作的程式發展者而言是項嚴重的限制。

[gh]: <https://zh.wikipedia.org/zh-tw/GitHub> "GitHub是一個線上軟體原始碼代管服務平台，使用Git作為版本控制軟體，由開發者Chris Wanstrath、P. J. Hyett和湯姆·普雷斯頓·沃納使用Ruby on Rails編寫而成。在2018年，GitHub被微軟公司收購。GitHub同時提供付費帳戶和免費帳戶。這兩種帳戶都可以建立公開或私有的代碼倉庫，但付費使用者擁有更多功能。根據在2009年的Git使用者調查，GitHub是最流行的Git存取站點。[5]除了允許個人和組織建立和存取保管中的代碼以外，它也提供了一些方便社會化共同軟體開發的功能，即一般人口中的社群功能，包括允許使用者追蹤其他使用者、組織、軟體庫的動態，對軟體代碼的改動和bug提出評論等。GitHub也提供了圖表功能，用於概觀顯示開發者們怎樣在代碼庫上工作以及軟體的開發活躍程度。 "
[git]: <https://backlog.com/git-tutorial/tw/intro/intro1_1.html> "git是一個分散式版本控制軟體，最初由林納斯·托瓦茲創作，於2005年以GPL授權條款釋出。最初目的是為了更好地管理Linux核心開發而設計。應注意的是，這與GNU Interactive Tools不同。 git最初的開發動力來自於BitKeeper和Monotone。"
[ghpg]: <https://zh.wikipedia.org/zh-tw/GitHub_Pages> "GitHub Pages是GitHub提供的一個網頁代管服務，於2008年推出[1][2]。可以用於存放靜態網頁，包括部落格、項目文檔[3][1]甚至整本書。[4]Jekyll軟體可以用於將文檔轉換成靜態網頁，該軟體提供了將網頁上傳到GitHub Pages的功能。[5]一般GitHub Pages的網站使用github.io的子域名，但是用戶也可以使用第三方域名。[6] "
[vsc_wiki]: <https://zh.wikipedia.org/wiki/Visual_Studio_Code> "Visual Studio Code（簡稱 VS Code）是一款由微軟開發且跨平台的免費原始碼編輯器[6]。該軟體支援語法突顯、程式碼自動補全（又稱 IntelliSense）、程式碼重構功能，並且內建了命令列工具和 Git 版本控制系統[7]。使用者可以更改佈景主題和鍵盤捷徑實現個人化設定，也可以透過內建的擴充元件程式商店安裝擴充元件以加強軟體功能。"