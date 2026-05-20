# 🏗️ 智能暖通空调设计系统

> 基于 MiMo V2.5 构建的暖通空调设计辅助平台

[![Python](https://img.shields.io/badge/Python-3.11+-blue.svg)](https://python.org)
[![React](https://img.shields.io/badge/React-18-61DAFB.svg)](https://reactjs.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.110-009688.svg)](https://fastapi.tiangolo.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![MiMo](https://img.shields.io/badge/MiMo-V2.5-FF6900.svg)](https://platform.xiaomimimo.com)

## ✨ 功能特性

- 🔥 **负荷计算** — 基于围护结构传热理论的冷热负荷计算
- 🔧 **设备选型** — 智能匹配热泵机组、末端设备
- 📊 **方案比选** — 多方案技术经济对比分析
- 📝 **报告生成** — MiMo V2.5 自动生成设计文档
- 🌐 **Web 界面** — React 可视化操作界面

## 🏛️ 系统架构

```
┌─────────────────────────────────────────────┐
│              React Frontend                  │
│  ┌──────┐ ┌──────┐ ┌──────┐ ┌──────────┐   │
│  │负荷  │ │设备  │ │方案  │ │ 报告     │   │
│  │计算  │ │选型  │ │比选  │ │ 生成     │   │
│  └──┬───┘ └──┬───┘ └──┬───┘ └────┬─────┘   │
└─────┼────────┼────────┼──────────┼──────────┘
      │        │        │          │
      ▼        ▼        ▼          ▼
┌─────────────────────────────────────────────┐
│           FastAPI Backend                    │
│  ┌────────┐ ┌────────┐ ┌──────────────────┐ │
│  │负荷计算│ │设备库  │ │ MiMo API Client  │ │
│  │Engine  │ │Selector│ │ (报告/审查/问答) │ │
│  └────────┘ └────────┘ └──────────────────┘ │
└─────────────────────────────────────────────┘
```

## 🚀 快速开始

### 环境要求
- Python 3.11+
- Node.js 18+
- MiMo API Key（[申请地址](https://platform.xiaomimimo.com)）

### 后端启动

```bash
cd backend
pip install -r requirements.txt
export MIMO_API_KEY="your-api-key"
uvicorn main:app --reload --port 8000
```

### 前端启动

```bash
cd frontend
npm install
npm run dev
```

访问 http://localhost:5173

### Docker 启动

```bash
docker-compose up -d
```

## 📡 API 文档

| 端点 | 方法 | 说明 |
|------|------|------|
| `/api/calculate/load` | POST | 冷热负荷计算 |
| `/api/equipment/select` | POST | 设备选型 |
| `/api/compare/schemes` | POST | 方案比选 |
| `/api/generate/report` | POST | 生成设计报告 |
| `/api/health` | GET | 健康检查 |

### 负荷计算示例

```bash
curl -X POST http://localhost:8000/api/calculate/load \
  -H "Content-Type: application/json" \
  -d '{
    "city": "北京",
    "building_type": "办公",
    "area": 500,
    "floor_height": 3.6,
    "wall_type": "加气混凝土",
    "window_type": "双层中空玻璃",
    "window_ratio": 0.35
  }'
```

## 🔧 技术栈

| 层级 | 技术 |
|------|------|
| 前端 | React 18 + TypeScript + Vite + Tailwind CSS |
| 后端 | Python 3.11 + FastAPI + Pydantic |
| AI | MiMo V2.5 Pro（报告生成）+ MiMo V2.5 Vision（图纸识别）|
| 部署 | Docker + Docker Compose |

## 📐 计算原理

基于《民用建筑供暖通风与空气调节设计规范》(GB 50736)，采用稳态传热方法：

- **围护结构传热**: Q₁ = K × A × (t_w - t_n)
- **新风负荷**: Q₂ = G × ρ × (h_w - h_n)
- **内部得热**: Q₃ = 人员 + 照明 + 设备
- **总负荷**: Q = Q₁ + Q₂ + Q₃ × 修正系数

## 📄 License

MIT License
