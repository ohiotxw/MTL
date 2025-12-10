

# 概览 (Overview)

**DGHME** 是一个基于 PyTorch 的深度学习多任务模型，专为**临床表格数据**设计。它能够从真实的患者数据中学习，并对多种并发症风险进行高精度的同步预测。

| 重要链接 (Important Links) | |
| :--- | :--- |
| :computer: **[项目网站][项目网站]** | 访问我们的项目网站，了解更多关于我们的医疗预测模型生态系统。 |
| :orange\_book: **[技术博客][技术博客]** | 深入了解多任务学习、模型可解释性以及在临床AI中的应用。 |
| :book: **[文档][文档]** | 包含快速入门、用户指南、开发文档和API参考。 |
| :octocat: **[代码仓库][代码仓库]** | 本项目的 GitHub 仓库链接。 |
| :keyboard: **[开发状态][开发状态]** | 本软件目前处于 **Beta** 测试阶段。 |
| [ **社区**][Community] | 加入我们的 Slack 工作区，参与讨论并获取最新公告。 |

目前，该库实现了在 *[此处添加您的论文标题]* 论文中描述的 **DGHME** 模型，该论文发表于 *[此处添加会议/期刊名称，如 AMIA 2025]*。

# 安装 (Install)

您可以通过 `pip` 或 `conda` 直接安装 **DGHME** 独立库。

**使用 `pip`:**

```bash
pip install dghme
```

**使用 `conda`:**

```bash
conda install -c pytorch -c your-channel dghme
```

当直接使用 DGHME 库时，您可能需要手动将数据预处理为正确的格式，例如：

  * 连续特征必须是浮点数（`float`）。
  * 分类特征必须是整数（`int`）或字符串（`string`）。
  * 数据中不应包含任何缺失值。

# 使用示例 (Usage Example)

在此示例中，我们加载一个内置的糖尿病并发症模拟数据集。我们使用 `DGHME` 模型从真实数据中学习，然后对新样本进行预测。

```python
from dghme import DGHME
from dghme import load_demo

# 加载模拟的患者数据和任务信息
real_data, continuous_cols, target_cols, task_groups_config = load_demo()

# 初始化 DGHME 模型
# 模型的关键在于定义任务分组
dghme = DGHME(
    task_groups=task_groups_config,
    epochs=100
)

# 使用真实数据进行训练
dghme.fit(real_data, continuous_cols, target_cols)

# 创建一些新的患者数据用于预测 (这里我们使用训练数据的前5行作为示例)
new_patient_data = real_data.head(5)

# 进行预测
predictions = dghme.predict(new_patient_data)

print(predictions)
```

*关于此模拟数据集的更多信息，请参阅我们的文档。*
