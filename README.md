### 快速开始

#### 1. 初始化环境配置

复制 `.env.example` 为 `.env` 并修改环境变量值：

```bash
cp .env.example .env
vim .env
```

- RESTIC_REPOSITORY: 设置备份仓库位置。
- RESTIC_PASSWORD: 设置仓库密码。
- HEALTHCHECKS_URL: 设置 HealthChecks 地址。

#### 2. 添加服务配置

在 

在 `main.yaml` 的 `includes` 部分引入单个服务的配置文件：

```diff
@@ -3,3 +3,4 @@ version: "1"
 includes:
   - "profiles/00_global.yaml"
   - "profiles/01_base.yaml"
+  - "profiles/vaultwarden.yaml"
```

#### 3. 验证配置

使用以下命令检查服务配置是否正确：

```bash
# 列出所有配置文件内容
resticprofile -c ./main.yaml

# 查看特定服务（如 vaultwarden）的配置详情
resticprofile -c ./main.yaml -n vaultwarden show
```

### 常用命令

```bash
# 不运行 restic 命令，而是显示命令行
resticprofile -c ./main.yaml -n vaultwarden --dry-run backup
# 运行 restic 命令，但不写入仓库
resticprofile -c ./main.yaml -n vaultwarden backup --dry-run
# 正常运行 restic 命令
resticprofile -c ./main.yaml -n vaultwarden backup
``` 