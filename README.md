# 简化版表单收集系统

一个基于GitHub Issues的轻量级信息收集系统，支持24小时自动清理，完全免费且易于部署。

## 🌟 系统特性

- **零成本部署**：基于GitHub Pages和Issues，无需服务器
- **24小时自动清理**：通过GitHub Actions自动删除过期数据
- **响应式设计**：支持手机、平板、电脑等各种设备
- **简单易用**：5分钟即可完成部署
- **数据透明**：所有提交都可在GitHub Issues中查看
- **隐私保护**：不收集IP地址等敏感信息

## 🚀 快速开始

### 1. 配置GitHub Token（必需）

1. 访问：https://github.com/settings/tokens
2. 点击 "Generate new token (classic)"
3. 设置Token权限：
   - ✅ `public_repo`（公开仓库访问）
   - ✅ `repo`（私有仓库访问，如果使用私有仓库）
4. 生成Token并**妥善保存**

### 2. 配置表单页面

1. 打开 `simple-github-form.html`
2. 找到以下配置部分：
```javascript
const GITHUB_CONFIG = {
    owner: 'Neilni2099',           // 你的GitHub用户名
    repo: 'form-collector-auto',   // 当前仓库名
    token: 'YOUR_GITHUB_TOKEN'     // 替换为你的GitHub Token
};
```
3. 将 `YOUR_GITHUB_TOKEN` 替换为你生成的Token

### 3. 启用GitHub Pages

1. 进入仓库设置：Settings → Pages
2. 选择部署源：
   - **Source**: Deploy from a branch
   - **Branch**: main
   - **Folder**: /
3. 点击保存，等待部署完成

### 4. 获取表单链接

部署完成后，你的表单地址将是：
```
https://[你的用户名].github.io/form-collector-auto/simple-github-form.html
```

## 📋 使用方法

### 提交信息
1. 访问表单页面
2. 填写姓名、学号等必填信息
3. 可选择上传附件（最大5MB）
4. 点击提交按钮

### 查看数据
1. 进入你的GitHub仓库
2. 点击 "Issues" 选项卡
3. 所有表单提交都会显示为Issues
4. 每个Issue都包含完整的提交信息

### 管理数据
- **手动删除**：在Issues页面关闭或删除特定Issue
- **批量清理**：使用GitHub Actions工作流自动清理
- **修改清理时间**：编辑 `.github/workflows/auto-cleanup.yml` 文件

## ⚙️ 自定义配置

### 修改清理时间
编辑 `.github/workflows/auto-cleanup.yml`：
```yaml
# 修改清理时间（默认24小时）
cutoffTime = new Date(now.getTime() - 48 * 60 * 60 * 1000);  # 改为48小时
```

### 修改文件大小限制
编辑 `simple-github-form.html`：
```javascript
if (file && file.size > 10 * 1024 * 1024) {  // 改为10MB
```

### 添加新字段
在表单中添加新字段：
```html
<div class="mb-3">
    <label for="newField" class="form-label">新字段</label>
    <input type="text" class="form-control" id="newField" name="newField">
</div>
```

## 🔧 故障排除

### 常见问题

**1. 提交失败**
- 检查GitHub Token是否正确配置
- 确认Token有足够权限
- 查看浏览器控制台错误信息

**2. 自动清理不工作**
- 检查GitHub Actions是否启用
- 查看Actions日志获取详细错误
- 手动触发工作流进行测试

**3. 页面无法访问**
- 确认GitHub Pages已启用
- 检查仓库是否为公开
- 等待几分钟让部署完成

### 调试工具

**查看提交日志**：
1. 进入仓库的Actions选项卡
2. 点击最新的工作流运行
3. 查看详细日志信息

**测试API连接**：
```bash
curl -H "Authorization: token YOUR_TOKEN" \
     https://api.github.com/user
```

## 📊 数据格式

每个表单提交会创建一个Issue，格式如下：

```markdown
## 信息收集表单提交

**提交时间：** 2024-01-27 15:30:45

### 基本信息
- **姓名：** 张三
- **学号：** 2024001
- **备注：** 需要特别说明的内容

### 系统信息
- **浏览器：** Mozilla/5.0...
- **提交时间戳：** 1643280645000

### 处理说明
此Issue将在24小时后自动删除。
```

## 🎯 使用场景

- **班级信息收集**：学生信息、联系方式等
- **活动报名**：会议、培训、聚会报名
- **问卷调查**：简单的意见收集
- **文件收集**：作业、作品、证明材料上传

## 📱 移动端支持

- 完全响应式设计
- 支持手机拍照上传
- 触摸友好的表单控件
- 优化的移动端体验

## 🔒 安全说明

- 所有数据存储在GitHub Issues中
- 24小时后自动删除，不留痕迹
- 不收集用户IP地址等敏感信息
- 仅收集表单中明确要求的字段
- 支持HTTPS加密传输

## 🤝 贡献指南

欢迎提交Issue和Pull Request来改进这个系统！

## 📞 技术支持

如有问题，请通过以下方式联系：
1. 在GitHub仓库提交Issue
2. 查看Actions日志获取错误信息
3. 参考本README的故障排除部分

---

**⭐ 如果觉得有用，请给仓库点个Star！**