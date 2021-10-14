# comitizen-practice-demo
Vue 项目 commitizen + husky, git commit 提交信息规范校验 demo

## 初始化项目
```bash
npm install @vue/cli -g # 安装 @vue/cli
vue create comitizen-practice-demo
# [Vue 3] typescript, router, vuex, eslint, unit-mocha) 
```

## commitizen 提交测试
### docs 类型提交
```bash
# 修改 README.md
git add . # 添加到 git
git cz # 提交
# ? Select the type of change that you're committing: docs:     Documentation only changes
# ? What is the scope of this change (e.g. component or file name): (press enter to skip) readme
# ? Write a short, imperative tense description of the change (max 86 chars):
# (46) update readme.md, add init project description
# ? Provide a longer description of the change: (press enter to skip) 

# ? Are there any breaking changes? No
# ? Does this change affect any open issues? No
# [main caae82e] docs(readme): update readme.md, add init project description
# 1 file changed, 7 insertions(+)
# zuo@zmac comitizen-practice-demo % 
```
查看提交信息
```bash
zuo@zmac comitizen-practice-demo % git log
commit caae82ec7beb66423f190ab86a6343447b250046 (HEAD -> main)
Author: zuoxiaobai <guoqzuo@gmail.com>
Date:   Thu Oct 14 07:17:31 2021 +0800

    docs(readme): update readme.md, add init project description
```

### fix 类型提交
在 github 仓库提交一个 issue，看是否提交 fix 时，可以关联这个 issue

创建一个 issue [fix 类型提交关联 issue 测试 #1](https://github.com/zuoxiaobai/comitizen-practice-demo/issues/1)

### feat 类型提交
新增一个特性
```bash
feat(test): test feat type commit
```

## changelog 自动生成
```
$ npm install -g conventional-changelog-cli
$ cd my-project
$ conventional-changelog -p angular -i CHANGELOG.md -s
```
注意：默认版本是 package.json 中的 version 参数: "version": "0.1.0", 如果版本变更，需要使用 npm version '版本号'，修改版本号，再生成

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Run your unit tests
```
npm run test:unit
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
