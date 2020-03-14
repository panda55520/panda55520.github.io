---
title: Hexo + GitHub Pages 建立部落格
date: 2020/01/30 15:51:50
categories:
- 宅宅工程師
tags:
- hexo
- github
- blog
- 3-hexo
- gitalk
---

## [簡報檔] <td  colspan = '4'><a href="../../../../ppt/Hexo/Hexo.html" target='_blank'>🔗另開新分頁</a></td>
<table width="100%" height="100%">
<tr width='100px'>
    <th style='font-weight:bold;color:#fff;border: 1px solid #ddd;background-color:#100f14'>快捷鍵功能</th>
    <td style='color:#fff;border: 1px solid #ddd;background-color:#bf1827'><font color=>Key F<br>
    全螢幕放映</td>
    <td>Key O<br>投影片預覽</td>
    <td>Key S<br>簡報者檢視畫面</td>
</tr>
<tr height='500px'>
    <th>簡報</th>
    <td  colspan = '3'><iframe src="../../../../ppt/Hexo/Hexo.html" width="100%" height="100%" style="border-color:#100f14;border-width:3px;border-style:solid;"></iframe></td>
</tr>
</table>

## [懶人包]

### 一、事前安裝
|軟體|內容|
|---|---|
| [GitHub](http://github.com/)|登入創建 `{yourName}.github.io` Git儲存庫(Repository)|
| [Git for windows](https://gitforwindows.org/)|下載並安裝...透過Git命令視窗執行指令|
| [Node.js](https://nodejs.org/zh-tw/download/)|下載並安裝...使用套件管理工具|

### 二、初始化
Git Clone `{yourName}.github.io`至 `{localPath}`本機目錄，打開Git命令視窗(Git Bash Here)，逐步執行指令。
```
git --version                           #檢查git安裝是否完成(可省略)
npm --version                           #檢查npm安裝是否完成(可省略)
npm install hexo-cli --global           #安裝hexo(--global參數 : 安装套件會放在/user/local)
hexo --version                          #檢查hexo安裝是否完成(可省略)
hexo init blog                          #初始化部落格到新資料夾blog
cd blog                                 #移動至部落格目錄
npm install                             #安裝package.json檔案的套件

```

### 三、部署網站
調整『部落格設定檔』，檔案路徑在 `{localPath}/blog/_config.yml`
``` Markdown
# Deployment
## Docs: http://hexo.io/docs/deployment.html
deploy:
  type: git
  repository: https://github.com/{yourName}/{yourName}.github.io.git
  branch: master

```
回到Git命令視窗，繼續執行指令
```
npm install hexo-deployer-git --save    #安裝hexo一鍵佈署功能(--save參數 : 安裝套件 + 同步更新package.json檔案)
hexo clean                              #清除cache(第一次可省略)
hexo generate                           #產生檔案到資料夾public
hexo server                             #本機預覽網頁(預設Port為4000 Ctrl+C停止預覽)
hexo deploy                             #部署網頁至GitHub

```

### 四、套用主題(進階)

主題庫推薦👍
1. [Hexo.io官網主題](https://hexo.io/themes/)
2. [知乎 : 有哪些好看的 Hexo 主题？](https://www.zhihu.com/question/24422335)

Hexo預設主題是landscape，若想套用其他的主題，修改『部落格設定檔』的主題為 `{yourTheme}`
``` Markdown
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
  theme: {yourTheme}

```

回到Git命令視窗，Git Clone `{yourTheme}` 至 `{localPath}/blog/themes/{yourTheme}` 並且重新部署網站
```
git clone {yourTheme的Git Repository URL} themes/{yourTheme}
hexo clean                             
hexo generate                          
hexo server                                                             
hexo deploy             

```

### 五、3-hexo留言板(進階)
本篇套用3-hexo主題，宣告Gitalk的檔案路徑在 `{localPath}/blog/themes/3-hexo/layout_partial/comments/gitalk.ejs`</br>
可以直接在宣告時指定參數，或者從『主題設定檔』彈性調整，路徑在 `{localPath}/blog/themes/3-hexo/_config.yml`
``` Markdown
#############评论设置#############
comment:
  on: true
  type: gitalk  # 评论系统：gitalk、disqus、gentie、gitment,注意：使用时，在下方对应位置进行配置
  comment_count: true  # 文章标题下方显示评论数
  preload_comment: false  # 预加载评论区
## false: 当点击评论条等区域时再加载评论模块
## true: 页面加载时加载评论区
# 各评论系统配置 ↓↓
gitalk:
  githubID: {yourName}
  repo: {yourName}.github.io
  ClientID: {yourClientID}
  ClientSecret: {yourClientSecret}
  adminUser: {yourName}
  distractionFreeMode: true
  language: zh-TW
  perPage: 10
# gitalk：利用github issue制作的第三方聊天插件
# https://github.com/gitalk/gitalk
# 参数介绍：
# githubID: github用户名
# repo: 使用哪个仓库的issue
# ClientID 和 ClientSecret 创建 OAuth application 就会生成：https://github.com/settings/applications/new
# adminUser: 必须为上面仓库的合作者（有写入权限），使用自己的 github 用户名即可
# distractionFreeMode: 全屏遮罩效果
# language: 语言：支持：en / zh-CN / zh-TW 三种
# perPage: 每次加载的数据大小，默认10，最大100

```

取得`{yourClientID}`和`{yourClientSecret}`必須從 https://github.com/settings/developers 登入新增OAuth Apps產生token
``` Markdown
#Application name:
  {yourName}.github.io
#Homepage URL:
  https://{yourName}.github.io/
#Application description:
  {yourName}.github.io
#Authorization callback URL:
  https://{yourName}.github.io/

```

回到Git命令視窗，安裝Gitalk並且重新部署網站
```
npm install gitalk --save    #安裝gitalk功能(--save參數 : 安裝套件 + 同步更新package.json檔案)
hexo clean                              
hexo generate                           
hexo server                             
hexo deploy                          

```

### 六、參考資料
- [姚韋辰 : Hexo+GitHub，新手也可以快速建立部落格](https://yaoandy107.github.io/hexo-tutorial/)
- [杨玉杰 : 3-hexo使用说明](https://yelog.org/2017/03/23/3-hexo-instruction/})
