# MoonTV/LunaTV 配置编辑器
https://hafrey1.github.io/LunaTV-config  

--- 

## DigitalPlat 免费域名注册链接(us.kg)
免费注册 **.qzz.io  和 **.qd.je 域名,成功注册后多获得+1个免费域名额度

[注册地址](https://dash.domain.digitalplat.org/signup?ref=628Y3lAzQY)

##  MoonTV/LunaTV配置
订阅使用：复制下面链接  

👉 Base58编码订阅链接[精简版🎬源链接](https://raw.githubusercontent.com/hafrey1/LunaTV-config/refs/heads/main/jin18.txt)    （推荐使用自己部署的代理）精简版禁18源

```bash
https://pz.v88.qzz.io?format=2&source=jin18
```
```bash
https://raw.githubusercontent.com/hafrey1/LunaTV-config/refs/heads/main/jin18.txt
```
👉 Base58编码订阅链接[精简版🎬+🔞源链接](https://raw.githubusercontent.com/hafrey1/LunaTV-config/refs/heads/main/jingjian.txt) （推荐使用自己部署的代理）精简版剔除无搜索结果和污染搜索结果源                             
```bash
https://pz.v88.qzz.io?format=2&source=jingjian
```
```bash
https://raw.githubusercontent.com/hafrey1/LunaTV-config/refs/heads/main/jingjian.txt
```

👉 Base58编码订阅链接[完整版🎬+🔞源链接](https://raw.githubusercontent.com/hafrey1/LunaTV-config/refs/heads/main/LunaTV-config.txt) （推荐使用自己部署的代理）                          
```bash
https://pz.v88.qzz.io?format=2&source=full
```
```bash
https://raw.githubusercontent.com/hafrey1/LunaTV-config/refs/heads/main/LunaTV-config.txt
```

--- 

# 🌐 CORSAPI（API 代理 & JSON 订阅器）

这是一个基于 **Cloudflare Workers** 的中转代理 + JSON 配置前缀替换工具。

支持将 API 请求通过 Worker 转发，并自动为 JSON 配置中的 `api` 字段添加/替换前缀。

同时支持生成 **Base58 编码的订阅格式**，并提供**多种配置源选择**，方便在外部应用中快速使用。

---

<details>
  
<summary>✨ 功能特性</summary>
  
# 

### 1. 通用 API 代理

使用 `?url=` 参数转发任意 API 请求

**示例：**

```
https://<你的域名>/?url=https://ikunzyapi.com/api.php/provide/vod/
```

### 2. 多配置源支持

使用 `?source=` 参数选择不同的资源配置：

- **`source=jin18`** - 精简版（31个资源，仅普通内容）
- **`source=jingjian`** - 精简+成人版（61个资源）
- **`source=full`** - 完整版（88个资源，**默认**）

### 3. 统一的 format 参数

使用 `?format=` 参数控制输出格式

- **`format=0`** 或 **`format=raw`** - 原始 JSON
- **`format=1`** 或 **`format=proxy`** - 添加代理前缀的 JSON
- **`format=2`** 或 **`format=base58`** - 原始 JSON 的 Base58 编码
- **`format=3`** 或 **`format=proxy-base58`** - 代理前缀 JSON 的 Base58 编码

--- 

</details>

<details>
  
<summary>🚀 部署方法</summary>
  
#   

🌐 部署到 Cloudflare Workers

1. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com)。
2. 进入 Workers & Pages → 创建应用程序（Create Application） → Workers → 从 Hello World! 开始 → 项目命名 → 部署 → 编辑代码。
3. 将项目中的 _worker.js 文件内容复制到在线编辑器中。
4. 点击 保存并部署（Save and Deploy） 完成上线。
5. （可选）若项目使用 KV 存储：
- 存储和数据库 → Workers KV → Ceate instance  → 命名空间名称（KV Namespaces） 创建一个新的命名空间。
- 命名空间名称可自定义，例如：MyKVNamespace。
- 在 Worker设置 绑定 → 添加绑定 → KV命名空间 → 添加绑定 → 变量名为：CONFIG_KV → 创建的KV命名空间 → 添加绑定 。
6. 绑定自定义域名：打开 Worker 设置 → Triggers(域和路由) → 添加 → Custom Domains(自定义域名)，添加你的域名并保存。

📦 部署到 Cloudflare Pages

1. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com)。
2. 下载仓库中的 _worker.js 文件。
3. 在本地新建一个空文件夹（名称随意），将 _worker.js 放入其中。
4. 前往 Workers & Pages → 创建应用程序（Create Application） → Pages → 上传资产（开始使用） → 项目命名 → 创建项目 → 从计算机中选择 → 上传文件夹 → 选择新建的文件 → 部署站点（Deploy Site）。
5. （可选）如需使用 KV：
- 存储和数据库 → Workers KV → Ceate instance  → 命名空间名称（KV Namespaces） 创建一个KV命名空间。
- 新建命名空间（名称随意），绑定变量名为：CONFIG_KV。
- 部署完成后，前往 Pages 控制台 → 设置 → 绑定（Bindings） → 添加 → KV 命名空间  →  变量名为：CONFIG_KV → 选择创建的KV空间 → 保存。
- 保存后返回 “部署” 选项卡。
8. 点击 创建新部署（Create New Deployment），重新上传文件并点击 保存并部署 即可。

- 部署完成后，你就拥有了自己的 API 代理与订阅转换服务！

---   

</details>

<details>
<summary>🔗 使用示例</summary>
  
#  

假设你的 Worker 部署在：[`https://api.example.workers.dev`](https://api.example.workers.dev)

### 示例 1：代理任意 API

```
https://api.example.workers.dev/?url=https://ikunzyapi.com/api.php/provide/vod/
```

### 示例 2：获取原始 JSON 配置（精简+成人版）

```jsx
https://api.example.workers.dev/?format=0&source=jingjian
```

### 示例 3：获取代理前缀的 JSON 配置（精简+成人版）

```jsx
https://api.example.workers.dev/?format=1&source=jingjian
```

### 示例 4：获取原始 Base58 编码（精简+成人版）

```jsx
https://api.example.workers.dev/?format=2&source=jingjian
```

### 示例 5：获取代理前缀的 Base58 编码订阅（精简+成人版）

```jsx
https://api.example.workers.dev/?format=3&source=jingjian
```

### 示例 6：自定义代理前缀

```jsx
https://api.example.workers.dev/?format=1&source=full&prefix=https://my-proxy.com/?url=
```

---   
  
</details>

<details>
<summary>🛠️ 参数说明</summary>
  
# 
  
| 参数     | 说明             | 可选值                          | 示例         |        
| -------- | ---------------- | ------------------------------- | ------------ |
| `url`    | 代理任意 API 请求 | 任意有效 URL                     | `?url=https://...` |
| `format` | 配置模式         | `format=0 或 raw - 原始 JSON` <br> `format=1 或 proxy - 添加代理前缀` <br> `format=2 或 base58 - 原始 Base58` <br> `format=3 或 proxy-base58 - 代理 Base58` | `?format=0` |
| `source` | 配置源选择       | `source=jin18` - 精简版 <br> `source=jingjian` - 精简+成人 <br> `source=full` - 完整版） | `?source=jin18` |
| `prefix` | 自定义代理前缀   | 任意代理地址                      | `?prefix=https://.../?url=` |
| `errors&limit=10` | 查看错误日志 | `errors&limit=10`                 | `https://<你的域名>?errors&limit=10` |

---  

## 📦 配置源对比

| 配置源 | 资源数量 | 包含成人内容 | 适用场景 |
| --- | --- | --- | --- |
| **jin18** | 31个 | ❌ 否 | 家庭使用、轻量级应用 |
| **jingjian** | 61个 | ✅ 是 | 个人使用、中等需求 |
| **full** | 88个 | ✅ 是 | 完整功能、最大兼容性 |


🧩 **前缀替换逻辑**  
- 若 JSON 中的 `api` 字段已包含旧前缀（`?url=`），系统会自动去除旧前缀并替换为新的代理前缀。  
- 可自定义代理路径，方便接入私有 API 或多 Worker 配置。
  
---   
  
</details>

<details>
<summary> 📋 完整订阅链接模板</summary>
  
# 

将 `\<你的域名\>` 替换为你的实际 Worker 地址：

### 精简版（jin18）

```jsx
# 原始 JSON
https://<你的域名>/?format=0&source=jin18

# 带代理前缀的 JSON
https://<你的域名>/?format=1&source=jin18

# 原始 Base58 编码
https://<你的域名>/?format=2&source=jin18

# 代理 Base58 编码（推荐用于订阅）
https://<你的域名>/?format=3&source=jin18
```

### 精简+成人版（jingjian）

```jsx
# 原始 JSON
https://<你的域名>/?format=0&source=jingjian

# 带代理前缀的 JSON
https://<你的域名>/?format=1&source=jingjian

# 原始 Base58 编码
https://<你的域名>/?format=2&source=jingjian

# 代理 Base58 编码（推荐用于订阅）
https://<你的域名>/?format=3&source=jingjian
```

### 完整版（full，默认）

```jsx
# 原始 JSON
https://<你的域名>/?format=0&source=full

# 带代理前缀的 JSON
https://<你的域名>/?format=1&source=full

# 原始 Base58 编码
https://<你的域名>/?format=2&source=full

# 代理 Base58 编码（推荐用于订阅）
https://<你的域名>/?format=3&source=full
```

---   

</details>

<details>
<summary>📌 注意事项</summary>
  
# 
  
- **Workers 免费额度**：每天 10 万次请求，适合轻量使用。超出后需升级付费套餐。
- **代理替换逻辑**：如果 JSON 中 `api` 字段已包含 `?url=` 前缀，会先去掉旧前缀，再加上新前缀。
- **Base58 输出**：适合直接作为订阅链接在支持该格式的客户端中使用。
- **配置源更新**：配置源来自 GitHub，内容会定期更新。Worker 会缓存 7200 秒（2小时）。
- **超时设置**：默认请求超时时间为 9 秒，超时后会返回错误信息。
- **CORS 支持**：已启用完整的 CORS 支持，可直接在前端应用中调用。

---   
  
</details>

<details>
<summary>🔧 高级配置</summary>
  
# 

### 修改配置源地址

在 `worker.js` 中找到 `JSON_SOURCES` 对象并修改：

```jsx
const JSON_SOURCES = {
  'jin18': 'https://raw.githubusercontent.com/your-repo/jin18.json',
  'jingjian': 'https://raw.githubusercontent.com/your-repo/jingjian.json',
  'full': 'https://raw.githubusercontent.com/your-repo/full.json'
}
```

### 修改超时时间

找到以下代码并修改超时毫秒数：

```jsx
const timeoutId = setTimeout(() => controller.abort(), 9000) // 改为其他值
```

### 添加访问日志

可以在代码中添加日志记录：

```jsx
console.log(`Request from: ${request.headers.get('cf-connecting-ip')}`)
```

</details>

---

## 🆕 更新内容

- 📄 **Luna-TV配置编辑器**：专业的 JSON 配置文件可视化编辑器。  
- 🔍 **自动检测API状态**：每 1 小时检测一次 API 可用性，并记录最近 100 次测试报告。  
- 🧩 **源名称前添加图标**：源名称前添加图标，方便区分。  
- 🌐 **被墙资源自动中转**：为受限 API 提供 CF Worker 中转能力。  
- 📄 **添加_comment参数**：为异常源添加_comment参数以方便维护,不影响正常使用!(2025.12.06)

---   

## 🧪 测试与示例

### ✅ 使用中转API测试
- 通过 CORSAPI 转发后，大幅提升视频源可用率。  
- 可“复活”原本无法访问的资源。  

### ⚙️ 精简版源更新
- 去除污染源与无搜索结果源（如 🎬虎牙、🔞丝袜、🔞色猫）。  
- 精简后共 **57 个可用源**，在中转代理下全部可访问。  
<details>
<summary>示例</summary>
<img width="1025" height="486" alt="61" src="https://github.com/user-attachments/assets/81c80108-7c03-4583-87ab-b7b57cdfd3bd" />
  
  
</details>

---   
  
# API 健康报告（每日自动检测API状态）

## API 状态（最近更新：2026-11-12 07:19 CST）

- 总 API 数量：168
- 成功 API 数量：109
- 失败 API 数量：59
- 平均可用率：68.8%
- 完美可用率（100%）：104 个
- 高可用率（80%-99%）：10 个
- 中等可用率（50%-79%）：3 个
- 低可用率（<50%）：51 个

<div style="font-size: 11px;">

<!-- API_TABLE_START -->
| 状态 | 资源名称 | 地址 | API | 搜索功能 | 成功次数 | 失败次数 | 成功率 | 最近7天趋势 |
|------|---------|-----|-----|---------|---------:|--------:|-------:|--------------|
| ✅ | 🎬360 资源 | [Link](https://360zy.com) | [Link](https://360zyzz.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬360资源 | [Link](https://360zy.com) | [Link](https://360zy.com/api.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬CK资源 | [Link](https://ckzy.me) | [Link](https://ckzy.me/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬iKun资源 | [Link](https://ikunzy.com) | [Link](https://ikunzyapi.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬New6V磁力 | [Link](https://www.xb6v.com) | [Link](https://www.xb6v.com) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬TV-乐子HTTP | [Link](http://cj.lziapi.com) | [Link](http://cj.lziapi.com/api.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬TV-优质资源库1080 | - | [Link](https://api.yzzy-api.com/inc/ldg_api_all.php/provide/vod) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬TV-光速HTTP | [Link](http://api.guangsuapi.com) | [Link](http://api.guangsuapi.com/api.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬TV-最大点播 | [Link](http://zuidazy.me) | [Link](http://zuidazy.me/api.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬TV-大地资源网络 | - | [Link](https://dadiapi.com/api.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬TV-天涯海角 | [Link](https://tyyszyapi.com) | [Link](https://tyyszyapi.com/api.php/provide/vod) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬TV-快车资源阿 | - | [Link](https://caiji.kuaichezy.org/api.php/provide) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬TV-新浪资源 | [Link](http://api.xinlangapi.com) | [Link](http://api.xinlangapi.com/xinlangapi.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬TV-无尽CC | - | [Link](https://api.wujinapi.cc/api.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬TV-无尽NET | - | [Link](https://api.wujinapi.net/api.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬TV-暴风APP | [Link](https://app.bfzyapi.com) | [Link](https://app.bfzyapi.com/api.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬TV-牛牛点播 | [Link](https://api.niuniuzy.me) | [Link](https://api.niuniuzy.me/api.php/provide/vod) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬TV-神马云 | [Link](https://api.1080zyku.com) | [Link](https://api.1080zyku.com/inc/apijson.php) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬TV-红牛资源 | - | [Link](https://www.hongniuzy3.com/api.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬TV-金鹰资源 | [Link](https://jyzyapi.com) | [Link](https://jyzyapi.com/api.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬TV-闪电资源 | [Link](https://sdzyapi.com) | [Link](https://sdzyapi.com/api.php/provide/vod) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬TV-非凡影视new | [Link](http://ffzy5.tv) | [Link](http://ffzy5.tv/api.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬TV-非凡采集 | [Link](http://cj.ffzyapi.com) | [Link](http://cj.ffzyapi.com/api.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬U酷影视 | [Link](https://www.ukuzy.com) | [Link](https://api.ukuapi88.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬最大资源 | zuida.xyz | [Link](https://api.zuidapi.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬剧圈APP | [Link](http://124.221.3.182:19987) | [Link](http://124.221.3.182:19987/app/bn) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬半日APP | [Link](http://103.217.190.91:19987) | [Link](http://103.217.190.91:19987/app/bn) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬卧龙资源 | [Link](https://wolongzyw.com) | [Link](https://wolongzyw.com/api.php/provide/vod) | ❌ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬卧龙资源1 | [Link](https://collect.wolongzyw.com) | [Link](https://collect.wolongzyw.com/api.php/provide/vod) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬厂长影视 | [Link](https://cz01.vip) | [Link](https://cz01.vip) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬天堂APP | [Link](https://dyttandroid04-1372779881.cos.ap-shanghai.myqcloud.com) | [Link](https://dyttandroid04-1372779881.cos.ap-shanghai.myqcloud.com/app_dyttandroid.txt) | 无结果 | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬天涯 | [Link](http://tyyszy.com) | [Link](http://tyyszy.com/api.php/provide/vod) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬如意资源 | [Link](https://www.ryzyw.com) | [Link](https://cj.rycjapi.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬小丑4K | [Link](https://4kxc.com) | [Link](https://4kxc.com) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬尤酷 | [Link](https://api.ukuapi.com) | [Link](https://api.ukuapi.com/api.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬布布APP | [Link](https://323433ssdfd.top) | [Link](https://323433ssdfd.top) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬建安 | [Link](http://154.219.117.232:9981) | [Link](http://154.219.117.232:9981/jacloudapi.php/provide/vod) | 不匹配 | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬指南4K | [Link](https://4kzn.cc) | [Link](https://4kzn.cc) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬无尽资源1 | [Link](https://wujinzy.com) | [Link](https://api.wujinapi.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬旺旺影视 | [Link](https://vip.wwgz.cn:5200) | [Link](https://vip.wwgz.cn:5200) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬旺旺短剧 | [Link](https://wwzy.tv) | [Link](https://wwzy.tv/api.php/provide/vod) | ❌ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬旺旺资源 | [Link](https://api.wwzy.tv) | [Link](https://api.wwzy.tv/api.php/provide/vod) | ❌ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬暴风资源 | [Link](https://bfzy.tv) | [Link](https://bfzyapi.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬极速资源 | [Link](https://jszyapi.com) | [Link](https://jszyapi.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬枫叶影视 | [Link](https://www.vip1949.com) | [Link](https://www.vip1949.com/) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬樱花资源 | [Link](https://yhzy.cc) | [Link](https://m3u8.apiyhzy.com/api.php/provide/vod) | ❌ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬王子APP | [Link](https://app.95112475.xyz) | [Link](https://app.95112475.xyz) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬电影天堂 | [Link](http://caiji.dyttzyapi.com) | [Link](http://caiji.dyttzyapi.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬番社动漫 | [Link](https://www.dora-video.cn) | [Link](https://www.dora-video.cn/search/sy/?niandai={year}&cat={class}&tag={cateId}&gaojijiansuo=1&zhuangtai={by}) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬种子4K | [Link](https://sidhub.cc) | [Link](https://sidhub.cc) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬红牛资源 | [Link](https://www.hongniuzy.com) | [Link](https://www.hongniuzy2.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬索尼资源 | [Link](https://suonizy.net) | [Link](https://suoniapi.com/api.php/provide/vod) | ❌ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬苹果APP | [Link](https://xpgandroid03-1372779881.cos.ap-beijing.myqcloud.com) | [Link](https://xpgandroid03-1372779881.cos.ap-beijing.myqcloud.com/app_xpg_android.txt) | 无结果 | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬茉莉APP | [Link](https://allinadmin.oss-cn-hangzhou.aliyuncs.com) | [Link](https://allinadmin.oss-cn-hangzhou.aliyuncs.com/bk/9.txt) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬蓝鸟APP | [Link](https://lanyingjisu.oss-cn-wuhan-lr.aliyuncs.com) | [Link](https://lanyingjisu.oss-cn-wuhan-lr.aliyuncs.com/lyjszx.txt) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬虎牙资源 | [Link](https://www.huyaapi.com) | [Link](https://www.huyaapi.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬蜡笔4K | [Link](https://www.fmcf.fun) | [Link](https://www.fmcf.fun) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬豪华资源 | [Link](https://www.haohuazy.com) | [Link](https://hhzyapi.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬迅雷吧磁力 | [Link](https://xunlei8.me) | [Link](https://xunlei8.me) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬速播资源 | www.subozy.com | [Link](https://subocaiji.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬量子资源 | [Link](https://cj.lzcaiji.com) | [Link](https://cj.lzcaiji.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬金鹰点播 | [Link](https://jinyingzy.com) | [Link](https://jinyingzy.com/api.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬闪电4K | [Link](http://shandian.blog) | [Link](http://shandian.blog) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬闪电资源 | [Link](https://shandianzy.com) | [Link](https://xsd.sdzyapi.com/api.php/provide/vod) | ❌ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬非凡资源 | [Link](https://cj.ffzyapi.com) | [Link](https://api.ffzyapi.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬马猴APP | [Link](https://45.150.167.18:8000) | [Link](https://45.150.167.18:8000) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🎬鸭鸭资源 | [Link](https://yayazy3.com) | [Link](https://cj.yayazy.net/api.php/provide/vod) | ❌ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞155资源 | [Link](https://155zy2.com) | [Link](https://155api.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞91-精品- | [Link](https://91jpzyw.com) | [Link](https://91jpzyw.com/api.php/provide/vod) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞91麻豆 | [Link](https://91md.me) | [Link](https://91md.me/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞AV-CK | [Link](https://www.ckzy1.com) | [Link](https://www.ckzy1.com/api.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞AV-森林资源 | [Link](https://slapibf.com) | [Link](https://slapibf.com/api.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞AV-淫水机资源站 | [Link](https://www.xrbsp.com) | [Link](https://www.xrbsp.com/api/json.php) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞AV-玉兔-2 | [Link](https://yutuzy10.com) | [Link](https://yutuzy10.com/api.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞AV-香奶儿资源站 | [Link](https://www.gdlsp.com) | [Link](https://www.gdlsp.com/api/json.php) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞AV-黄色仓库 | [Link](https://hsckzy.vip) | [Link](https://hsckzy.vip/api.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞AV-黄色资源啊啊 | - | [Link](https://hsckzy888.com/api.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞AV-黑木耳 | [Link](https://json.heimuer.xyz) | [Link](https://json.heimuer.xyz/api.php/provide/vod) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞AV-黑木耳点播 | [Link](https://json02.heimuer.xyz) | [Link](https://json02.heimuer.xyz/api.php/provide/vod) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞jkun资源 | [Link](https://jkunzyapi.com) | [Link](https://jkunzyapi.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞souavZY | [Link](https://api.souavzy.vip) | [Link](https://api.souavzy.vip/api.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞souavZY | [Link](https://api.souavzyw.net) | [Link](https://api.souavzyw.net/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞乐播资源 | [Link](https://lbapi9.com) | [Link](https://lbapi9.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞奥斯卡 | [Link](https://aosikazy.com) | [Link](https://aosikazy.com/api.php/provide/vod) | ❌ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞奶香资源 | [Link](https://Naixxzy.com) | [Link](https://Naixxzy.com/api.php/provide/vod) | ❌ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞小鸡资源 | [Link](https://xiaojizy.live) | [Link](https://api.xiaojizy.live/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞杏吧资源 | [Link](https://xingba111.com) | [Link](https://xingba111.com/api.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞杏吧资源 | [Link](https://xingba111.com) | [Link](https://xingba222.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞桃花资源 | [Link](https://thzy8.me) | [Link](https://thzy1.me/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞森林资源 | [Link](https://slapibf.com) | [Link](https://beiyong.slapibf.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞滴滴资源 | [Link](https://didizy.com) | [Link](https://api.ddapi.cc/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞玉兔资源 | [Link](https://apiyutu.com) | [Link](https://apiyutu.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞番号资源 | [Link](http://fhapi9.com) | [Link](http://fhapi9.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞白嫖资源 | [Link](https://www.kxgav.com) | [Link](https://www.kxgav.com/api/json.php) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞精品资源 | [Link](https://www.jingpinx.com) | [Link](https://www.jingpinx.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞美少女 | [Link](https://www.msnii.com) | [Link](https://www.msnii.com/api/json.php) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞老色逼 | [Link](https://apilsbzy1.com) | [Link](https://apilsbzy1.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞色猫资源 | [Link](https://semaozy1.com) | [Link](https://caiji.semaozy.net/inc/apijson_vod.php/provide/vod) | 无结果 | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞豆豆资源 | [Link](https://doudouzy.com) | [Link](https://api.douapi.cc/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞黄AVZY | [Link](https://www.pgxdy.com) | [Link](https://www.pgxdy.com/api/json.php) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞黄色仓库 | hsckzy.xyz | [Link](https://hsckzy.xyz/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞黑料资源 | [Link](https://heiliaozy.cc) | [Link](https://www.heiliaozyapi.com/api.php/provide/vod) | ✅ | 30 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 无尽资源 | - | [Link](http://api.wujinapi.me/api.php/provide/vod) | ✅ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ✅ | 猫眼资源 | - | [Link](https://api.maoyanapi.top) | ❌ | 7 | 0 | 100.0% | ✅✅✅✅✅✅✅ |
| ❌ | 🎬爱奇艺 | [Link](https://iqiyizyapi.com) | [Link](https://iqiyizyapi.com/api.php/provide/vod) | ❌ | 29 | 1 | 96.7% | ✅✅✅✅✅✅❌ |
| ❌ | 🎬魔都动漫 | [Link](https://caiji.moduapi.cc) | [Link](https://caiji.moduapi.cc/api.php/provide/vod) | ❌ | 29 | 1 | 96.7% | ✅✅✅✅✅✅❌ |
| ❌ | 🎬魔都资源 | [Link](https://www.moduzy.net) | [Link](https://www.mdzyapi.com/api.php/provide/vod) | ❌ | 29 | 1 | 96.7% | ✅✅✅✅✅✅❌ |
| ✅ | 🔞大奶子 | [Link](https://apidanaizi.com) | [Link](https://apidanaizi.com/api.php/provide/vod) | ✅ | 29 | 1 | 96.7% | ✅✅✅✅✅✅✅ |
| ✅ | 🔞鲨鱼资源 | [Link](https://shayuapi.com) | [Link](https://shayuapi.com/api.php/provide/vod) | ✅ | 29 | 1 | 96.7% | ✅✅✅✅✅✅✅ |
| ❌ | 🎬TV-iqiyi资源 | - | [Link](https://www.iqiyizyapi.com/api.php/provide/vod) | ❌ | 6 | 1 | 85.7% | ✅✅✅✅✅✅❌ |
| ✅ | 🎬TV-非凡线路 | [Link](http://ffzy1.tv) | [Link](http://ffzy1.tv/api.php/provide/vod) | ✅ | 6 | 1 | 85.7% | ✅✅✅✅✅❌✅ |
| ❌ | 🎬TV-魔都影视 | [Link](https://www.moduzy.com) | [Link](https://www.moduzy.com/api.php/provide/vod) | ❌ | 6 | 1 | 85.7% | ✅✅✅✅✅✅❌ |
| ✅ | 🎬非凡 | [Link](http://ffzy.tv) | [Link](http://ffzy.tv/api.php/provide/vod) | ✅ | 6 | 1 | 85.7% | ✅✅✅✅✅❌✅ |
| 🚨 | 🎬茅台资源 | [Link](https://mtzy.me) | [Link](https://caiji.maotaizy.cc/api.php/provide/vod) | ❌ | 25 | 5 | 83.3% | ✅✅❌❌❌❌❌ |
| ✅ | 🎬华谊APP | [Link](https://1851089669.cdn.123clouddisk.com) | [Link](https://1851089669.cdn.123clouddisk.com/1851089669/44107727) | 无结果 | 5 | 2 | 71.4% | ✅✅❌✅✅❌✅ |
| ❌ | 🎬橘汁APP | [Link](https://123-1349250429.cos.ap-shanghai.myqcloud.com) | [Link](https://123-1349250429.cos.ap-shanghai.myqcloud.com/app.txt) | ❌ | 5 | 2 | 71.4% | ✅✅✅✅✅❌❌ |
| 🚨 | 🔞AV-辣椒资源黄黄 | - | [Link](https://apilj.com/api.php/provide) | ❌ | 4 | 3 | 57.1% | ✅✅✅✅❌❌❌ |
| 🚨 | 🎬豆瓣资源 | dbzy.tv | [Link](https://caiji.dbzy5.com/api.php/provide/vod) | ❌ | 13 | 17 | 43.3% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬TV-七七影视 | - | [Link](https://www.qiqidys.com/api.php/provide/vod/) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬TV-华为吧资源 | - | [Link](https://huawei8.live/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬TV-卧龙CC | - | [Link](https://collect.wolongzy.cc/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬TV-快播资源网站 | - | [Link](https://gayapi.com/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬TV-步步高资源 | [Link](https://api.yparse.com) | [Link](https://api.yparse.com/api/json) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬TV-淘片资源 | - | [Link](https://taopianapi.com/cjapi/sda/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬TV-爱短剧.cc | - | [Link](https://www.aiduanju.cc/) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬TV-蜂巢片库 | - | [Link](https://api.fczy888.me/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬TV-豆瓣资源-2 | [Link](https://caiji.dbzy.tv) | [Link](https://caiji.dbzy.tv/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬TV-金马资源网 | - | [Link](https://api.jmzy.com/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬TV-魔爪资源 | [Link](https://mozhuazy.com) | [Link](https://mozhuazy.com/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬U酷88 | [Link](https://api.ukuapi88.com) | [Link](https://jjpz.hafrey.dpdns.org/?url=https://api.ukuapi88.com/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬八零4K | [Link](https://woog.nxog.eu.org) | [Link](https://woog.nxog.eu.org) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬哔哩合集 | [Link](http://127.0.0.1:9978) | [Link](http://127.0.0.1:9978/file/TVBox/bili_cookie.txt) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬堇夏听书 | [Link](https://m.ting15.com) | [Link](https://m.ting15.com) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬多多4K | [Link](https://tv.yydsys.top) | [Link](https://tv.yydsys.top) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬小猫咪 | [Link](http://zy.xmm.hk) | [Link](https://zy.xmm.hk/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬小绵阳 | [Link](https://vs.okcdn100.top) | [Link](https://vs.okcdn100.top/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬山海资源 | [Link](https://zy.sh0o.cn) | [Link](https://zy.sh0o.cn/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬快映4K | [Link](http://xsayang.fun) | [Link](http://xsayang.fun) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬木偶4K | [Link](https://123.666291.xyz) | [Link](https://123.666291.xyz) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬果果短剧 | [Link](https://www.mochadj.com) | [Link](https://www.mochadj.com/i/{cateId}-{catePg}.html) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬热播APP | [Link](http://v.rbotv.cn) | [Link](http://v.rbotv.cn) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬玩偶4K | [Link](https://www.wogg.live) | [Link](https://www.wogg.live) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬百度云zy | [Link](https://bdzy1.com) | [Link](https://pz.v88.qzz.io/?url=https://api.apibdzy.com/api.php/provide/vod) | ❌ | 0 | 30 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬艾旦影视 | [Link](https://lovedan.net) | [Link](https://lovedan.net/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬花卷4K | [Link](https://www.hjzhencai.top) | [Link](https://www.hjzhencai.top) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬茉莉4K | [Link](https://www.hdmoli.com) | [Link](https://www.hdmoli.com) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬荐片磁力 | [Link](https://www.whhyn.com) | [Link](https://www.whhyn.com) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬蓝鹰APP | [Link](http://103.217.190.91:5566) | [Link](http://103.217.190.91:5566) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬虎斑4K | [Link](http://xhban.xyz) | [Link](http://xhban.xyz) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬金牌影视 | [Link](https://y2s52n7.com,https:) | [Link](https://y2s52n7.com,https://m.hkybqufgh.com,https://m.sizhengxt.com,https://m.9zhoukj.com,https://m.sizhengxt.com,https://m.jiabaide.cn) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬金蝉影视 | [Link](https://zy.jinchancaiji.com) | [Link](https://zy.jinchancaiji.com/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬面包影视 | [Link](https://v.aiwule.com) | [Link](https://v.aiwule.com/vodshow/{cateId}-{area}-{by}-{class}-{lang}-{letter}---{catePg}---{year}.html) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬飘零资源 | [Link](https://p2100.net) | [Link](https://p2100.net/api.php/provide/vod) | ❌ | 0 | 30 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬飞宇影院 | [Link](http://ntfeiyu.com) | [Link](http://ntfeiyu.com/nt/{cateId}/area/{area}/by/{by}/class/{class}/lang/{lang}/page/{catePg}/year/{year}.html) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🎬骚火影视 | [Link](https://shdy5.us) | [Link](https://shdy5.us) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🔞AIvin | [Link](http://lbapiby.com) | [Link](http://lbapiby.com/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🔞AV-色猫资源 | [Link](https://api.maozyapi.com) | [Link](https://api.maozyapi.com/inc/apijson_vod.php) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🔞丝袜资源 | [Link](https://siwazyw.tv) | [Link](https://siwazyw.tv/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🔞优优资源 | [Link](https://www.yyzywcj.com) | [Link](https://www.yyzywcj.com/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🔞最色资源 | [Link](https://zuisezy.com) | [Link](https://api.zuiseapi.com/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🔞幸资源 | [Link](https://xzytv.com) | [Link](https://xzybb2.com/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🔞杏吧资源 | [Link](https://xingba111.com) | [Link](https://pz.168188.dpdns.org/?url=https://xingba222.com/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🔞百万资源 | [Link](https://api.bwzym3u8.com) | [Link](https://api.bwzyz.com/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🔞细胞资源 | [Link](https://www.xxibaozyw.com) | [Link](https://www.xxibaozyw.com/api.php/provide/vod) | ❌ | 0 | 30 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🔞色南国 | [Link](https://api.sexnguon.com) | [Link](https://api.sexnguon.com/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 🔞香蕉资源 | [Link](https://www.xiangjiaozyw.com) | [Link](https://www.xiangjiaozyw.com/api.php/provide/vod) | ❌ | 0 | 30 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 百度资源 | [Link](https://api.apibdzy.com) | [Link](https://api.apibdzy.com/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
| 🚨 | 豆瓣资源 | [Link](https://dbzy.tv) | [Link](https://dbzy.tv/api.php/provide/vod) | ❌ | 0 | 7 | 0.0% | ❌❌❌❌❌❌❌ |
<!-- API_TABLE_END -->

---

# 免责声明

> **在使用本仓库前，请务必仔细阅读本声明。**
> 任何以任何形式访问、使用、复制、修改或分发本仓库内容的行为，均视为已阅读并同意本免责声明的全部条款。

---

## 一、定义与范围

* **本仓库**：指本 GitHub 仓库及其直接或间接相关的其他仓库。
* **维护者**：指本仓库的管理员、维护者及任何参与内容整理与分享的人员。
* **仓库内容**：指本仓库中提供的全部配置文件、源定义、代码片段、文档说明及引用的外部资源信息。

---

## 二、仓库用途说明（MoonTV / LunaTV 源配置）

1. 本仓库主要提供 **MoonTV / LunaTV 等相关项目的源配置、订阅定义或配置示例**，内容均整理自互联网公开信息。
2. 本仓库内容 **仅用于学习、测试与技术研究目的**，包括但不限于配置格式研究、源聚合方式分析及客户端兼容性测试。
3. **本仓库不存储、不托管、不分发任何音视频文件、媒体流或受版权保护的内容**，亦不提供任何形式的媒体服务。
4. 除非另有明确书面声明，本仓库 **不授予任何商业使用许可**。
5. 严禁将本仓库内容用于任何违反法律法规、版权规则或所在司法辖区政策的用途。

---

## 三、无任何担保声明

本仓库及其内容均以 **“现状（AS IS）”** 方式提供，维护者不作出任何形式的明示或暗示担保，包括但不限于：

* 合法性
* 准确性
* 完整性
* 可用性
* 适用于特定目的

使用本仓库内容所产生的一切风险均由使用者自行承担。

---

## 四、责任限制

1. 因使用、误用、修改或分发本仓库内容而导致的任何直接或间接损失，包括但不限于数据丢失、系统故障、服务中断、法律风险等，维护者概不负责。
2. 用户在使用本仓库内容过程中，如违反其所在国家或地区的法律法规，所产生的一切法律责任均由用户自行承担，与本仓库及维护者无关。

---

## 五、第三方软件与项目声明

1. MoonTV、LunaTV 及任何在本仓库中提及的第三方软件、硬件、服务或项目，均 **与本仓库不存在任何隶属、合作、授权或背书关系**。
2. 本仓库不对任何第三方软件或服务的功能、合法性或可用性作出保证。
3. 因使用第三方软件或服务所产生的一切后果，均由使用者自行承担。

---

## 六、转载与分发限制

1. 未经维护者明确授权，**禁止以任何形式在其他平台、网站、公众号、自媒体或镜像站点转载、发布或再分发本仓库内容**。
2. 允许在 GitHub 平台内出于学习和研究目的进行 fork，但须保留本免责声明且不得改变仓库性质或用途。
3. 通过正常开发工具获取的域名、地址或配置信息，且未涉及逆向工程或网络攻击行为的，不构成对计算机系统的非法侵入。

---

## 七、知识产权与侵权处理

1. 若任何单位或个人认为本仓库内容可能侵犯其合法权益，请及时联系维护者，并提供有效的身份证明及权属证明材料。
2. 在核实相关材料后，维护者将依法依规尽快删除或处理相关内容。

---

## 八、使用期限与删除建议

1. 本仓库内容仅供 **临时学习与研究参考**。
2. 任何关于使用时限（如 24 小时）的表述，均属于风险提示性质，并非强制性法律义务（法律另有规定的除外）。
3. 建议用户在完成学习或研究后，及时删除本仓库内容的本地副本。
4. 如对相关功能存在长期或生产环境需求，请自行独立开发实现。

---

## 九、司法辖区提示

1. 本仓库内容 **不建议在中国大陆地区使用**，尤其是在相关应用或配置可能违反当地法律法规的情形下。
2. 用户应自行评估并承担因使用本仓库内容所带来的合规与法律风险。

---

## 十、免责声明的修改与接受

1. 维护者保留在不另行通知的情况下，随时修改或补充本免责声明的权利。
2. 任何对本仓库内容的访问、使用、复制、修改或分发行为，均视为已充分阅读并接受本免责声明的全部内容。



**若您不同意本免责声明中的任何条款，请立即停止使用并删除本仓库的全部内容。**


---



## ⭐ Star History
[![Star History](https://starchart.cc/hafrey1/LunaTV-config.svg?variant=light)](https://starchart.cc/hafrey1/LunaTV-config)














































































































































































































