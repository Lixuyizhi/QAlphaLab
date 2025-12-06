# Qlib量化投资研究平台

Qlib是一个由微软开发的开源量化投资研究平台，专注于中国A股市场的量化策略开发、回测与分析。本项目基于Qlib进行了扩展和定制，提供了更丰富的量化研究工具和策略实现。

## 项目简介

本项目旨在为量化投资者和研究者提供一个完整的量化研究框架，包括：

- 数据获取与管理
- 特征工程与因子开发
- 机器学习模型训练
- 策略回测与优化
- 性能分析与可视化

## 项目结构

```text

├── .conda/                 # 虚拟环境目录
├── .gitignore              # Git忽略文件配置
├── branch_research.ipynb   # 分支研究示例
├── get_SQL_data.ipynb      # SQL数据获取示例
├── logs/                   # 回测日志和结果
│   ├── allAshare_*/        # 全A股票相关策略日志
│   ├── hushen300_*/        # 沪深300相关策略日志
│   ├── shangzheng50_*/     # 上证50相关策略日志
│   ├── zhongzheng1000_*/   # 中证1000相关策略日志
│   └── zhongzheng500_*/    # 中证500相关策略日志
├── official_example_code/  # 官方示例代码
│   ├── configuration.yaml  # 配置文件
│   ├── learn_Qlib_notebook.ipynb  # Qlib学习笔记
│   ├── multiindex_learning.ipynb  # 多重索引学习
│   └── official_example_code.ipynb  # 官方示例代码
├── requirements.txt        # 项目依赖配置
├── transform_csv_to_bin.ipynb  # CSV转二进制格式工具
├── weightStrategy_backtest_Fixed_period_Multi_group_Rebalancing.ipynb  # 固定周期多组权重策略回测
├── weightStrategy_backtest_Quarterly_Multi_group_Rebalancing.ipynb     # 季度多组权重策略回测
├── weightStrategy_backtest_Quarterly_single_group_rebalancing.ipynb    # 季度单组权重策略回测
└── 待改进问题.ipynb        # 待改进问题记录
```

### 主要目录说明

- **.conda/**: 项目虚拟环境目录
- **logs/**: 保存回测结果和日志，按不同策略和指数分类
- **official_example_code/**: 包含官方提供的示例代码和教程
- **requirements.txt**: 项目依赖配置文件，包含所有必需的Python库

## 核心功能

### 1. 数据管理

- 支持多种数据源(股票、指数、基金等)
- 提供数据获取、清洗、存储一体化解决方案
- 支持CSV和Qlib二进制格式数据

### 2. 特征工程

- 内置多种经典量化因子(如Alpha158)
- 支持自定义因子开发
- 提供因子分析和评价工具

### 3. 模型训练*（暂不支持）

- 支持多种机器学习模型(LightGBM等)
- 提供模型调参和优化工具
- 支持模型保存和加载

### 4. 策略回测

- 完整的回测框架，支持自定义策略
- 支持日频和分钟级回测
- 提供详细的回测报告和性能指标

### 5. 性能分析

- 生成收益曲线、回撤曲线等可视化图表
- 计算夏普比率、信息比率等风险指标
- 支持多策略对比分析

## 安装和设置

### 环境要求

- Python 3.11+
- Windows/Linux/macOS
- 推荐使用Anaconda环境

### 安装步骤

1. 克隆或下载本项目到本地
2. 创建并激活虚拟环境（可选但推荐）

   ```bash
   conda create -n qlib_env python=3.11 -y
   conda activate qlib_env
   ```

3. 安装所有依赖

   ```bash
   pip install -r requirements.txt
   ```

   注：requirements.txt已包含pyqlib和其他所有必需的依赖库

4. 数据准备

   项目支持通过`get_SQL_data.ipynb`获取SQL数据并转换成因子数据，通过`transform_csv_to_bin.ipynb`将CSV格式数据转换为Qlib二进制格式（主要是价格数据）

## 快速开始

### 1. 导入必要的库

```python
# 1. 导入必要的库
import qlib
from qlib.constant import REG_CN
import logging
import os
import pandas as pd
```

### 2. 初始化Qlib

```python
# 初始化Qlib
provider_uri = "./.qlib/qlib_data/allAShare_with_indexValue"
qlib.init(provider_uri=provider_uri, region=REG_CN)
```

## 使用示例

本项目已构建多种策略和工具帮助用户快速上手：

### 数据处理工具

- **get_SQL_data.ipynb**: SQL数据获取和处理示例
- **transform_csv_to_bin.ipynb**: CSV格式数据转换为Qlib二进制格式工具

### 回测策略

- **weightStrategy_backtest_Fixed_period_Multi_group_Rebalancing.ipynb**: 固定周期多组权重策略回测
- **weightStrategy_backtest_Quarterly_Multi_group_Rebalancing.ipynb**: 季度多组权重策略回测
- **weightStrategy_backtest_Quarterly_single_group_rebalancing.ipynb**: 季度单组权重策略回测

### 研究示例

- **branch_research.ipynb**: 分支研究示例
- **官方示例代码**:
  - **official_example_code/official_example_code.ipynb**: 官方示例代码，包含完整的Qlib工作流
  - **official_example_code/learn_Qlib_notebook.ipynb**: Qlib学习笔记，详细介绍Qlib的使用方法
  - **official_example_code/multiindex_learning.ipynb**: 多重索引学习示例

### 问题记录

- **待改进问题.ipynb**: 项目待改进问题记录和跟踪

## 配置说明

### 数据配置

数据存储在`.qlib/`目录下，可以通过以下方式配置：

```python
# 设置数据路径
provider_uri = "./.qlib/qlib_data/allAShare_with_indexValue"
# 初始化Qlib
qlib.init(provider_uri=provider_uri, region=REG_CN)
```

### 策略配置

在回测文件（如`weightStrategy_backtest_Quarterly_Multi_group_Rebalancing.ipynb`）中，您可以通过以下配置进行分组回测：

```python
strategy_config = {
    "topk": 20,                    # 选择前20只股票
    "start_percent": param_dict[i][0],  # 分组起始百分比
    "end_percent": param_dict[i][1],    # 分组结束百分比
    "signal": signal_obj,          # 使用信号对象而不是原始数据
    "rebalance_day": 20,           # 再平衡周期（天）
    "risk_degree": 1,              # 风险度设置
}
```

其中`param_dict`定义了不同分组的百分比范围，用于实现多组回测。

## 日志和结果

回测日志和结果存储在`logs/`目录下，按不同策略和指数分类：

- **hushen300_*/**: 沪深300相关策略日志
- **shangzheng50_*/**: 上证50相关策略日志
- **zhongzheng500_*/**: 中证500相关策略日志
- **zhongzheng1000_*/**: 中证1000相关策略日志
- **allAshare_*/**: 全A股票相关策略日志

每个策略目录包含：

- 回测报告
- 持仓明细
- 收益曲线
- 风险指标

## 自定义策略

用户可以通过继承`BaseStrategy`类来自定义策略：

```python
from qlib.strategy import BaseStrategy

class MyStrategy(BaseStrategy):
    def __init__(self, topk=20, **kwargs):
        super().__init__(**kwargs)
        self.topk = topk
    
    def generate_order_list(self, score, risk_degree=0.95):
        # 实现自定义策略逻辑
        # ...
        return order_list
```
