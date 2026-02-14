# 狼人杀头像修复任务

## 问题分析
- 移动端头像不显示
- 根因：`.card` 使用 `height:0` + `paddingBottom:130%` 做等比容器，但 `.card-front/.card-back` 是 `position:absolute; height:100%`，在部分移动端浏览器中 `height:100%` 基于父元素的 `height:0` 计算，导致卡片正反面高度为0，内容不可见
- SVG 本身没问题，`makeAvatar` 函数生成的内嵌 SVG 是合法的

## 修复方案
- 将 `.card` 的 aspect-ratio hack 改为使用 CSS `aspect-ratio` 属性，同时保留 padding-bottom 作为 fallback
- 给 `.card-front/.card-back` 添加 `top:0;left:0` 确保定位正确
- 给 `.card` 添加明确的 `min-height` 防止塌陷

## 进度
- [x] 读取并分析代码
- [ ] 应用修复
- [ ] 推送到 GitHub
- [ ] 验证部署
