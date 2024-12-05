---
date: '2024-12-06T12:46:50+08:00'
title: '使用code-server实现多端撰写部署'
draft: false
tags: ["code-server"]
categories: ["code-server"]
---


> hugo搭建OK了，但是还
[text](../posts/my-first-post.md)


[text](../posts/my-first-post.md)

在 Code Server 中，可以通过 **VS Code 插件市场** 安装扩展来增强功能。以下是一些轻量级且常用的插件推荐，它们可以提高效率，同时占用较少的系统资源和性能：

---

### **1. 基础效率类插件**
这些插件专注于提升日常开发的便利性：

#### **Bracket Pair Colorizer 2**
- **功能**：为括号、花括号、方括号着色，方便查看匹配。
- **性能**：占用资源少，不会显著影响编辑器速度。
- **替代**：VS Code 原生功能（如果你的 Code Server 是新版本）。

---

#### **Prettier - Code Formatter**
- **功能**：格式化代码，支持 JavaScript、HTML、CSS 等多种语言。
- **性能**：只在格式化时工作，不占用额外资源。
- **推荐使用场景**：团队协作，统一代码风格。

---

#### **GitLens**
- **功能**：可视化 Git 提交记录、变更日志、代码作者等信息。
- **性能**：默认配置占用资源少，大型项目可能需优化设置。
- **替代方案**：仅使用 VS Code 自带的 Git 支持。

---

### **2. Markdown 和文档类插件**
适合你的博客撰写场景：

#### **Markdown All in One**
- **功能**：支持 Markdown 快捷键、实时预览、目录生成等。
- **性能**：轻量级，占用资源很小。
- **推荐理由**：博客撰写的高效工具。

---

#### **Markdown Preview Enhanced**
- **功能**：提供功能丰富的 Markdown 预览，支持数学公式、图表等高级功能。
- **性能**：渲染复杂内容时稍有性能开销，但总体较轻量。

---

### **3. 代码片段和自动补全**
提高代码撰写效率的插件：

#### **Auto Rename Tag**
- **功能**：编辑 HTML/XML 标签时自动更新配对标签。
- **性能**：占用资源极小。
- **适用场景**：Web 开发。

---

#### **Path Intellisense**
- **功能**：为文件路径提供智能补全。
- **性能**：轻量且高效。
- **适用场景**：频繁处理路径引用的项目。

---

#### **TabNine (免费版)**
- **功能**：AI 驱动的代码补全工具，支持多语言。
- **性能**：占用资源低于 Copilot，但依赖网络。
- **适用场景**：希望提升代码补全效率但资源有限时。

---

### **4. 文件管理和搜索类**
优化文件导航和搜索体验的插件：

#### **Project Manager**
- **功能**：快速切换项目和管理工作区。
- **性能**：占用资源低。
- **推荐理由**：方便在 Code Server 多项目之间快速切换。

---

#### **VSCode-icons**
- **功能**：为文件和文件夹提供图标，增强文件导航体验。
- **性能**：只影响界面渲染，不影响编辑器性能。

---

### **5. 开发语言支持**
根据你的开发语言选择语言支持插件：

#### **Java Extension Pack**
- **功能**：Java 语言开发支持，包括调试、Maven、Spring Boot 等。
- **性能**：单独安装核心插件（如 Language Support for Java）以降低占用。
- **适用场景**：Java 开发。

#### **Python**
- **功能**：Python 代码补全、调试支持。
- **性能**：对于小型 Python 项目，性能开销可忽略。

#### **vscode-eslint**
- **功能**：JavaScript 和 TypeScript 的代码风格校验。
- **性能**：资源占用低，适合前端开发。

---

### **6. Docker 和 DevOps 支持**
适合在 Code Server 上直接进行容器化开发或服务器运维。

#### **Docker**
- **功能**：管理和运行容器，查看 Docker 镜像、容器日志等。
- **性能**：对资源要求较低，尤其适合已有 Docker 环境的项目。

#### **Remote - SSH**
- **功能**：通过 SSH 管理远程服务器。
- **性能**：资源占用小，视网络速度而定。

---

### **7. 轻量调试插件**
对于简单调试需求，可以选择以下插件：

#### **Debugger for Java**
- **功能**：支持 Java 项目的调试。
- **性能**：小型项目几乎无额外性能开销。

#### **REST Client**
- **功能**：在编辑器中直接测试 HTTP 请求。
- **性能**：资源占用极低。
- **适用场景**：替代 Postman 等工具，适合测试 API。

---

### **安装插件的方法**
1. 打开 Code Server 的扩展市场：
   - 点击左侧活动栏中的 **扩展图标**。
2. 搜索并安装所需插件。
3. 如果无法连接到市场，可以配置国内镜像：
   - 编辑 `settings.json` 添加以下内容：
     ```json
     {
       "extensionsGallery": {
         "serviceUrl": "https://marketplace.visualstudio.com/_apis/public/gallery",
         "cacheUrl": "https://vscode.blob.core.windows.net/gallery/index",
         "itemUrl": "https://marketplace.visualstudio.com/items"
       }
     }
     ```

---

### **总结**
- **Markdown 编辑**：使用 `Markdown All in One` 和 `Markdown Preview Enhanced`。
- **代码协作**：使用 `GitLens` 和 `Prettier`。
- **开发效率**：根据语言选择语言支持插件，结合 `Path Intellisense` 和 `Auto Rename Tag`。
- **资源占用控制**：避免安装过多插件，保持核心功能即可。

如需更详细的配置或具体插件优化建议，请告诉我！