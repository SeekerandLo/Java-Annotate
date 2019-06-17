## [Travis](https://www.travis-ci.org)
- 自信的测试和发布  
- 使用 `Travis CI` 同步你的 `GitHub Projects`,你可以1分钟的测试你的代码 

## 向导
这是一个非常短的向导使用 Travis CI 和你的 GitHub 代码托管仓库，如果你是一个持续集成的新人或者想知道更多信息关于 Travis CI 做什么，去看 [Core Concepts for Beginners]()

### 前提
- 一个 `GitHub` 账户
- 在 `GitHub` 上托管项目的权限

### 开始使用 Travis CI
1. 去 [Travis-ci.com](Travis-ci.com)，使用 GitHub 账号注册
2. 接收 Travis CI 的授权，你会回调到 GitHub
3. 点击活动的绿色按钮，选择想使用 Travis CI 的项目
4. 添加 `.travis.yml` 文件到你的项目中，这个文件是告诉 Travis CI 怎么做，做什么。下面是一个 Ruby 语言的具体例子，应该在 `Ruby2.2` 的环境下，使用最新版本的 `JRuby`
    ```yml
    language: ruby
    rvm:
    - 2.2
    - jruby
    ``` 
    Ruby 项目默认安装依赖的命令是 `build install`，`rake` 构建项目
5. 添加 `.travis.yml` 到 git 仓库，提交和推送，去触发 Travis CI 的构建
    ```
    当你添加 .travis.yml 文件后，Travis 会在你提交、推送之后运行
    ```
6. 通过访问 Travis CI 选择你的仓库，通过命令返回的状态在构建状态页面检查自己是否构建通过或失败。


### 选择不同的语言
```yml
language: ruby
```
```yml
language: java
```
```yml
language: node_js
```
```yml
language: python
```
```yml
language: php
```
如果你需要在 macOS 测试或运行项目，或者项目使用 [Swift](https://baike.baidu.com/item/SWIFT/14080957?fr=aladdin) 或者 [Objective-C](https://baike.baidu.com/item/SWIFT/14080957?fr=aladdin)，使用 **macOS** 的环境
```yml
os: osx
```
> 你不必要去使用 macOS 如果你在 Mac 上开发，macOS 仅仅在你使用 Swift，Objective-C 或者其他 macOS-specific 软件时被需要

Travis CI 支持[多种语言](https://docs.travis-ci.com/user/languages/)

### 不仅仅是运行测试
Travis CI 不仅仅是为了运行测试，这有许多你能用你的代码做的事：
- 部署到 [GitHub 页面](https://docs.travis-ci.com/user/deployment/pages/)
- 在 [Heroku](https://docs.travis-ci.com/user/deployment/heroku/) 上运行应用
- 上传 [RubyGems](https://docs.travis-ci.com/user/deployment/heroku/)
- 发送 [通知](https://docs.travis-ci.com/user/notifications/)

### 阅读更多
阅读更多
- [定制 build](https://docs.travis-ci.com/user/customizing-the-build)
- [保护数据的最佳实践](https://docs.travis-ci.com/user/best-practices-security/)
- [build states](https://docs.travis-ci.com/user/build-stages/)
- [build matrixs](https://docs.travis-ci.com/user/customizing-the-build/#build-matrix)
- [installing dependencies](https://docs.travis-ci.com/user/customizing-the-build/#build-matrix)
- [setting up databases](https://docs.travis-ci.com/user/database-setup/)