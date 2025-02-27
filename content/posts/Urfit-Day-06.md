---
title: "Urfit Day 06"
date: "2025-02-24"
author: Joanna Lei
# avatar: /img/author.jpg
# authorlink: https://author.site
cover: /img/D6-Job.png
# images:
#   - /img/cover.jpg
categories:
  - My Coding Life
tags:
  - Job
# nolastmod: true
draft: false
---

### Day-6 三元運算燒腦中
  
<!--more-->
  
## 今日進度

### 拿到的票  
- **推PR**：看新進職員手冊裡，關於Git的規範。把做好的票push上去之後發PR。
- **優化程式碼**：針對同事的回覆，優化程式碼（三元運算式重複的邏輯＆重複物件做簡化）

  原本設定：
  ```tsx
    const actions = [
      {
        condition: hasTabSetting ? tabsContents.includes('program') : withProgram,
        link: `/creators/${id}?tabkey=programs`,
        label: formatMessage(commonMessages.content.addCourse),
      },
      {
        condition:
          enabledModules.podcast && (hasTabSetting ? tabsContents.includes('podcast') : withPodcast),
        link: `/creators/${id}?tabkey=podcasts`,
        label: formatMessage(commonMessages.content.podcasts),
      },
      <!-- 下列多筆略 -->
    ]
    ```
  優化程式碼：
  1.將重複的值拉出來，在設定一個公版用.map將值帶入 
  ```tsx
   const actionContents = [
    {key:'program', withKey: withProgram, tabkey: "programs", contentKey: commonMessages.content.addCourse},
    {key:'podcast', moduleEnabled: enabledModules.podcast, tabkey: "podcasts", withKey: withPodcast, contentKey: commonMessages.content.podcasts},
     <!-- 下列多筆略 -->
  ]
  const actions = actionContents.map(({ key, moduleEnabled = true, withKey, tabkey, contentKey }
    )  => ({
    condition: moduleEnabled && (hasTabSetting ? tabsContents.includes(key) : withKey),
    link: `/creators/${id}?tabkey=${tabkey}`,
    label: formatMessage(contentKey),
  }))
  ```

  2.再將重複判斷拉出來。用到`??`空值運算  
  ```tsx
  const tabsContents = settings['creator.content.tab']?.split(',') || []
  const hasTabSetting = Boolean(settings['creator.content.tab'])
  

  const actionContents:{
    key: Module;
    withKey: boolean | undefined;
    tabkey: string;
    contentKey: {
      id: string;
      defaultMessage: string;
    };
  }[] = [
    {key:'program', withKey: withProgram, tabkey: "programs", contentKey: commonMessages.content.addCourse},
    {key:'podcast', tabkey: "podcasts", withKey: withPodcast, contentKey: commonMessages.content.podcasts},
    <!-- 下列多筆略 -->
  ]
  const actions = actionContents.map(({ key, withKey, tabkey, contentKey }
    )  => ({
    condition: (enabledModules[key]) && (hasTabSetting ? tabsContents.includes(key) : withKey),
    link: `/creators/${id}?tabkey=${tabkey}`,
    label: formatMessage(contentKey),
  }))
  ```

### React:
[鐵人賽React文章：從 Hooks 開始，讓你的網頁 React 起來](https://ithelp.ithome.com.tw/articles/10216355)

- 今天沒進度


### 會議  
- 例會（約10分鍾）：簡單報告上週五進度
 

### 明天進度
- 接新的票

### 回答出來的問題
- **Q: 為什麼JSX可以直接操作?**   
  主要是在問，為什麼HTML可以放在JavaScript裡面，而且可以運作？    
  是因為這邊是JSX檔，全名是 JavaScript XML，瀏覽器並讀不懂JSX，而是需要編譯器工具，通常在 React 專案中，JSX 轉譯會自動由 Babel 或 Vite、Webpack 等工具處理。


### 待回答的問題們
- Q.1: useState & useEffect的差別是？
- Q.2: stateless？
- Q.3: 查名詞 ：Template string 模板字串``
- Q.4: 什麼是Migration/ Migrate (回答不出來要被打屁屁了＠＠)
- Q.5: nullish vs falsy

### 遇到的問題
- TypeScript 型別定義，沒有定義導致無法使用變數。

## 今日心得
在下判斷式的時候，如果沒有清楚的知道設定的條件，就沒辦法很好的定義判斷式。   
早上針對禮拜五的判斷式和另外一個主管討論了一下，因為對設定有不同的設想，所以解法就不一樣。  

今天把上週小出來的功能，優化再優化！！，所有會重複用的的Code都拔出來了，真是累（苦笑），對於物件可以怎麼設定和轉換還不熟悉，所以操作起來卡卡的，雖然有Ai輔助，但有需設定還是要自己看清楚，沒辦法100%照貼。  
試著用ChatGPT, Perplexity, Claude來解答一樣的問題，沒想到這次最佳解答是ChatGPT！！看來以後還是都讓他們試著回答好了～Perplexity沒有回答到問題，Claude給了超複雜的解答，差點沒看到暈倒（笑）。  

第一張票算是順利的通關了，嗚嗚好感動，剩一點時間再來繼續K React，還要複習JavaScript，不然基礎的觀念沒弄懂，真的很卡。（現在懺悔上課期間沒有多練習一秒鐘）