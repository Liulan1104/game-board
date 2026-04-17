# 🎮 游戏行业看板 - 在线版

每日自动更新的游戏行业热点看板，支持 **日期回溯** 和 **产品筛选**，数据自动存储365天，超期自动清理。

---

## ✨ 功能特性

| 功能 | 说明 |
|------|------|
| 📰 每日热点 | 自动抓取 B站/微博/知乎 等平台热搜 |
| 📅 日历视图 | 月历展示游戏公测/上线时间 |
| 🔍 分类筛选 | 手游 / 端游 / 电竞 / 行业 / IP |
| 🎯 产品筛选 | 按具体产品（如"原神""崩坏星穹铁道"）筛选 |
| 📆 日期回溯 | 键盘 ← → 或日期控件切换任意天 |
| 🗑️ 自动清理 | 超过365天的数据自动删除 |

---

## 🚀 部署（3分钟完成）

### 方案一：Netlify + GitHub（推荐·自动更新）

#### 第1步：创建 GitHub 仓库

1. 打开 [github.com/new](https://github.com/new)
2. 仓库名填写 `game-industry-board`
3. 选择 **Private**（避免数据暴露）
4. 点击 **Create repository**

#### 第2步：上传项目文件

在终端运行：

```bash
cd /Users/elainesmacbook/WorkBuddy/20260416181029/在线看板项目

# 初始化 git（如果尚未初始化）
git init
git add .
git commit -m "Initial commit"

# 关联你的 GitHub 仓库（把 YOUR_USERNAME 换成你的 GitHub 用户名）
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/game-industry-board.git
git push -u origin main
```

#### 第3步：配置 Netlify 自动部署

1. 打开 [app.netlify.com](https://app.netlify.com)
2. 点击 **Add new site** → **Import an existing project**
3. 选择 **GitHub**，授权 Netlify 访问你的仓库
4. 配置构建：
   - **Build command**: （留空）
   - **Publish directory**: `.`
5. 点击 **Deploy site**

#### 第4步：开启 GitHub Actions 自动更新

1. 在 GitHub 仓库 → **Settings** → **Secrets** → **Actions**
2. 点击 **New repository secret**，名称填 `NETLIFY_AUTH_TOKEN`，值填你的 Netlify Personal Access Token（[到这里生成](https://app.netlify.com/user/applications))

> 💡 **每日自动运行**：GitHub Actions 每天北京时间 9:00 自动抓取当天数据并推送到仓库，Netlify 自动检测到更新并重新部署网站。

---

### 方案二：纯 Netlify Drop（无需 GitHub）

适合快速预览，不支持自动更新：

1. 打开 [app.netlify.com/drop](https://app.netlify.com/drop)
2. 直接拖入 `在线看板项目` 文件夹
3. 获得永久在线链接 ✅

> 数据更新时：修改 `data/daily/YYYY-MM-DD.json` 后重新拖入即可

---

## 📂 数据文件结构

```
项目目录/
├── index.html                    # 主看板页面
├── netlify.toml                  # Netlify 配置
├── .github/
│   └── workflows/
│       └── daily-update.yml      # 每日自动抓取脚本
├── data/
│   └── daily/
│       ├── 2026-04-11.json      # 每日数据（YYYY-MM-DD格式）
│       ├── 2026-04-12.json
│       └── ...
```

### 每日 JSON 文件格式

```json
{
  "date": "2026-04-17",
  "dayLabel": "4月17日（周五）",
  "news": [
    {
      "rank": 1,
      "cat": "手游",
      "products": ["原神", "崩坏星穹铁道"],
      "title": "《崩坏：星穹铁道》LAND嘉年华门票1分钟售罄",
      "source": "微博/B站",
      "company": "米哈游",
      "hot": "1分钟售罄",
      "detail": "完整摘要内容..."
    }
  ],
  "games": [
    {
      "date": "2026-04-17",
      "name": "王者荣耀世界",
      "company": "腾讯天美",
      "platform": "iOS/Android/PC",
      "rank": "S",
      "type": "开放世界MMOARPG",
      "publisher": "腾讯",
      "note": "年度最重磅手游 · 今日上线",
      "category": "mobile"
    }
  ]
}
```

---

## ⌨️ 快捷键

| 快捷键 | 功能 |
|--------|------|
| `←` | 前一天 |
| `→` | 后一天 |
| `Esc` | 关闭弹窗 |

---

## 🔧 手动维护（游戏日历）

游戏上线日历（`games` 字段）需要手动维护，建议：

1. 每周一更新当周重点游戏上线计划
2. 在 `data/daily/YYYY-MM-DD.json` 中添加 `games` 数组
3. 提交后 GitHub Actions 自动触发部署

---

## 📊 数据源

- **B站热搜**：API 抓取游戏区排行
- **微博热搜**：实时热搜游戏相关内容
- **知乎热榜**：游戏行业相关讨论
- **游戏日历**：手动维护重点游戏上线计划

---

## ❓ 常见问题

**Q: 数据最多存多久？**
A: GitHub Actions 每天自动清理超过365天的数据。

**Q: 如何修改抓取逻辑？**
A: 编辑 `.github/workflows/daily-update.yml`，里面有详细的爬虫代码注释。

**Q: 想添加更多游戏到日历？**
A: 直接编辑 `data/daily/YYYY-MM-DD.json`，在 `games` 数组中添加条目即可。

**Q: GitHub Actions 需要付费吗？**
A: 免费！GitHub 提供每月2000分钟免费 Actions 时长，每日运行绰绰有余。
