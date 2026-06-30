# CSDN技术博客AI领域文章多维数据挖掘分析

## 项目简介

本项目通过网络爬虫从CSDN搜索API采集 **5821篇** 涵盖机器学习、大模型、深度学习、自然语言处理、数据挖掘、ChatGPT、AIGC、强化学习、计算机视觉、Transformer、卷积神经网络共11个关键词的技术博客文章数据，采用10种数据挖掘方法进行全面分析。

数据时间跨度：2015-2026年

## 文件说明

| 文件 | 说明 |
|------|------|
| `CSDN_AI数据挖掘分析报告.docx` | 完整Word报告（按学术模板格式） |
| `CSDN_AI数据挖掘分析.ipynb` | Jupyter Notebook（全部分析代码） |
| `csdn_ml_articles_5821.csv` | 原始数据集（5821篇，14个字段） |
| `figures/` | 全部22张可视化图表（PNG） |

## 数据集字段

| 字段 | 说明 |
|------|------|
| article_id | 文章唯一标识 |
| title | 文章标题 |
| author / nickname | 作者信息 |
| publish_date | 发布日期 |
| views | 浏览量 |
| likes | 点赞数 |
| comments | 评论数 |
| collections | 收藏数 |
| description | 文章摘要 |
| language_tags | 技术标签 |
| search_keyword | 来源搜索关键词 |

## 分析方法与结果

### 1. 描述性统计分析

年度发文量分布显示2023-2025年为AI领域发文高峰期，2024年达到峰值1409篇。

![年度发文量分布](figures/fig1_yearly_distribution.png)

各搜索关键词对应的文章数量：

![关键词分布](figures/fig2_keyword_distribution.png)

浏览量、点赞数、评论数的分布特征（截断至P99）：

![数值分布](figures/fig3_metrics_distribution.png)

### 2. TF-IDF文本特征提取

Top30高频词揭示了AI技术社区的核心概念生态：

![Top30高频词](figures/fig4_top30_words.png)

词云可视化：

![词云](figures/fig5_wordcloud.png)

### 3. LDA主题建模

通过一致性评估确定最优主题数K=5，识别出五个核心主题：数据挖掘与ML实践、强化学习、自然语言处理、AIGC与ChatGPT、计算机视觉与Transformer。

![LDA一致性评估](figures/fig6_lda_coherence.png)

![LDA主题-关键词热力图](figures/fig7_lda_heatmap.png)

### 4. K-Means聚类分析

肘部法则与轮廓系数双重评估，最优K=10，SVD降维至50维（解释方差45.2%）。

![K-Means评估](figures/fig8_kmeans_evaluation.png)

![PCA降维可视化](figures/fig9_kmeans_pca.png)

### 5. Apriori关联规则挖掘

发现29条关联规则，最强关联对："神经网络→CNN"（提升度10.55）、"Transformer→深度学习"（提升度4.55）。

![关联规则气泡图](figures/fig10_association_rules.png)

![Top20技术标签频次](figures/fig11_tag_frequency.png)

### 6. 时间序列趋势分析

2023年初出现发文量跃升拐点，与ChatGPT发布后的AI热潮高度一致。

![月度发文趋势](figures/fig12_monthly_trend.png)

![各领域月度热度演变](figures/fig13_keyword_trends.png)

### 7. 分类模型：文章热度预测

四种模型（LR/RF/XGBoost/GBDT）预测文章热度（浏览量≥1000），XGBoost在F1分数上最优（0.7174）。

![模型性能对比](figures/fig14_model_comparison.png)

![特征重要性Top20](figures/fig15_feature_importance.png)

![混淆矩阵](figures/fig16_confusion_matrix.png)

### 8. 技术态度倾向分析

构建技术领域词典（积极推广词69个、审慎问题词52个、技术深度词29个），通过关键词匹配法量化文章态度倾向。积极词均频（1.16次/篇）为审慎词均频（0.43次/篇）的2.7倍。

![三类词频分布](figures/fig17_sentiment_distribution.png)

![各领域态度词频对比](figures/fig18_sentiment_by_keyword.png)

![年度态度趋势](figures/fig19_sentiment_yearly.png)

### 9. 异常检测

Isolation Forest识别出291篇异常文章（5%），其中12篇呈"高浏览低点赞"标题党特征，36篇为"低浏览高点赞"冷门宝藏。

![IF异常分数分布](figures/fig20_iforest_scores.png)

![异常检测散点图](figures/fig21_anomaly_scatter.png)

![IF与LOF对比](figures/fig22_anomaly_comparison.png)

## 环境依赖

```
numpy, pandas, matplotlib, seaborn
scikit-learn, xgboost
jieba, wordcloud, gensim, mlxtend, snownlp
```

Python >= 3.10

## 技术栈

- **数据采集**: Python urllib (CSDN搜索API)
- **文本处理**: jieba分词, TF-IDF, LDA (gensim)
- **聚类/降维**: K-Means, SVD, PCA (scikit-learn)
- **关联规则**: Apriori (mlxtend)
- **分类模型**: Logistic Regression, Random Forest, XGBoost, GBDT
- **情感分析**: 自构建领域词典 + 关键词匹配
- **异常检测**: Isolation Forest, LOF (scikit-learn)
- **可视化**: matplotlib + seaborn (学术风格, SimHei字体)
