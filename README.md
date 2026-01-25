#### 📌 步骤 1：重新生成 GitHub 令牌
> 核心：必须选择 `Tokens (classic)` 类型，fine-grained 令牌权限逻辑更复杂，新手不推荐

1. 打开 GitHub 主页，点击右上角**头像** → `Settings`（设置）
2. 左侧导航栏下滑，点击 `Developer settings`（开发者设置）
3. 选择 `Personal access tokens` → `Tokens (classic)`
4. 点击 `Generate new token (classic)`，进入令牌配置页：
   | 配置项 | 推荐值 | 说明 |
   |--------|--------|------|
   | Note | `bookmark-backup` | 令牌备注，便于后续识别用途 |
   | Expiration | `No expiration` | 有效期（也可自定义，建议至少 90 天） |
   | Scopes（权限） | ✅ `repo` 分类下**所有子项** | 必须勾选：<br>- repo:status<br>- repo_deployment<br>- public_repo<br>- repo:invite<br>- security_events<br>- workflow |
5. 点击 `Generate token`，**立即复制令牌**（仅显示一次，丢失需重新生成）
   > ⚠️ 重要：复制后妥善保存，不要泄露给他人

#### 📌 步骤 2：验证仓库权限
确保令牌所属账号对目标仓库有**写入权限**：

##### 场景 1：仓库属于个人
直接确认：
- 仓库 URL 格式：`https://github.com/你的账号/仓库名`
- 确保登录的 GitHub 账号是该仓库的**所有者**

##### 场景 2：仓库属于组织
需额外授权：
1. 进入组织主页 → `Settings`（设置）
2. 左侧导航栏选择 `Third-party access`（第三方访问）
3. 找到你的令牌（备注为 `bookmark-backup`）→ 点击 `Grant` 授权访问该组织
   （或在组织 `Settings` → `Personal access tokens` 中确认令牌已授权）

#### 📌 可选：验证令牌有效性
生成令牌后，可通过 curl 快速验证权限（替换占位符）：
```bash
curl -H "Authorization: token 你的令牌" https://api.github.com/repos/你的账号/仓库名
