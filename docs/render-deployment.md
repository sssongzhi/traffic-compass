# 个人线上部署（Render 免费版）

代码仓库：https://github.com/sssongzhi/traffic-compass

## 部署

1. 登录 Render，打开 https://dashboard.render.com/select-repo?type=blueprint ，选择该仓库，读取根目录 `render.yaml`。
2. 填写 `DEEPSEEK_KEY`（自己的 DeepSeek API Key），只填写到 Render，不提交 GitHub。
3. 确认使用 Free 计划后部署。等待服务显示 Live，打开 Render 提供的 HTTPS 地址。
4. 当前按个人选择使用免密码访问，打开地址即可使用。
5. 粘贴一段文案运行审核，确认报告和追问均正常。

若手动创建 Web Service：Root Directory 为 `webapp`，Build Command 为 `pip install -r requirements.txt`，Start Command 为 `uvicorn app:app --host 0.0.0.0 --port $PORT`，Health Check 为 `/healthz`。环境变量按 `render.yaml` 配置，免密码模式不设置 `ACCESS_PASSWORD` 和 `REQUIRE_ACCESS_AUTH`。

## 使用限制

- 免费实例空闲后休眠，首次重新打开可能需要等待启动。
- 本地文件系统不持久：历史聊天、账号、预测记录，以及在网页设置里保存的 Key，可能在重启或重新部署后丢失。请把 DeepSeek Key 配在 Render 环境变量中；重要记录使用网页导出功能另存。
- 云端仅启用文字模式。抖音扫码登录和依赖本机 Cookie 的链接提取不适合此部署。
- Render 免费托管不包含 DeepSeek API 调用费用。
- 当前页面和接口无需密码即可访问。以后若需开启保护，在 Render 设置 `ACCESS_PASSWORD` 和 `REQUIRE_ACCESS_AUTH=1`；用户名默认为 `owner`。强制保护模式缺少密码会拒绝启动。

## 后续更新

修改提交到此 GitHub 仓库后，Render 可自动重新部署。不要提交 `.env`、API Key、Cookie 或 `_data` 中的数据库。
