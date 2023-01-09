---
title: Wiki.js
tags: note_system Code
layout: article
aside:
  toc: true
sidebar:
  nav: layouts
date: 2023-01-04
modify_date: 2023-01-04 10:36:19
---

## 背景

- Wiki.js是在Node.js上運行並用JavaScript編寫的Wiki引擎。它是根據Affero GNU[通用公共許可][gnu]發布的免費軟件。提供方式可以作為自託管解決方案，也可以在DigitalOcean和AWS市場上使用“單擊”安裝。([wiki][wikijs_wiki])
- 根據wikipedia[^1]上的數據，Wiki.js誕生於28 January 2017，是wiki家族最年輕的系統(相對最年長的系統[WikiWikiWeb][WikiWikiWeb]是1995誕生)，雖然如此，也是最為活耀的系統，目前已經更新到2.5版。
- Wiki.js的特色自然是其執行node.js的網站架構，目前還有[Nuclino][Nuclino]、[TiddlyWiki][TiddlyWiki]等其他的系統也是使用javascript的網頁程式，前者是個公司經營的協作系統、後者適合個人筆記系統，沒有資料庫系統程式支援搜尋引擎(可以使用[[elasticsearch]]引擎)。

- [Wiki.js官網][wikijs_official]
- [wiki.js 使用 postgres 支持中文全文检索](https://zhuanlan.zhihu.com/p/335359081)

## TiddlyWiki

### system installation

- 安裝與啟動，詳參[ Jermolene /TiddlyWiki5][Jermo]
- 中文之設定，詳參[bramchen][bramchen]：修改 `./MyWiki/tiddlywiki.info` ，加入

```bash
Open a command line terminal and type:

    npm install -g tiddlywiki
    If it fails with an error you may need to re-run the command as an administrator:
    sudo npm install -g tiddlywiki (Mac/Linux)

Ensure TiddlyWiki is installed by typing:

    tiddlywiki --version

    In response, you should see TiddlyWiki report its current version (eg "5.2.5". You may also see other debugging information reported.)

Try it out:

    tiddlywiki mynewwiki --init server to create a folder for a new wiki that includes server-related components
    tiddlywiki mynewwiki --listen to start TiddlyWiki
    Visit http://127.0.0.1:8080/ in your browser
```

### language

- 注意如果後面還有設定，在"`]`"後要加上"`,`"

```java
    "languages": [
        "zh-Hant"
    ]
```
`tiddlywiki mynewwiki --listen host=125.229.149.182 port=8080`

https://www.getit01.com/p20180112331214433/

---
[^1]: Comparison of wiki software, [wikipedia][cmp](2022)

[Jermo]: <https://github.com/Jermolene/TiddlyWiki5> "Installing TiddlyWiki on Node.js"
[bramchen]: <http://bramchen.objectis.net/> "bramchen"
[TiddlyWiki]: <https://en.wikipedia.org/wiki/TiddlyWiki> "TiddlyWiki is a personal wiki and a non-linear notebook for organising and sharing complex information. It is an open-source single page application wiki in the form of a single HTML file that includes CSS, JavaScript, embedded files such as images, and the text content. It is designed to be easy to customize and re-shape depending on application. It facilitates re-use of content by dividing it into small pieces called Tiddlers."
[Nuclino]: <https://en.wikipedia.org/wiki/Nuclino> "Nuclino is a cloud-based team collaboration software which allows teams to collaborate and share information in real time.[2][3] It was founded in Munich, Germany in 2015.[4] Some notable features include a WYSIWYG collaborative real-time editor and a visual representation of a team's knowledge in a graph. In addition to its web-based and desktop application, in 2018, Nuclino launched a free mobile app for Android and iOS."
[WikiWikiWeb]: <https://zh.wikipedia.org/wiki/WikiWikiWeb> "WikiWikiWeb是第一個用戶可編輯的維基網站，於1995年3月25日由其發明者程序員沃德·坎寧安與Portland Pattern Repository網站一起討論軟件設計模式後推出。WikiWikiWeb這個名字最初也是於運行這個網站的維基軟件名稱。這個維基軟件用Perl編程語言編寫，後更名為“WikiBase”。WikiWikiWeb是由坎寧安在1994年開發的，目的是方便程序員之間的思想交流。這個概念是基於坎寧安在20世紀80年代後期編寫HyperCard堆程式時想到的"
[gnu]: <https://en.wikipedia.org/wiki/GNU_Affero_General_Public_License> "GNU Affero General Public License"
[cmp]: <https://en.wikipedia.org/wiki/Comparison_of_wiki_software> "Comparison of wiki software"
[wikijs_official]: <https://js.wiki/> "The most powerful and extensible open source Wiki software, Make documentation a joy to write using Wiki.js's beautiful and intuitive interface!"
[wikijs_wiki]: <https://en.wikipedia.org/wiki/Wiki.js> "Wiki.js是在Node.js上運行並用JavaScript編寫的Wiki引擎。它是根據Affero GNU通用公共許可發布的免費軟件。它可以作為自託管解決方案提供，也可以在DigitalOcean和AWS市場上使用“單擊”安裝提供。"

