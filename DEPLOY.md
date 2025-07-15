# 部署说明

## 🚀 快速部署

### 前置条件

确保本地环境已安装：

- Go 1.21+
- Node.js 22+
- npm

### 部署步骤

1. **执行部署脚本**

   ```bash
   ./deploy.sh
   ```

2. **部署过程**
   - 构建 Go 后端应用
   - 构建 Vue 前端应用
   - 清理服务器旧数据
   - 上传文件到服务器
   - 配置 Nginx 反向代理
   - 启动 systemd 服务

### 🌐 访问地址

- **前端界面**: http://49.233.41.155
- **后端 API**: http://49.233.41.155/api

### 📋 服务器配置

- **服务器**: 49.233.41.155
- **后端服务路径**: /opt/gin-web-server
- **前端文件路径**: /var/www/gin-web-server
- **服务名称**: gin-web-server

### 🔧 服务器管理命令

```bash
# 查看服务状态
systemctl status gin-web-server

# 启动服务
systemctl start gin-web-server

# 停止服务
systemctl stop gin-web-server

# 重启服务
systemctl restart gin-web-server

# 查看日志
journalctl -u gin-web-server -f

# 重新加载Nginx配置
systemctl reload nginx
```

### 📁 文件结构

```
服务器文件结构:
├── /opt/gin-web-server/         # 后端应用
│   ├── gin-web-server          # 二进制文件
│   └── data/                   # 数据目录
│       └── persons.db          # SQLite数据库
├── /var/www/gin-web-server/    # 前端文件
│   ├── index.html
│   ├── assets/
│   └── ...
└── /etc/nginx/sites-available/gin-web-server  # Nginx配置
```

### 🧹 数据清理

部署脚本会自动清理以下旧数据：

- 旧的静态文件 (static, templates, uploads)
- 旧的前端文件
- 旧的 Nginx 配置链接

**注意**: 数据库文件默认会保留，如需清理请手动删除或修改部署脚本。

### 🔍 故障排查

1. **服务无法启动**

   ```bash
   journalctl -u gin-web-server -n 50
   ```

2. **前端无法访问**

   ```bash
   nginx -t
   systemctl status nginx
   ```

3. **API 请求失败**
   ```bash
   curl http://localhost:8080/api/persons
   ```

### 🔄 更新部署

重新执行部署脚本即可：

```bash
./deploy.sh
```

### 📝 注意事项

1. 确保服务器已安装 Nginx
2. 确保服务器防火墙开放 80 端口
3. 数据库文件会自动创建在 `/opt/gin-web-server/data/` 目录
4. 部署会自动清理旧的静态文件，但保留数据库文件
