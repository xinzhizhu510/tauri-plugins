# 发布到 GitHub Packages

本仓库已配置为自动构建和发布包到 GitHub Packages (`npm.pkg.github.com`)。

## 自动发布

当代码推送到 `main` 或 `release` 分支时，GitHub Actions 将自动：
1. 构建所有插件包
2. 将包发布到 GitHub Packages
3. 为每个发布的包创建 Git 标签（格式：`包名@版本号`，例如 `tauri-plugin-auth@0.2.3`）

## 手动发布

你也可以在 GitHub Actions 页面手动触发发布工作流。

## 包列表

以下包将被发布到 GitHub Packages：

- `@xinzhizhu510/tauri-plugin-auth`
- `@xinzhizhu510/tauri-plugin-context-menu`
- `@xinzhizhu510/tauri-plugin-geolocation`
- `@xinzhizhu510/tauri-plugin-haptic-feedback`
- `@xinzhizhu510/tauri-plugin-iap`
- `@xinzhizhu510/tauri-plugin-map-display`
- `@xinzhizhu510/tauri-plugin-notifications`
- `@xinzhizhu510/tauri-plugin-sharing`

## 使用已发布的包

要在你的项目中使用这些包，需要配置 npm 以使用 GitHub Packages：

1. 在项目根目录创建 `.npmrc` 文件：
```
@xinzhizhu510:registry=https://npm.pkg.github.com
```

2. 安装包：
```bash
npm install @xinzhizhu510/tauri-plugin-auth
```

3. 如果包是私有的，你需要使用 GitHub Personal Access Token (PAT) 进行身份验证：
```bash
npm login --registry=https://npm.pkg.github.com
```

## 本地构建

要在本地构建所有包：

```bash
# 安装依赖
npm install

# 构建所有包（排除 example-app）
npx lerna run build --stream --ignore @xinzhizhu510/tauri-plugin-example-app
```

## 配置说明

- **lerna.json**: 配置了 Lerna 使用 GitHub Packages registry
- **.npmrc**: 配置了包的作用域和认证
- **.github/workflows/publish.yml**: 自动构建和发布工作流，包括自动创建和推送 Git 标签
- **.github/workflows/build.yml**: PR 和开发分支的构建验证工作流
- **packages/*/package.json**: 每个包都配置了正确的 registry 和 repository URL

## Git 标签管理

### 自动标签创建

从现在开始，每次通过 GitHub Actions 发布包时，工作流会自动为每个发布的包创建 Git 标签。标签格式为 `包名@版本号`，例如：

- `tauri-plugin-auth@0.2.3`
- `tauri-plugin-iap@0.2.3`
- `tauri-plugin-geolocation@0.1.6`

这些标签可以用于：
- 在 Git 历史中标记特定版本
- 创建 GitHub Releases
- 方便用户查看和下载特定版本的代码

### 推送现有版本的标签

对于已经发布但尚未打标签的版本，可以使用以下命令手动创建和推送标签：

```bash
# 为当前已发布的包创建标签（本地）
git tag -a tauri-plugin-auth@0.2.3 -m "Release tauri-plugin-auth version 0.2.3"
git tag -a tauri-plugin-context-menu@0.1.4 -m "Release tauri-plugin-context-menu version 0.1.4"
git tag -a tauri-plugin-geolocation@0.1.6 -m "Release tauri-plugin-geolocation version 0.1.6"
git tag -a tauri-plugin-haptic-feedback@0.1.4 -m "Release tauri-plugin-haptic-feedback version 0.1.4"
git tag -a tauri-plugin-iap@0.2.3 -m "Release tauri-plugin-iap version 0.2.3"
git tag -a tauri-plugin-map-display@0.2.3 -m "Release tauri-plugin-map-display version 0.2.3"
git tag -a tauri-plugin-notifications@0.1.3 -m "Release tauri-plugin-notifications version 0.1.3"
git tag -a tauri-plugin-sharing@0.2.3 -m "Release tauri-plugin-sharing version 0.2.3"

# 推送所有标签到远程仓库
git push --tags
```

**注意**：推送标签需要对仓库有写入权限。
