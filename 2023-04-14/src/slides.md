---
layout: cover
download: 'https://antfu.me/talks/2021-04-29'
highlighter: shiki
info: |
  ## Vitepress

  Pattens and tips for using vitepress to create static blog on Github page.

  [Suxiong](https://yesux.github.io/) at **fCC Shanghai 2023-04**
---

# Sharing

如何使用 VitePress 搭建个人博客.

<div class="uppercase text-sm tracking-widest">
苏雄
</div>

<div class="abs-bl mx-14 my-12 flex">
  <img src="https://d33wubrfki0l68.cloudfront.net/774b60156d8f103170dc66f3ad10310941114653/da262/img/fcc_secondary_large.svg" class="h-8">
  <div class="ml-5 flex flex-col text-left">
    <div>Shanghai</div>
    <div class="text-sm opacity-50">Apr. 16th, 2023</div>
  </div>
</div>

---
layout: 'intro'
---

# 苏雄

<div class="leading-8 opacity-80">
有一只猫🐱<br>
一名前端程序员<br>
喜欢协作体验、玩游戏和开源建设<br>
</div>

<div class="my-10 grid grid-cols-[40px,1fr] w-min gap-y-4">
  <ri-github-line class="opacity-50"/>
  <div><a href="https://github.com/YeSuX" target="_blank">Github</a></div>
  <ri-twitter-line class="opacity-50"/>
  <div><a href="https://twitter.com/YeSuX1998" target="_blank">Twitter</a></div>
  <ri-user-3-line class="opacity-50"/>
  <div><a href="https://yesux.github.io/" target="_blank">Blog</a></div>
</div>

<img src="https://avatars.githubusercontent.com/u/44074974?v=4" class="rounded-full w-40 abs-tr mt-16 mr-12"/>

---
layout: center
---

# 为什么要搭建个人博客？


---
layout: center
---

<div class="flex content-around items-center">
  <div class="mr-10px">
    <div class="text-center text-lg">我的博客</div>
    <iframe class="rounded-lg border-solid border" src="https://yesux.github.io/"
        width="400px" height="500"/>
  </div>
  <div>
  <div class="mb-20px">- 个人博客可以促进个人成长和自我反思，增加自我认知。</div>
  <div class="mb-20px">- 个人博客可以成为个人品牌的代表，增加自己的影响力和信任度。</div>
  <div>- 个人博客可以为个人提供更多的机会和平台，展示自己的才华与能力。</div>
  </div>
</div>

---
layout: center
---

# 如何搭建

---

# 一. Github
<v-clicks>

1. 注册GitHub账号。

2. 在 GitHub 上创建一个新的仓库，并将其命名为 `<username>.github.io`，其中 `<username>` 是你的 GitHub 用户名。

3. 新建`gh-pages`分支，并指定由该分支build你的Github Pages site。
![iENjay.png](https://i.328888.xyz/2023/04/16/iENjay.png)
</v-clicks>

---

<v-clicks>

4. 给机器人自动部署的权限。
[![iENRAF.png](https://i.328888.xyz/2023/04/16/iENRAF.png)](https://imgloc.com/i/iENRAF)
![iENcrH.png](https://i.328888.xyz/2023/04/16/iENcrH.png)

5. 在本地克隆新建的 GitHub 仓库。
</v-clicks>

---

# 二. Vitepress

1. 安装`node.js`和`npm`。

2. 安装`vitepress`。

```shell
npm install -D vitepress
```

3. 创建一个名为 `index.md` 的文件，这将是你的博客首页。

4. 创建一个名为 `.vitepress` 的文件夹，并在其中创建一个 `config.ts` 文件。该文件是你的博客的配置文件，你需要在其中设置博客的标题、描述、主题等信息。

---

5. 在 `.vitepress` 的文件夹下，创建一个 `theme/index.ts` 文件。该文件是主题配置文件，你可以在该文件中自定义主题，并且该文件将vue实例暴露出来，你可以绑定相关的vue插件。

```ts
import DefaultTheme from 'vitepress/theme'
// 一个vue组件库
import naive from 'naive-ui'

export default {
  ...DefaultTheme,
  enhanceApp({ app }) {
    // 将组件库绑定到vue实例中
    app.use(naive)
  },
}
```

6. 创建一个名为 blog 的文件夹，用于存储你的博客文章。在 blog 文件夹中创建一个名为 hello-world.md 的文件，并在其中写入你的第一篇博客文章。并在`.vitepress/config.ts`中配置相应的路由导航。

```ts
export default defineConfig({
  themeConfig: {
    nav: [
      { text: 'Blog', link: '/blog/', activeMatch: '/blog/' }
    ]
  }
})
```

---

7. 在命令行中使用以下命令启动 VitePress：

```shell
cd <path/to/your/repo>
vitepress dev
```

8. 在浏览器中打开 http://localhost:3000，你将看到你的博客主页和第一篇博客文章。可以通过修改 `index.md` 和 `hello-world.md` 中的内容来修改博客。

---

# 自动化部署

1. 创建一个 `.github/workflows/deploy.yml` 文件。

<div class="overflow-y-scroll h-sm">

```yml 
name: Deploy

on:
  push:
    branches:
      - master

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
        with:
          fetch-depth: 0
      - uses: actions/setup-node@v3
        with:
          node-version: 16
          cache: yarn
      - run: yarn install --frozen-lockfile

      - name: Build
        run: yarn build

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: .vitepress/dist
          # cname: example.com # if wanna deploy to custom domain
```
</div>

---

<div class="text-center">学习资源</div>

## 部署站点

1. [Github](https://github.com/)

2. [vercel](https://vercel.com/)

## 静态站点生成器

1. [Eleventy](https://www.11ty.dev/)

2. [Astro](https://astro.build/)

3. [Gatsby](https://www.gatsbyjs.com/)

4. [Vuepress](https://vuepress.vuejs.org/)

5. ...

---
layout: center
---

# 结语

希望这个简单的步骤可以帮助你快速搭建个人博客，期待看到你的作品！
