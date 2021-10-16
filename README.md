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
```bash
npm version 0.2.0 # 修改 package.json 版本号，并打一个 tag，待 push，commit 信息 0.0.2
git push origin --tags # push tags
git commit --amend -m 'feat(version):version to 0.2.0' # commit 信息不对，导致生成 log 有问题，需要修改
# 修上次提交记录，把 0.2.0 改为标准格式再生成，就可以生成 change log 了
```
npm version 时加上比较好的注释试试
```bash
zuo@zmac comitizen-practice-demo % npm version 0.4.0 -m 'feat(version):0.4.0 tag remark'
v0.4.0
zuo@zmac comitizen-practice-demo % git log
commit 0fdcd82353f3907c4a31e470402b6dce743b4b11 (HEAD -> main, tag: v0.4.0)
Author: zuoxiaobai <guoqzuo@gmail.com>
Date:   Fri Oct 15 06:58:20 2021 +0800

    feat(version):0.4.0 tag remark

# 再次生成 changelog 又不行了，空白
```

## 使用 standard-version 
上面的例子中，npm run version 更新版本号会直接提交，导致且 commit 信息就是版本号，不符合 commitizen 规范。导致手动生成 log 时，会是空白。[standard-version](https://github.com/conventional-changelog/standard-version) 就很好的解决了这个问题。安装后，只需要 npm run release，就可以有 npm run version 的功能，而且提交信息是标准的 commitizen 规范，而且自动生成 changelog 自动打 tag，自动 commit。你只需要 push 即可。
```bash
npm install standard-version --save-dev
```
scripts 设置
```js
// scripts
"release": "standard-version"
```

```bash
zuo@zmac comitizen-practice-demo % npm run release

> comitizen-practice-demo@0.4.1 release /Users/zuo/Desktop/fecloe/comitizen-practice-demo
> standard-version

✔ bumping version in package.json from 0.4.1 to 0.4.2
✔ bumping version in package-lock.json from 0.4.1 to 0.4.2
✔ created CHANGELOG.md
✔ outputting changes to CHANGELOG.md
✔ committing package-lock.json and package.json and CHANGELOG.md
✔ tagging release v0.4.2
ℹ Run `git push --follow-tags origin main` to publish
zuo@zmac comitizen-practice-demo %
# git push
# git push --tags
```

需要注意的是，CHANGELOG.md 是追加写入内容的，如果你之前没有对应的内容或删了之前的内容，会导致生成的内容较少，或者不完整。

### release 特定版本
```bash
# 0.4.1
npm run release # 0.4.1 => 0.4.2
npm run release -- --prerelease # 0.4.2 to 0.4.3-0
npm run release # 0.4.3-0 to 0.4.3
npm run release -- --prerelease alpha # 0.4.3 to 0.4.4-alpha.0

# patch、minor、major
npm run release -- --release-as minor  # 0.4.4-alpha.0 to 0.5.0
npm run release -- --release-as patch # 0.5.0 to 0.5.1
npm run release -- --release-as major # 0.5.1 to 1.0.0
npm run release -- --release-as prepatch # 1.0.0 to 1.0.1-0
npm run release -- --release-as preminor # 1.0.1-0 to 1.1.0-0
npm run release -- --release-as premajor # 1.1.0-0 to 2.0.0-0

# 手动指定版本
npm run release -- --release-as 2.1.3-alpha.1 # 2.0.0-0 to 2.1.3-alpha.1
# ✔ bumping version in package.json from 2.0.0-0 to 2.1.3-alpha.1
# ✔ bumping version in package-lock.json from 2.0.0-0 to 2.1.3-alpha.1
# ✔ tagging release v2.1.3-alpha.1
```
The newversion argument should be a valid semver string, a valid second argument to [semver.inc](https://github.com/npm/node-semver#functions) (one of patch, minor, major, prepatch, preminor, premajor,
## husk 校验
```bash
npm install husky --save-dev
```
安装 husky git hooks
```js
// package.json
{
  "scripts": {
    "prepare": "husky install"
  }
}
```
```bash
npm run prepare
# husky - Git hooks installed
```
commitizen hooks
```js
"husky": {
  "hooks": {
    "prepare-commit-msg": "exec < /dev/tty && git cz --hook || true",
  }
}
```
```bash
npx husky add .husky/pre-commit "npm test"
git add .husky/pre-commit
# 如果需要删除，直接 删除 .husky/pre-commit 文件即可

# 没有用，该提交的还是提交了。只是提交前，会自己运行 git cz
npx husky add .husky/prepare-commit-msg "exec < /dev/tty && git cz --hook || true"
git add .husky/prepare-commit-msg
# 查看当前目录 .husky 是否有生成 pre-commit, prepare-commit-msg 文件
```

## commitlint
commitlint[https://github.com/conventional-changelog/commitlint] 结合 husky 可以在 git commit 时校验 commit 信息是否符合规范
```bash
npm install -g @commitlint/cli @commitlint/config-conventional
# Configure commitlint to use conventional config
echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js

npx husky add .husky/commit-msg 'npx --no-install commitlint --edit "$1"'
```
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
