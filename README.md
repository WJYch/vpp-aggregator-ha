# ⚡ 虚拟电厂聚合平台 · HA 版

面向商业建筑（源宿酒店）的虚拟电厂聚合平台，部署于 Home Assistant，通过 GitHub Pages 展示。

## 功能

- **📊 总览监测** — 总负荷曲线、峰值标注、可调容量、光伏出力
- **🔌 负荷分解** — 空调/照明/蔚来换电站/中石油充电桩/空气源热泵分项堆叠图
- **📡 可调资源** — 5项可调负荷（蔚来/中石油/热泵/空调/光伏）能力清单+实时曲线
- **💰 分成计算** — 三方（业主/负荷方/运营方）分成公式+交互计算器

## 数据

当前使用模拟数据（15分钟粒度），基于源宿酒店可研报告年用电量600万度反推生成。

分项：
| 分项 | 年用电量 | 占比 |
|------|---------|------|
| 水冷空调 | 150万度 | 25% |
| 照明/插座/房间(含空气源热泵) | 150万度 | 25% |
| 蔚来换电站 | 200万度 | 33% |
| 中石油充电桩 | 100万度 | 17% |

## 部署

```bash
# 1. 生成模拟数据（可选，已有mock_data.json）
python3 generate_mock_data.py

# 2. 推送到 GitHub Pages
git add .
git commit -m "init: VPP聚合平台"
git remote add origin https://github.com/wjych/vpp-aggregator-ha.git
git push -u origin main

# 3. 在 GitHub 仓库 Settings > Pages 启用部署
```

## HA 集成

在 HA Lovelace 中添加 iframe 卡片：

```yaml
type: iframe
url: https://wjych.github.io/vpp-aggregator-ha/
aspect_ratio: 16:9
```

## 技术栈

- 纯前端 SPA（单页HTML + CSS + JS）
- Chart.js 可视化
- GitHub Pages 部署
- mock_data.json 定时更新（通过 NAS cron + fetch 脚本）
