
# 用了XJTU battery dataset的文章统计和整理

> [!NOTE]
> **目的**：本文件统计和整理了使用XJTU battery dataset的文章，并详细记录了该文章中的结果，便于其他文章在使用该数据集时可以直接搬运这里的结果对比。

English document: [English](./README.md)

最近更新🕒：2024-11-28 😀😀😀


**数据集链接：**
- [GitHub](https://wang-fujin.github.io/)
- [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.10963339.svg)](https://doi.org/10.5281/zenodo.10963339)

**数据说明和预处理代码：**
https://github.com/wang-fujin/Battery-dataset-preprocessing-code-library

**如果你使用了该数据集，请引用我们的文章：**

[Wang F, Zhai Z, Zhao Z, et al. Physics-informed neural network for lithium-ion battery degradation stable modeling and prognosis[J]. Nature Communications, 2024, 15(1): 4332.](https://www.nature.com/articles/s41467-024-48779-z)

## 数据汇总

> [!IMPORTANT]
> XJTU battery dataset一共包含6个Batch，共55只电池。并非所有文章都会用到所有电池，所以这里定义了一个缩写来表示文章用了哪些电池，格式为`Bxby`。
> - `Bx`表示第 x 个Batch；
> - `by`表示该Batch的第 y 只电池;
> - `All`表示所有电池。
> 
> 例如:
> - `B1b1`表示第1个Batch的第1只电池;
> - `B1`表示第1个Batch的所有电池;
> - `B2b1-b4`表示第2个Batch的第1到第4只电池;

> [!IMPORTANT]
> 我们把文章的训练和测试模式(Mode)分为两种：
> - 第一种：在同一个电池上训练和测试，用早期的数据训练，后期的数据测试，该模式记为`Train A and Test A`，简称为`AA`；
> - 第二种：在不同电池上训练和测试，该模式记为`Train A and Test B`，简称为`AB`；

---


### SOH估计结果汇总
| Battery |       Model Name       | Mode |    MSE    |  RMSE  |  MAE   |  MAPE   | R<sup>2</sup> |              Details              |                                                           Paper Link                                                           | Non-transfer learning | Transfer learning |
|:-------:|:----------------------:|:----:|:---------:|:------:|:------:|:-------:|:-------------:|:---------------------------------:|:------------------------------------------------------------------------------------------------------------------------------:|:-----:|:-----:|
| `B1b1`  |      HHO-LSTM-FC       | `AA` |     -     | 0.0078 | 0.0065 |    -    |    0.9422     |  [Yang et al. (2024)](#yang2024)  |                                       [link](https://www.mdpi.com/2071-1050/16/15/6316)                                        | ✅ | ✅  |
|  `All`  |        CNN[^1]         | `AB` | 0.000161  |   -    | 0.0085 | 0.00926 |    0.9187     | [Wang et al. (2024a)](#wang2024a) |                     [link](https://www.sciencedirect.com/science/article/pii/S2352152X23032826?via%3Dihub)                     | ✅ | ❌  |
|  `All`  |        LSTM[^1]        | `AB` | 0.000117  |   -    | 0.0079 | 0.00861 |    0.9407     | [Wang et al. (2024a)](#wang2024a) |                     [link](https://www.sciencedirect.com/science/article/pii/S2352152X23032826?via%3Dihub)                     | ✅ | ❌  |
|  `All`  |        GRU[^1]         | `AB` | 0.0000983 |   -    | 0.0071 | 0.00776 |    0.9503     | [Wang et al. (2024a)](#wang2024a) |                     [link](https://www.sciencedirect.com/science/article/pii/S2352152X23032826?via%3Dihub)                     | ✅ | ❌  |
|  `All`  |        MLP[^1]         | `AB` | 0.000139  |   -    | 0.0078 | 0.00844 |    0.9331     | [Wang et al. (2024a)](#wang2024a) |                     [link](https://www.sciencedirect.com/science/article/pii/S2352152X23032826?via%3Dihub)                     | ✅ | ❌  |
|  `All`  |     Attention[^1]      | `AB` | 0.000135  |   -    | 0.0087 | 0.00950 |    0.9317     | [Wang et al. (2024a)](#wang2024a) |                     [link](https://www.sciencedirect.com/science/article/pii/S2352152X23032826?via%3Dihub)                     | ✅ | ❌  |
|  `B1`   |        MMAU-Net        | `AB` |     -     | 1.40%  | 1.02%  |   -     |       -       | [Fan et al. (2024a)](#fan2024a)   |                                       [link](https://www.mdpi.com/2079-9292/13/16/3244)                                        | ✅ | ❌  |
|  `B2`   |        MMAU-Net        | `AB` |     -     | 1.50%  | 1.04%  |    -    |       -       |  [Fan et al. (2024a)](#fan2024a)  |                                       [link](https://www.mdpi.com/2079-9292/13/16/3244)                                        | ✅ | ❌  |
|  `B3`   |        MMAU-Net        | `AB` |     -     | 1.04%  | 0.66%  |    -    |       -       |  [Fan et al. (2024a)](#fan2024a)  |                                       [link](https://www.mdpi.com/2079-9292/13/16/3244)                                        | ✅ | ❌  |
| `B1-B2` |       MSCNN[^1]        | `AB` |     -     | 0.74%  | 0.67%  |  0.37%  |       -       | [Wang et al. (2024b)](#wang2024b) |                                           [link](https://doi.org/10.3390/en17174220)                                           | ✅ | ❌  |
| `B2b1`  |          ZKF           | `AA` |     -     | 0.0172 | 0.0125 | - |    0.9624     | [Wang et al. (2024c)](#wang2024c) |                 [link](https://ieeexplore.ieee.org/document/10672556)                  | ✅ | ❌  |
| `B2b4`  |          ZKF           | `AA` |     -     | 0.0167 | 0.0126 | - |    0.9628     | [Wang et al. (2024c)](#wang2024c) |                 [link](https://ieeexplore.ieee.org/document/10672556)                  | ✅ | ❌  |
| `B2b5`  |          ZKF           | `AA` |     -     | 0.0123 | 0.0079 | - |    0.9824     | [Wang et al. (2024c)](#wang2024c) |                 [link](https://ieeexplore.ieee.org/document/10672556)                  | ✅ | ❌  |
| `B1-B3` |       MSFDTN[^1]       | `AB` |   0.22%   |   -    | 3.93%  |    -    |    0.9533     | [Wang et al. (2024d)](#wang2024d) |                 [link](https://doi.org/10.1016/j.est.2024.114286)                 |          ❌          |        ✅        |
| `B1-B3` |       DR-Net[^1]       | `AB` |   1.92%   |   -    | 10.49% |    -    |       -       | [Wang et al. (2024d)](#wang2024d) |                 [link](https://doi.org/10.1016/j.est.2024.114286)                 |          ❌          |        ✅        |
| `B1-B3` |       AttMoE[^1]       | `AB` |   2.43%   |   -    | 10.63% |    -    |       -       | [Wang et al. (2024d)](#wang2024d) |                 [link](https://doi.org/10.1016/j.est.2024.114286)                 |          ❌          |        ✅        |
| `B1-B3` |       ELSTM[^1]        | `AB` |   2.07%   |   -    | 11.20% |    -    |       -       | [Wang et al. (2024d)](#wang2024d) |                 [link](https://doi.org/10.1016/j.est.2024.114286)                 |          ❌          |        ✅        |
| `B1-B3` |        MMMe[^1]        | `AB` |   5.53%   |   -    | 18.60% |    -    |       -       | [Wang et al. (2024d)](#wang2024d) |                 [link](https://doi.org/10.1016/j.est.2024.114286)                 |          ❌          |        ✅        |
| `B1-B3` | PVA-FFG-Transforme[^1] | `AB` |   6.11%   |   -    | 21.50% |    -    |       -       | [Wang et al. (2024d)](#wang2024d) |                 [link](https://doi.org/10.1016/j.est.2024.114286)                 |          ❌          |        ✅        |



[^1]: 表格中的MSE，RMSE，MAE，MAPE都是所有电池的平均值。

---

### RUL预测结果汇总
| Battery |   Model Name   | Mode |    MSE     |  RMSE   |  MAE   |    MAPE     | R<sup>2</sup> |             Details             | Paper Link | Non-transfer learning | Transfer learning |
|:-------:|:--------------:|:----:|:----------:|:-------:|:------:|:-----------:|:-------------:|:-------------------------------:|:-----:|:-----:|:-----:|

---

### V-Q 曲线预测结果汇总

| Battery | Model Name | Mode |    MSE     |    RMSE     |  MAE   |    MAPE     | R<sup>2</sup> |              Details              | Paper Link | Non-transfer learning | Transfer learning |
|:-------:|:----------:|:----:|:----------:|:-----------:|:------:|:-----------:|:-------------:|:---------------------------------:|:-----:|:-----:|:-----:|
| `B1b2`  |    PINN    | `AB` |  -  |  14.86e-3   |  -  |  -  | - | [Tang et al. (2024a)](#tang2024a) | [link](https://doi.org/10.1016/j.jechem.2024.10.018) |          ✅          |        ❌        |
| `B1b8`  |    PINN    | `AB` |  -  |  22.04e-3   |  -  |  -  | - | [Tang et al. (2024a)](#tang2024a) | [link](https://doi.org/10.1016/j.jechem.2024.10.018) |          ✅          |        ❌        |
| `B2b2`  |    PINN    | `AB` |  -  |  40.95e-3   |  -  |  -  | - | [Tang et al. (2024a)](#tang2024a) | [link](https://doi.org/10.1016/j.jechem.2024.10.018) |          ✅          |        ❌        |
| `B2b8`  |    PINN    | `AB` |  -  |  37.70e-3   |  -  |  -  | - | [Tang et al. (2024a)](#tang2024a) | [link](https://doi.org/10.1016/j.jechem.2024.10.018) |          ✅          |        ❌        |
|  `B1`   |     -      | `AB` |  -  | 0.046 (max) |  -  |  -  | - | [Tang et al. (2024b)](#tang2024b) | [link](https://doi.org/10.1016/j.etran.2024.100378) |          ✅          |        ❌        |
|  `B2`   |     -      | `AB` |  -  | 0.055 (max) |  -  |  -  | - | [Tang et al. (2024b)](#tang2024b) | [link](https://doi.org/10.1016/j.etran.2024.100378) |          ✅          |        ❌        |

---




# SOH estimation


<details> 
<summary id="yang2024">
Yang et al. (2024)
</summary>

[Yang G, Wang X, Li R, et al. State of Health Estimation for Lithium-Ion Batteries Based on Transferable Long Short-Term Memory Optimized Using Harris Hawk Algorithm[J]. Sustainability, 2024, 16(15): 6316.](https://www.mdpi.com/2071-1050/16/15/6316)

只用了Batch-1的第1个电池，记为`B1b1`。

文章实现了两种SOH估计模式：
1. 在NASA的B6和B7电池上预训练，然后用B1b1前30%的数据微调，然后再B1b1上测试；
2. 用B1b1的前70%的数据训练，然后在B1b1上测试；

结果：

|                    | RMSE   | MAE    | R2     | 模式  |
| ------------------ | ------ | ------ | ------ | --- |
| HHO-LSTM-FC-TL(B6) | 0.0037 | 0.0029 | 0.9941 | 1   |
| HHO-LSTM-FC-TL(B7) | 0.0034 | 0.0027 | 0.9952 | 1   |
| HHO-LSTM-FC        | 0.0078 | 0.0065 | 0.9422 | 2   |

</details>

<details>
<summary id="wang2024a">
Wang et al. (2024a)
</summary>

[Wang F, Zhai Z, Liu B, et al. Open access dataset, code library and benchmarking deep learning approaches for state-of-health estimation of lithium-ion batteries[J]. Journal of Energy Storage, 2024, 77: 109884.](https://www.sciencedirect.com/science/article/pii/S2352152X23032826?via%3Dihub)

我们在这篇文章中提供了一个benchmark，测试了5个深度学习模型在3种输入类型（`全部充电数据`、`部分充电数据`、`特征`）和3种归一化方式下的结果。


![具体结果](./Figures/Wang2024-1.jpg)

上面的图片是以`特征`作为输入，`[-1,1]归一化`的情况下5个模型的结果，所有结果都被放大了1000倍。
由于结果太多，我们只展示其中一种结果，其他结果可以查看原文。
</details>

<details>
<summary id="fan2024a">
Fan et al. (2024a)
</summary>

[Fan X, Yang X, Hou F. Integrated Mixed Attention U-Net Mechanisms with Multi-Stage Division Strategy Customized for Accurate Estimation of Lithium-Ion Battery State of Health[J]. Electronics, 2024, 13(16): 3244.](https://www.mdpi.com/2079-9292/13/16/3244)

文章使用了Batch-1、Batch-2和Batch-3的数据。
模型的输入为原始的电压、电流和温度数据。

训练集和测试集划分方式：

<img src="./Figures/Fan2024a-1.png" alt="Description" width="50%"/>

实验结果：

<img src="./Figures/Fan2024a-2.png" alt="Description" width="50%"/>


</details>

<details>
<summary id="wang2024b">
Wang et al. (2024b)
</summary>

[Wang J, Li H, Wu C, et al. State of Health Estimations for Lithium-Ion Batteries Based on MSCNN[J]. Energies, 2024, 17(17): 4220.](https://doi.org/10.3390/en17174220)

文章从充电数据中提取了8个特征，分别为：
`恒流充电时间`、`恒压充电时间`、`平均充电电压`、`平均充电电流`、`充电电压标准差`、
`充电电流偏度`、`充电电压偏度`、`充电电压峰度`。
分了3种模式来验证模型性能。

**注意**：下面表格中的记法`Group A`等效于上文定义的`B1`;
`Group B`等效于上文定义的`B2`。

---

**模式1：同一批次训练和测试**
训练集和测试集划分方式：

<img src="./Figures/Wang2024b-1.png" alt="Description" width="50%"/>

Batch-1数据集上的结果（表格中的`Group A 1` = `B1b1`） ：

<img src="./Figures/Wang2024b-2.png" alt="Description" width="50%"/>


Batch-2数据集上的结果（文章选择了Batch-2中的编号为奇数的电池，所以`Group B x` = `B2b(2x-1)`）：

<img src="./Figures/Wang2024b-3.png" alt="Description" width="50%"/>

---

**模式2：改变训练集的大小**
训练集和测试集划分方式：

<img src="./Figures/Wang2024b-4.png" alt="Description" width="50%"/>


实验结果：

<img src="./Figures/Wang2024b-5.png" alt="Description" width="50%"/>


---

**模式3：两个批次混合训练和测试**
训练集和测试集划分方式：

<img src="./Figures/Wang2024b-6.png" alt="Description" width="50%"/>

实验结果：

<img src="./Figures/Wang2024b-7.png" alt="Description" width="50%"/>

</details>

<details>
<summary id="wang2024c">
Wang et al. (2024c)
</summary>

[Wang Z, Zhao Z, Zhou M, et al. Online Capacity Prediction of Lithium-Ion Batteries Based on Physics-Constrained Zonotopic Kalman Filter[J]. IEEE Transactions on Reliability, 2024.](https://ieeexplore.ieee.org/document/10672556)

文章使用了Batch-2的3个电池数据，分别为：`B2b1`、`B2b4`、`B2b5`。

训练和测试的模式为`AA`,即用早期的数据训练，后期的数据测试。

构造了 $T_1$ 至 $T_2$ 期间的`平均充电电流`（ACC）作为间接HI来预测电池容量。

**结果可视化**：

<img src="./Figures/Wang2024c-1.png" alt="Description" width="50%"/>

文章分别测试了**不同预测起点**的结果：（表头分别为：`battery`, `Cycle`, `MAE`, `RMSE`, `R2`）

<img src="./Figures/Wang2024c-2.png" alt="Description" width="50%"/>

文章给出的与其他**方法对比**的结果如下：

<img src="./Figures/Wang2024c-3.png" alt="Description" width="50%"/>

</details>



<details>
<summary id="wang2024d">
Wang et al. (2024d)
</summary>

[Wang C, Wu J, Yang Y, et al. Multi-scale self-attention feature decoupling transfer network-based cross-domain capacity prediction of lithium-ion batteries[J]. Journal of Energy Storage, 2024, 103: 114286.](https://doi.org/10.1016/j.est.2024.114286)

文章使用了Batch-1、Batch-2的前8个和Batch-3的电池数据来验证提出的方法，分别为：`B1-B3`。
任务是使用迁移学习方法来预测电池的`容量`；
3个Batch分别表示3个域，文中表示为D1、D2、D3。


**结果可视化**：

<img src="./Figures/Wang2024d-1.jpg" alt="Description" width="50%"/>


文章给出的与其他**方法对比**的结果如下：

<img src="./Figures/Wang2024d-2.png" alt="Description" width="70%"/>

</details>










---

# RUL prediction

---

# 其他任务

<details>
<summary id="tang2024a">
Tang et al. (2024a)
</summary>

[Tang A, Xu Y, Tian J, et al. Physics-informed battery degradation prediction: Forecasting charging curves using one-cycle data[J]. Journal of Energy Chemistry, 2024.](https://doi.org/10.1016/j.jechem.2024.10.018)

文章所做的任务是预测充电曲线，用一个cycle的CC阶段的V-Q预测来预测未来多个cycle的V-Q曲线。
用了Batch-1和Batch-2的数据来验证。
每个Batch中，电池#1，#3，#4，#5，#6，#7的数据用来训练，#2，#8的数据用来测试。
预测长度为150个cycle。

</details>


<details>
<summary id="tang2024b"> Tang et al. (2024b) </summary>
[Tang A, Xu Y, Liu P, et al. Deep learning driven battery voltage-capacity curve prediction utilizing short-term relaxation voltage[J]. eTransportation, 2024: 100378.](https://doi.org/10.1016/j.etran.2024.100378)

文章利用驰豫电压曲线来预测V-Q曲线，用了Batch-1和Batch-2的数据来验证。

注意，文章只给出了`最大RMSE`的值，分别为0.046和0.055，并没有给出平均值。

**结果可视化**：

<img src="./Figures/Tang2024b-1.png" alt="Description" width="70%"/>


</details>

