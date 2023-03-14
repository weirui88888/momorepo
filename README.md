# momorepo学习

a monorepo generated by lerna，record some useful code

# 简介

该 repo 是由 lerna 搭建而成，是一个标准的 momorepo 类型的仓库，packages 的管理模式是 independent，也就是 packages 下面的每个包都会拥有独立的版本

```javascript
lerna init --independent // 如果不带--independent参数，那么packages下面的所有包都会共享一个版本，任何一个包中发生了改变，其他的所有包都会发版，因为他们要共享一个版本，感觉这样的话丢失了实用lerna的本意
```

关于更多关于 lerna 的用法和介绍可参考

[lerna 管理前端模块最佳实践](https://juejin.cn/post/6844903568751722509)
[基于 lerna 管理 packages 的 Monorepo 项目最佳实践](https://juejin.cn/post/6844903911095025678)
[lerna 命令总结](https://juejin.cn/post/7033673456751214600#heading-2)

# verdaccio 搭建简单本地 npm 仓库服务

该项目在学习使用 lerna 发包阶段比较合适配合 Verdaccio 这个工具库进行演示，如果熟悉了 lerna 发包流程，则该模块不需要关注

- 第一步：先全局安装 verdaccio
- 第二步：终端中执行 verdaccio 将会启动一个本地服务器，模拟 npm 仓库
- 第三步：在该 repo 终端下，执行 npm adduser --registry http://localhost:4873/ 注册一个上述本地服务器的用户后才可以进行发包
- 第四步：开发包，提交 commit 后，执行 lerna publish --no-push 即可指发包，不提交记录到 origin master 上

**注:** 为了将我们 packages 下面的包发布到本地，我们需要注意三件事

- 根目录下面要创建一个.npmrc 文件，配置一个 npm 源 registry='http://localhost:4873/'
- 通过 lerna create 创建的包中，package.json 中的 publishConfig.registry 需要删掉
- 当我们需要发布正式的包到 npm 仓库或者公司私有库中时，需要替换上面的 registry 为对应的仓库地址即可

# 搭建

一个合格的仓库当然要添加这些工程化配置，作为工程师的我们，只需要把眼光聚焦在代码本身这件事上

## 1.prettier

```javascript
npm i -D prettier // 安装后创建.prettierignore与.prettierrc.js进行配置
```
