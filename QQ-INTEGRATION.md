# QQ 集成开发指南

## 概述
OpenClaw QQ 插件基于腾讯 QQ 开放平台，支持机器人消息收发、定时任务和技能扩展。

## 技术架构
- **插件 ID**: openclaw-qqbot
- **API**: QQ Bot API v2 (WebSocket + HTTP)
- **消息类型**: 文本、Markdown、图片、语音、文件
- **频道类型**: c2c (私聊), group (群聊)

## 开发环境设置
1. **插件安装**:
   ```bash
   # 从 npm 下载
   npm pack @tencent-connect/openclaw-qqbot
   # 解压到 extensions/
   tar -xzf *.tgz -C /home/ubuntu/.openclaw/extensions/openclaw-qqbot --strip-components=1
   ```

2. **配置更新**:
   - 添加到 openclaw.json plugins.allow
   - 添加到 plugins.entries
   - 重启网关

## API 调用示例
### 发送私聊消息
```bash
openclaw message send --channel qqbot --target "qqbot:c2c:openid" --message "内容"
```

### 日志分析
- 使用 `openclaw logs --limit 50` 查看最近消息
- openid 在日志的 `user_openid` 字段

## Cron 任务配置
- 编辑 `/home/ubuntu/.openclaw/cron/jobs.json`
- payload: agentTurn 消息
- delivery: channel=qqbot, to=qqbot:c2c:openid

## 故障排除
- **消息不发送**: 检查 token、openid、IP 白名单
- **插件不加载**: 确认 extensions/ 目录结构
- **日志无消息**: 确认机器人已添加到好友/群

## 扩展开发
- **添加技能**: 在 skills/ 下创建 SKILL.md
- **自定义命令**: 使用 slash-commands 技能
- **多媒体**: 支持图片上传和语音合成

## 当前配置
- AppID: 1903725624
- openid: 024A03C84189DB4BD6FBCFC39FB6B422
- 任务: 每日 8:00 天气报告