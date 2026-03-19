# Articles Using XJTU Battery Dataset: Compilation and Summary

> [!NOTE]
> **Objective:** This document compiles and summarizes articles that utilize the `XJTU battery dataset`, providing detailed records of the results reported in these articles. This is intended to facilitate direct comparison for future works using the same dataset.

Chinese document: [Chinese](./README-CH.md)

Last updated🕒: 2026-3-12 😀😀😀  

**Dataset Links:**
- [GitHub](https://wang-fujin.github.io/)
- [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.10963339.svg)](https://doi.org/10.5281/zenodo.10963339)

**Data Description and Preprocessing Code:**
https://github.com/wang-fujin/Battery-dataset-preprocessing-code-library

**Please cite our paper if you use this dataset:**

[Wang F, Zhai Z, Zhao Z, et al. Physics-informed neural network for lithium-ion battery degradation stable modeling and prognosis[J]. Nature Communications, 2024, 15(1): 4332.](https://www.nature.com/articles/s41467-024-48779-z)

## Data Summary
> [!IMPORTANT]
> The `XJTU battery dataset` comprises 6 batches with a total of 55 batteries. Not all articles use all batteries, so a shorthand is defined to indicate which batteries are used in the articles, formatted as `Bxby`.
> - `Bx` denotes the x-th batch;
> - `by` denotes the y-th battery in that batch;
> - `All` indicates all batteries.
> 
> Examples:
> - `B1b1` indicates the 1st battery in the 1st batch;
> - `B1` indicates all batteries in the 1st batch;
> - `B2b1-b4` indicates the 1st to 4th batteries in the 2nd batch.

> [!IMPORTANT]
> We categorize the training and testing modes (Mode) in the articles into two types:
> - Type 1: Training and testing on the same battery, using early data for training and later data for testing. This mode is noted as `Train A and Test A`, abbreviated as `AA`.
> - Type 2: Training and testing on different batteries, noted as `Train A and Test B`, abbreviated as `AB`.

---





### Summary of SOH Estimation Results
| Battery |       Model Name        | Mode |    MSE     |  RMSE   |  MAE   |    MAPE     | R<sup>2</sup> |              Details              | Paper Link | Non-transfer learning | Transfer learning |
|:-------:|:-----------------------:|:----:|:----------:|:-------:|:------:|:-----------:|:-------------:|:---------------------------------:|:-----:|:-----:|:-----:|
| `B1b1`  |       HHO-LSTM-FC       | `AA` |     -      | 0.0078  | 0.0065 |      -      |    0.9422     |  [Yang et al. (2024)](#yang2024)  | [link](https://www.mdpi.com/2071-1050/16/15/6316) | ✅ | ✅  |
|  `All`  |         CNN[^1]         | `AB` |  0.000161  | -       | 0.0085 |   0.00926   |    0.9187     | [Wang et al. (2024a)](#wang2024a) | [link](https://www.sciencedirect.com/science/article/pii/S2352152X23032826?via%3Dihub) | ✅ | ❌  |
|  `All`  |        LSTM[^1]         | `AB` |  0.000117  | -       | 0.0079 |   0.00861   |    0.9407     | [Wang et al. (2024a)](#wang2024a) | [link](https://www.sciencedirect.com/science/article/pii/S2352152X23032826?via%3Dihub) | ✅ | ❌  |
|  `All`  |         GRU[^1]         | `AB` | 0.0000983  | -       | 0.0071 |   0.00776   |    0.9503     | [Wang et al. (2024a)](#wang2024a) | [link](https://www.sciencedirect.com/science/article/pii/S2352152X23032826?via%3Dihub) | ✅ | ❌  |
|  `All`  |         MLP[^1]         | `AB` |  0.000139  | -       | 0.0078 |   0.00844   |    0.9331     | [Wang et al. (2024a)](#wang2024a) | [link](https://www.sciencedirect.com/science/article/pii/S2352152X23032826?via%3Dihub) | ✅ | ❌  |
|  `All`  |      Attention[^1]      | `AB` |  0.000135  | -       | 0.0087 |   0.00950   |    0.9317     | [Wang et al. (2024a)](#wang2024a) | [link](https://www.sciencedirect.com/science/article/pii/S2352152X23032826?via%3Dihub) | ✅ | ❌  |
|  `B1`   |        MMAU-Net         | `AB` |    -      | 1.40%  | 1.02%  |   -     |      -        | [Fan et al. (2024a)](#fan2024a)   |                                       [link](https://www.mdpi.com/2079-9292/13/16/3244)                                        | ✅ | ❌  |
|  `B2`   |        MMAU-Net         | `AB` |     -     | 1.50%  | 1.04%  |    -    |       -       |  [Fan et al. (2024a)](#fan2024a)  |                                       [link](https://www.mdpi.com/2079-9292/13/16/3244)                                        | ✅ | ❌  |
|  `B3`   |        MMAU-Net         | `AB` |     -     | 1.04%  | 0.66%  |    -    |       -       |  [Fan et al. (2024a)](#fan2024a)  |                                       [link](https://www.mdpi.com/2079-9292/13/16/3244)                                        | ✅ | ❌  |
| `B1-B2` |        MSCNN[^1]        | `AB` |     -     | 0.74%  | 0.67%  |  0.37%  |       -       | [Wang et al. (2024b)](#wang2024b) |                                           [link](https://doi.org/10.3390/en17174220)                                           | ✅ | ❌  |
| `B2b1`  |           ZKF           | `AA` | - | 0.0172 | 0.0125 | - | 0.9624 | [Wang et al. (2024c)](#wang2024c) |                 [link](https://ieeexplore.ieee.org/document/10672556)                  | ✅ | ❌  |
| `B2b4`  |           ZKF           | `AA` | - | 0.0167 | 0.0126 | - | 0.9628 | [Wang et al. (2024c)](#wang2024c) |                 [link](https://ieeexplore.ieee.org/document/10672556)                  | ✅ | ❌  |
| `B2b5`  |           ZKF           | `AA` | - | 0.0123 | 0.0079 | - | 0.9824 | [Wang et al. (2024c)](#wang2024c) |                 [link](https://ieeexplore.ieee.org/document/10672556)                  | ✅ | ❌  |
| `B1-B3` |       MSFDTN[^1]        | `AB` |   0.22%   |   -    | 3.93%  |    -    | 0.9533 | [Wang et al. (2024d)](#wang2024d) |                 [link](https://doi.org/10.1016/j.est.2024.114286)                 |          ❌          |        ✅        |
| `B1-B3` |       DR-Net[^1]        | `AB` |   1.92%   |   -    | 10.49% |    -    |       -       | [Wang et al. (2024d)](#wang2024d) |                 [link](https://doi.org/10.1016/j.est.2024.114286)                 |          ❌          |        ✅        |
| `B1-B3` |       AttMoE[^1]        | `AB` |   2.43%   |   -    | 10.63% |    -    |       -       | [Wang et al. (2024d)](#wang2024d) |                 [link](https://doi.org/10.1016/j.est.2024.114286)                 |          ❌          |        ✅        |
| `B1-B3` |        ELSTM[^1]        | `AB` |   2.07%   |   -    | 11.20% |    -    |       -       | [Wang et al. (2024d)](#wang2024d) |                 [link](https://doi.org/10.1016/j.est.2024.114286)                 |          ❌          |        ✅        |
| `B1-B3` |        MMMe[^1]         | `AB` |   5.53%   |   -    | 18.60% |    -    |       -       | [Wang et al. (2024d)](#wang2024d) |                 [link](https://doi.org/10.1016/j.est.2024.114286)                 |          ❌          |        ✅        |
| `B1-B3` | PVA-FFG-Transformer[^1] | `AB` |   6.11%   |   -    | 21.50% |    -    |       -       | [Wang et al. (2024d)](#wang2024d) |                 [link](https://doi.org/10.1016/j.est.2024.114286)                 |          ❌          |        ✅        |
|  `B1`   | GJO-SNuSVR[^1] | `AB` | - | 0.0048 | - | 0.0041 | - | [Liu  et al. (2025a)](#liu2025a)  | [link](https://doi.org/10.1016/j.est.2024.114822) |          ✅         |       ❌         |
|  `B2`   | EVO-LSSVM | `AB` | - | 0.4939% | - | - |    0.9915     | [Liu  et al. (2025b)](#liu2025b)  | [link](https://doi.org/10.1016/j.measurement.2024.116620) |          ✅         |       ❌         |
|  `B3`   | EVO-LSSVM | `AB` | - | 0.4018% | - | - |    0.9947     | [Liu  et al. (2025b)](#liu2025b)  | [link](https://doi.org/10.1016/j.measurement.2024.116620) |          ✅         |       ❌         |
| `B1b3`  | BiGRU-Attention | `AA` | - | 0.8611  | 0.6522 |    -    |       -       | [Sun et al. (2025a)](#sun2025a)  | [link](https://doi.org/10.1016/j.energy.2025.134756) |          ✅         |       ❌         |
|  `B1`   |      BatteryPINN [^1]      | `AB` | - | 0.5671% |   -    | 0.3443% |       -       |  [Liu et al. (2025c)](#liu2025c)  | [link](https://doi.org/10.1016/j.aei.2025.103211) |          ✅         |       ❌         |
|  `B2`   |      BatteryPINN [^1]      | `AB` | - | 0.2900% |   -    | 0.2014% |       -       |  [Liu et al. (2025c)](#liu2025c)  | [link](https://doi.org/10.1016/j.aei.2025.103211) |          ✅         |       ❌         |
|  `B3`   |      BatteryPINN [^1]      | `AB` | - | 0.7193% |   -    | 0.5817% |       -       |  [Liu et al. (2025c)](#liu2025c)  | [link](https://doi.org/10.1016/j.aei.2025.103211) |          ✅         |       ❌         |
|`B1b1`、`B1b6`、`B2b2`| - | `AA` |  <0.07%   | <2.67%  | <1.61% | - | - |   [He et al. (2025a)](#he2025a)   | [link](https://doi.org/10.1016/j.est.2025.116820) |          ✅         |       ❌         |
|`B1b1-B1b4` | PI-TFT-iDOA | `AA` |     -     |   View details    |   View details     |   -    |       View details        |   [Hu et al. (2025a)](#hu2025a)   | [link](https://doi.org/10.1016/j.energy.2025.138239) |          ✅         |       ❌         |
| `All` | GRU | `AB` | - | 0.0254 | - | 0.0234 | 0.9718 | [Coronado et al. (2025a)](#Coronado2025a) | [link](https://doi.org/10.1109/INTERCON67304.2025.11244713) | ✅         |       ❌         |
| `B1b1-b4` | KAN | `AB` |  - | <0.0052 | <0.0043 | - | - | [Jia et al. (2025a)](#Jia2025a) | [link](https://ieeexplore.ieee.org/document/10922385/) | ✅ |  ❌ |
| `B1` | HSSTT | `AB` | - | 1.638% | 1.285% | - | - | [Lin et al. (2025a)](#Lin2025a) | [link](https://ieeexplore.ieee.org/document/11126537) |  ✅ |  ❌ |
| `B1b1-b4`,`B2b1、b3`| CNN | `AB` | - | view details | - | view details | - | [Zhao et al. (2025a)](#Zhao2025a) | [link](https://doi.org/10.1016/j.est.2025.117296) | ✅ | ✅  |
| `B1b1-b6` | MLPS | `AB` | - | 0.3868% | 0.2531% | 0.2771% | 0.9946 | [Liu et al. (2026a)](#Liu2026a) | [link](https://doi.org/10.1016/j.est.2025.119595) | ✅ |  ❌ |
| `B1` | KG-CNN | `AB` | - | 42.53 mAh | - | - | - | [Zhang et al. (2025a)](#Zhang2025a) | [link](https://doi.org/10.1016/j.ress.2025.111211) | ✅ |  ❌ |
| `B1` | RATGH | `AB` | - | <1.14% | <0.655% | <0.598% |  >0.9643 | [Chen et al. (2026a)](#Chen2026a) | [link](https://link.springer.com/article/10.1007/s00202-025-03350-x) | ✅ |  ❌ |
| `B1b1-b3` | FCSA-PatchTSCT | `AB` | - | <0.0057 | <0.0047 | - | >0.9882 | [Gui et al. (2026a)](#Gui2026a) | [link](https://ieeexplore.ieee.org/document/11265776) | ❌ |  ✅ |
| `All` | FourierKAN | `AB` | - | 1.0765% | 0.84234% | 0.91732% | - | [He et al. (2025b)](#He2025b) | [link](https://ieeexplore.ieee.org/document/11278989) | ✅ |  ❌ |
| `All` | EFATransformer | `AB` | - | 0.4101% | 0.266% | 0.296% | - | [Huang et al. (2025a)](#Huang2025a) | [link](https://ieeexplore.ieee.org/document/11244181) | ✅ |  ❌ |
| `B1-B2` | GAT-LSTM | `AB` | - | <0.23% | <0.11% | <0.12%| >0.9972 | [Gao et al. (2025a)](#Gao2025a) | [link](https://ieeexplore.ieee.org/document/11384461) |✅ |  ❌ |

[^1]: The MSE, RMSE, MAE, and MAPE values in the table are averages across all batteries.

---

### Summary of RUL Prediction Results
| Battery |   Model Name   | Mode |    MSE     |  RMSE   |  MAE   |    MAPE     | R<sup>2</sup> |             Details             | Paper Link | Non-transfer learning | Transfer learning |
|:-------:|:--------------:|:----:|:----------:|:-------:|:------:|:-----------:|:-------------:|:-------------------------------:|:-----:|:-----:|:-----:|
|`B1,B3-B5`| ShuffleNet | `AB` |  - | - | - | - | - | [Feng et al. (2025a)](#feng2025a) | [link](https://doi.org/10.1016/j.est.2025.116210) |          ✅          |        ❌        |
| `B1-B2` | AlexNet | `AB` | - | 24.04[^2] | - | 7.86% | - | [Yang et al. (2025a)](#Yang2025a) | [link](https://doi.org/10.1016/j.jpowsour.2025.236620) | ✅  | ❌ |
| `B1,B3` | ECA-CNN | `AB` | - | - | - | - | - | [Li et al. (2025a)](#Li2025a) | [link](https://ieeexplore.ieee.org/document/11268112) | ✅  | ❌ |

[^2]: The unit is `cycle`.

---

### Summary of V-Q Prediction Results

| Battery |   Model Name   | Mode |    MSE     |  RMSE   |  MAE   |    MAPE     | R<sup>2</sup> |              Details              | Paper Link | Non-transfer learning | Transfer learning |
|:-------:|:--------------:|:----:|:----------:|:-------:|:------:|:-----------:|:-------------:|:---------------------------------:|:-----:|:-----:|:-----:|
| `B1b2` |    PINN    | `AB` |  -  | 14.86e-3 |  -  |  -  | - | [Tang et al. (2024a)](#tang2024a) | [link](https://doi.org/10.1016/j.jechem.2024.10.018) |          ✅          |        ❌        |
| `B1b8` |    PINN    | `AB` |  -  | 22.04e-3 |  -  |  -  | - | [Tang et al. (2024a)](#tang2024a) | [link](https://doi.org/10.1016/j.jechem.2024.10.018) |          ✅          |        ❌        |
| `B2b2` |    PINN    | `AB` |  -  | 40.95e-3 |  -  |  -  | - | [Tang et al. (2024a)](#tang2024a) | [link](https://doi.org/10.1016/j.jechem.2024.10.018) |          ✅          |        ❌        |
| `B2b8` |    PINN    | `AB` |  -  | 37.70e-3 |  -  |  -  | - | [Tang et al. (2024a)](#tang2024a) | [link](https://doi.org/10.1016/j.jechem.2024.10.018) |          ✅          |        ❌        |
|  `B1`   |     -      | `AB` |  -  | 0.046 (max) |  -  |  -  | - | [Tang et al. (2024b)](#tang2024b) | [link](https://doi.org/10.1016/j.etran.2024.100378) |          ✅          |        ❌        |
|  `B2`   |     -      | `AB` |  -  | 0.055 (max) |  -  |  -  | - | [Tang et al. (2024b)](#tang2024b) | [link](https://doi.org/10.1016/j.etran.2024.100378) |          ✅          |        ❌        |



---

---
### Summary of SOC Estimation Results
| Battery | Model Name | Mode |    MSE     | RMSE  |  MAE  | MAPE  | R<sup>2</sup> |              Details              | Paper Link | Non-transfer learning | Transfer learning |
|:-------:|:----------:|:----:|:----------:|:-----:|:-----:|:-----:|:-------------:|:---------------------------------:|:-----:|:-----:|:-----:|
| `B1` |    TFN     | `AB` |  -  | 0.78% | 0.61% | 2.70% | - | [Wang et al. (2025a)](#wang2025a) | [link](https://doi.org/10.1016/j.energy.2025.134722) |          ✅          |        ❌        |
|`B3` |    TFN     | `AB` |  -  | 2.27% | 1.90% | 5.47% | - | [Wang et al. (2025a)](#wang2025a) | [link](https://doi.org/10.1016/j.energy.2025.134722) |          ✅          |        ❌        |

---




# SOH Estimation


<details> 
<summary id="yang2024">
Yang et al. (2024)
</summary>

[Yang G, Wang X, Li R, et al. State of Health Estimation for Lithium-Ion Batteries Based on Transferable Long Short-Term Memory Optimized Using Harris Hawk Algorithm[J]. Sustainability, 2024, 16(15): 6316.](https://www.mdpi.com/2071-1050/16/15/6316)

Used only the 1st battery of Batch-1, noted as `B1b1`.

The article implemented two SOH estimation modes:
1. Pre-training on NASA's B6 and B7 batteries, then fine-tuning with the first 30% data of `B1b1`, followed by testing on `B1b1`.
2. Training with the first 70% data of `B1b1`, followed by testing on `B1b1`.

Results:

|                    | RMSE   | MAE    | R<sup>2</sup> | Mode  |
| ------------------ | ------ | ------ | ------------- | ---  |
| HHO-LSTM-FC-TL(B6) | 0.0037 | 0.0029 | 0.9941        | 1    |
| HHO-LSTM-FC-TL(B7) | 0.0034 | 0.0027 | 0.9952        | 1    |
| HHO-LSTM-FC        | 0.0078 | 0.0065 | 0.9422        | 2    |

</details>

<details>
<summary id="wang2024a">
Wang et al. (2024a)
</summary>

[Wang F, Zhai Z, Liu B, et al. Open access dataset, code library and benchmarking deep learning approaches for state-of-health estimation of lithium-ion batteries[J]. Journal of Energy Storage, 2024, 77: 109884.](https://www.sciencedirect.com/science/article/pii/S2352152X23032826?via%3Dihub)

In this article, we provide a benchmark testing five deep learning models on three types of inputs (`all charging data`, `partial charging data`, `features`) and under three normalization methods.

![Specific Results](./Figures/Wang2024-1.jpg)

The above image shows the results of the five models using `features` as input and `[-1,1] normalization`, with all results magnified by 1000 times. Due to the abundance of results, we only show one type here; other results can be found in the original paper.
</details>

<details>
<summary id="fan2024a">
Fan et al. (2024a)
</summary>

[Fan X, Yang X, Hou F. Integrated Mixed Attention U-Net Mechanisms with Multi-Stage Division Strategy Customized for Accurate Estimation of Lithium-Ion Battery State of Health[J]. Electronics, 2024, 13(16): 3244.](https://www.mdpi.com/2079-9292/13/16/3244)

The article uses data from `Batch-1`, `Batch-2`, and `Batch-3`.
The model inputs are the `raw voltage`, `raw current`, and `raw temperature` data.

Dataset partitioning:

<img src="./Figures/Fan2024a-1.png" alt="Description" width="50%"/>



Experimental results:：

<img src="./Figures/Fan2024a-2.png" alt="Description" width="50%"/>


</details>


<details>
<summary id="wang2024b">
Wang et al. (2024b)
</summary>

[Wang J, Li H, Wu C, et al. State of Health Estimations for Lithium-Ion Batteries Based on MSCNN[J]. Energies, 2024, 17(17): 4220.](https://doi.org/10.3390/en17174220)

The article extracts 8 features from the charging data, which are:
`Constant current charging time`, `Constant voltage charging time`, `Average charging voltage`, `Average charging current`, `Standard deviation of charging voltage`, 
`Skewness of charging current`, `Skewness of charging voltage`, `Kurtosis of charging voltage`.  
Three modes were used to validate the model's performance.

**Note**: In the table below, `Group A` is equivalent to `B1` as defined above;  
`Group B` is equivalent to `B2` as defined above.

---

**Mode 1: Training and testing on the same batch**  
Dataset Partitioning:  

<img src="./Figures/Wang2024b-1.png" alt="Description" width="50%"/>

Results on Batch-1 dataset (`Group A 1`  = `B1b1`):  

<img src="./Figures/Wang2024b-2.png" alt="Description" width="50%"/>


Results on Batch-2 dataset (the article selected odd-numbered batteries from Batch-2, so `Group B x` = `B2b(2x-1)`):  

<img src="./Figures/Wang2024b-3.png" alt="Description" width="50%"/>


---

**Mode 2: Varying the size of the training set**  
Dataset Partitioning:  

<img src="./Figures/Wang2024b-4.png" alt="Description" width="50%"/>

Experimental results:  

<img src="./Figures/Wang2024b-5.png" alt="Description" width="50%"/>


---

**Mode 3: Mixed training and testing on two batches**  
Dataset Partitioning:  

<img src="./Figures/Wang2024b-6.png" alt="Description" width="50%"/>


Experimental results:  

<img src="./Figures/Wang2024b-7.png" alt="Description" width="50%"/>


</details>


<details>
<summary id="wang2024c">
Wang et al. (2024c)
</summary>

[Wang Z, Zhao Z, Zhou M, et al. Online Capacity Prediction of Lithium-Ion Batteries Based on Physics-Constrained Zonotopic Kalman Filter[J]. IEEE Transactions on Reliability, 2024.](https://ieeexplore.ieee.org/document/10672556)

The article uses data from 3 batteries in Batch-2, specifically: `B2b1`, `B2b4`, `B2b5`.  

The training and testing mode is `AA`, meaning early data is used for training and later data for testing.  

The `average charging current (ACC)` during the period from $T_1$ to $T_2$ is constructed as an indirect health indicator (HI) to predict battery capacity.

**Results Visualization**:  

<img src="./Figures/Wang2024c-1.png" alt="Description" width="50%"/>

The authors test the estimated results of **different starting points** (with headers: `battery`, `Cycle`, `MAE`, `RMSE`, `R2`):

<img src="./Figures/Wang2024c-2.png" alt="Description" width="50%"/>

The **comparison results** with other methods provided in the article are as follows:

<img src="./Figures/Wang2024c-3.png" alt="Description" width="50%"/>

</details>




<details>
<summary id="wang2024d">
Wang et al. (2024d)
</summary>

[Wang C, Wu J, Yang Y, et al. Multi-scale self-attention feature decoupling transfer network-based cross-domain capacity prediction of lithium-ion batteries[J]. Journal of Energy Storage, 2024, 103: 114286.](https://doi.org/10.1016/j.est.2024.114286)

The article uses the battery of Batch-1, the first 8 of Batch-2 and Batch-3 to verify the proposed method, which are: `B1-B3`.
The task is to use the transfer learning method to predict the `capacity` of the battery;
The 3 Batchs represent 3 domains, which are represented as D1, D2, and D3 in the article.


**Results Visualization**：
<img src="./Figures/Wang2024d-1.jpg" alt="Description" width="50%"/>


The **comparison results** with other methods provided in the article are as follows:
<img src="./Figures/Wang2024d-2.png" alt="Description" width="70%"/>

</details>




<details>
<summary id="liu2025a">
Liu et al. (2025a)
</summary>

[Liu Y, Ding J, Cai Y, et al. A battery SOH estimation method based on entropy domain features and semi-supervised learning under limited sample conditions[J]. Journal of Energy Storage, 2025, 106: 114822.](https://doi.org/10.1016/j.est.2024.114822)

This paper uses the first 7 battery data of Batch-1 to verify the proposed GJO-SNuSVR method;
The task is SOH estimation;



**Results Visualization**：

<img src="./Figures/Liu2025a-1.png" alt="Description" width="50%"/>


The **comparison results** with other methods provided in the article are as follows:

<img src="./Figures/Liu2025a-2.png" alt="Description" width="70%"/>

</details>



<details>
<summary id="liu2025b">
Liu et al. (2025b)
</summary>

[Liu Y, Ding J, Yao L, et al. A novel high-accuracy intelligent estimation method for battery state of health[J]. Measurement, 2025, 245: 116620.](https://doi.org/10.1016/j.measurement.2024.116620)


This paper uses Batch-1 dataset to train the proposed EVO_LSSVM model and tests it on Batch-2 and Batch3 dataset;
The task is SOH estimation;



**Results Visualization**：

<img src="./Figures/Liu2025b-2.png" alt="Description" width="50%"/>
<img src="./Figures/Liu2025b-3.png" alt="Description" width="50%"/>

The **comparison results** with other methods provided in this paper are as follows:

<img src="./Figures/Liu2025b-1.png" alt="Description" width="70%"/>

</details>


<details>
<summary id="sun2025a">
Sun et al. (2025a)
</summary>

[Sun R, Chen J, Li B, et al. State of health estimation for Lithium-ion batteries based on novel feature extraction and BiGRU-Attention model[J]. Energy, 2025: 134756.](https://doi.org/10.1016/j.energy.2025.134756)


This paper uses the battery 3 of Batch-1 to verify the proposed BiGRU-Attention model, denoted as `B1b3`;
The task is SOH estimation;

The data division method is `AA`, that is, early data is used for training and later data is used for testing;
The author makes two splitting methods: 6:4 and 7:3.

**Results Visualization**：

<img src="./Figures/Sun2025a-2.png" alt="Description" width="70%"/>

The **comparison results** with other methods provided in this paper are as follows:


<img src="./Figures/Sun2025a-1.png" alt="Description" width="70%"/>
</details>


<details>
<summary id="liu2025c">
Liu et al. (2025c)
</summary>

[Liu Y, Chen H, Yao L, et al. A physics-guided approach for accurate battery SOH estimation using RCMHCRE and BatteryPINN[J]. Advanced Engineering Informatics, 2025, 65: 103211.](https://doi.org/10.1016/j.aei.2025.103211)

This paper uses Batch-1 to Batch-3 dataset to verify the proposed BatteryPINN method;

**Results Visualization**：

<img src="./Figures/Liu2025c-1.png" alt="Description" width="50%"/>

Individual SOH estimation results for each battery：

<img src="./Figures/Liu2025c-4.png" alt="Description" width="50%"/>

The **comparison results** with other methods provided in this paper are as follows:


<img src="./Figures/Liu2025c-2.png" alt="Description" width="70%"/>


MAE of the best and worst cases for each Batch:

<img src="./Figures/Liu2025c-3.png" alt="Description" width="70%"/>
</details>

<details>
<summary id="he2025a">
He et al. (2025a)
</summary>

[He H, Zhang W, Long Z, et al. Prediction of lithium-ion batteries health decline trajectories based on early image features[J]. Journal of Energy Storage, 2025, 124: 116820.](https://doi.org/10.1016/j.est.2025.116820)

This paper uses batteries 1 and 6 of Batch-1 and battery 2 of Batch-2 to verify the proposed method, denoted as `B1b1`, `B1b6` and `B2b2`;
The first 20% of the data is used for training, and the last 80% of the data is used for testing.

**Results Visualization**：

<img src="./Figures/He2025a-1.png" alt="Description" width="70%"/>

The estimation result for each battery：

<img src="./Figures/He2025a-2.png" alt="Description" width="50%"/>
</details>


<details>
<summary id="hu2025a">Hu et al. (2025a)</summary>

[Hu Y, Yun Z, Wang J, et al. A battery SOH estimation method based on PI-TFT-iDOA driven Li-Battery discharge state features[J]. Energy, 2025: 138239.](https://doi.org/10.1016/j.energy.2025.138239)


This paper uses the first 4 battery data of Batch-1 to verify the proposed PI-TFT-iDOA method;
The task is SOH estimation;

The estimation result for each battery：

<img src="./Figures/Hu2025a-1.png" alt="Description" width="50%"/>

<img src="./Figures/Hu2025a-2.png" alt="Description" width="50%"/>

</details>

<details>
<summary id="Coronado2025a">Coronado et al. (2025a)</summary>

[Coronado A M, Zegarra F C. Optimizing Neural Networks for SoH Prediction in Li-Ion Batteries: CNN, GRU, and GRU+ Attention with Optuna[C]//2025 IEEE XXXII International Conference on Electronics, Electrical Engineering and Computing (INTERCON). IEEE, 2025: 1-6.](https://doi.org/10.1109/INTERCON67304.2025.11244713)

The paper uses All batches for mixed training and testing:

<img src="./Figures/Coronado2025a-1.png" alt="Description" width="50%"/>

<img src="./Figures/Coronado2025a-2.png" alt="Description" width="50%"/>

</details>


<details>
<summary id='Jia2025a'>Jia et al. (2025a)</summary>

[Z. Jia, Z. Li, Z. Wang, Z. Liu and C. -M. Vong. Joint Prediction of SOH and RUL for Lithium Batteries Considering Capacity Self Recovery and Model Drift[J]. IEEE Internet of Things Journal, vol. 12, no. 12, pp. 22187-22196, 15 June15, 2025](https://ieeexplore.ieee.org/document/10922385)

<img src="./Figures/Jia2025a-1.png" alt="Description" width="50%"/>

<img src="./Figures/Jia2025a-2.png" alt="Description" width="50%"/>

</details>

<details>
<summary id='Lin2025a'>Lin et al. (2025a)</summary>

[Lin X, Bi Y, Fu R, et al. Hierarchical Stochastic Spatial–Temporal Transformer for Trustworthy State-of-Health Estimation of Batteries in Industrial Applications[J]. IEEE Transactions on Industrial Informatics, 2025.](https://ieeexplore.ieee.org/document/11126537)

The article validates the proposed HSSTT (Hierarchical Stochastic Spatial–Temporal Transformer) model using the XJTU `Batch-1`.

<img src="./Figures/Lin2025a-1.png" alt="Description" width="50%"/>

</details>

<details>
<summary id='Zhao2025a'>Zhao et al. (2025a)</summary>

[Zhao J, Zhang X, Hu C. Lithium-ion battery State-of-Health estimation using voltage-position encoding CNN and Incremental Capacity Analysis with a novel smoothing parameter selection strategy[J]. Journal of Energy Storage, 2025, 130: 117296.](https://doi.org/10.1016/j.est.2025.117296)

The study validated the proposed method using the data of the first four batteries in Batch 1 and the data of Battery 1 and Battery 3 in Batch 2, with two settings adopted: transfer setting and non-transfer setting.

**Non-Transfer Setting**: The paper provides the maximum error values under different sampling intervals.

<img src="./Figures/Zhao2025a-1.png" alt="Description" width="50%"/>

<img src="./Figures/Zhao2025a-2.png" alt="Description" width="50%"/>

<img src="./Figures/Zhao2025a-3.png" alt="Description" width="80%"/>

Comparison with other methods:

<img src="./Figures/Zhao2025a-5.png" alt="Description" width="50%"/>


**Transfer Setting**:
Training set uses Battery-4 and Battery-2 from Batch-1. Test data includes Battery-1 and Battery-3 from Batch-2. The first 25% of data from each test battery is used for fine-tuning.

<img src="./Figures/Zhao2025a-4.png" alt="Description" width="80%"/>

</details>

<details>
<summary id='Liu2026a'>Liu et al. (2026a)</summary>

[Liu Y, Xu Y, Liao Z, et al. High-precision battery state-of-health estimation method based on multi-scale gramian matrix entropy and data augmentation[J]. Journal of Energy Storage, 2026, 141: 119595.](https://doi.org/10.1016/j.est.2025.119595)

This study validated the prposed method using the data from the first six batteries in Batch-1.

<img src="./Figures/Liu2026a-1.png" alt="Description" width="80%"/>

</details>

<details>
<summary id='Zhang2025a'>Zhang et al. (2025a)</summary>

[Zhang K, Rayeem S K, Mai W, et al. Enhancing battery health estimation using incomplete charging curves and knowledge-guided deep learning[J]. Reliability Engineering & System Safety, 2025, 262: 111211.](https://doi.org/10.1016/j.ress.2025.111211)

<img src="./Figures/Zhang2025a-1.png" alt="Description" width="80%"/>

<img src="./Figures/Zhang2025a-2.png" alt="Description" width="50%"/>

</details>

<details>
<summary id='Chen2026a'>Chen et al. (2026a)</summary>

[Chen S, Wei C, Han L, et al. RATGH: state of health estimation of lithium-ion batteries based on ResAttention-Transformer with Gramian hybrid field encoding[J]. Electrical Engineering, 2026, 108(1): 55.](https://link.springer.com/article/10.1007/s00202-025-03350-x)

<img src="./Figures/Chen2026a-1.png" alt="Description" width="80%"/>

<img src="./Figures/Chen2026a-2.png" alt="Description" width="80%"/>

Comparison with other methods:

<img src="./Figures/Chen2026a-3.png" alt="Description" width="80%"/>

</details>

<details>
<summary id='Gui2026a'>Gui et al. (2026a)</summary>

[Gui X, Zhang S, Cheng Y, et al. Fine-Grained Subdomain Alignment and Feature Grouping Based Cross-Domain SOH Estimation for Lithium-Ion Batteries Using a Patch Time Series CNN-Transformer Network[J]. IEEE Transactions on Power Electronics, 2025.](https://ieeexplore.ieee.org/document/11265776)

The paper uses the first three batteries of Batch-1 to validate the proposed method. Although the paper uses `transfer learning`, it is based on the same batch of batteries used for both the target domain and the target domain.

<img src="./Figures/Gui2026a-3.png" alt="Description" width="50%"/>

There are three tasks on this dataset: G, H, and I. The results are as follows:

<img src="./Figures/Gui2026a-1.png" alt="Description" width="50%"/>

<img src="./Figures/Gui2026a-2.png" alt="Description" width="50%"/>

</details>

</details>

<details>
<summary id='He2025b'>He et al. (2025b)</summary>

[He J, Li T, Chen J, et al. An Interpretable Fourier Kolmogorov-Arnold Network for State-of-Health Estimation of Lithium-ion Batteries with Partial Charging Data[C]//2025 IEEE 23rd International Conference on Industrial Informatics (INDIN). IEEE, 2025: 1-6.](https://ieeexplore.ieee.org/document/11278989)

This paper proposed the FourierKAN method. The results are as follows:

<img src="./Figures/He2025b-1.png" alt="Description" width="80%"/>

</details>

<details>
<summary id='Huang2025a'>Huang et al. (2025a)</summary>

[Huang R, Chen Y, Liu C. Revealing state-feature dependencies in dynamic degradation: an exofeature-aware transformer for battery state-of-health prediction[J]. IEEE Transactions on Consumer Electronics, 2025.](https://ieeexplore.ieee.org/document/11244181)

This paper used all Batches to validate the proposed method, and the results are as follows:

<img src="./Figures/Huang2025a-1.png" alt="Description" width="80%"/>

Comparison with other methods:

<img src="./Figures/Huang2025a-2.png" alt="Description" width="80%"/>

</details>

<details>
<summary id='Gao2025a'>Gao et al. (2025a)</summary>

[Gao F, Zhang D, Wang P, et al. State-of-Health Estimation of Lithium-Ion Batteries Using Partial Constant-Voltage Charging Data[C]//2025 5th International Conference on New Energy and Power Engineering (ICNEPE). IEEE, 2025: 976-980.](https://ieeexplore.ieee.org/document/11384461)

<img src="./Figures/Gao2025a-1.png" alt="Description" width="50%"/>

</details>

---

# RUL Prediction
<details>
<summary id="feng2025a">
Feng et al. (2025a)
</summary>

[Feng H, Xue D. Parallel-branch enhanced ShuffleNet with dual-physics constraints for lithium-ion battery RUL prediction[J]. Journal of Energy Storage, 2025, 118: 116210.](https://doi.org/10.1016/j.est.2025.116210)

This paper uses battery data from Batch-1, Batch-3, Batch-4, and Batch-5 to verify the proposed ShuffleNet method.

**The detailed results are as follows**：

<img src="./Figures/Feng2025a-1.png" alt="Description" width="50%"/>

</details>

<details>
<summary id="Yang2025a">Yang et al. (2025a)</summary>

[Yang W, Yang H. Ultra-early prediction of lithium-ion battery cycle life based on assembled capacity curve extracted from a single cycle[J]. Journal of Power Sources, 2025, 640: 236620.](https://doi.org/10.1016/j.jpowsour.2025.236620)

This paper constructs features from the data of the first cycle to predict the RUL, using data from `Batch-1` and `Batch-2`, and performs 15-fold cross-validation.

<img src="./Figures/Yang2025a-1.png" alt="Description" width="80%"/>

<img src="./Figures/Yang2025a-2.png" alt="Description" width="80%"/>

<img src="./Figures/Yang2025a-3.png" alt="Description" width="50%"/>

<img src="./Figures/Yang2025a-4.png" alt="Description" width="80%"/>

</details>

<details>
<summary id="Li2025a">Li et al. (2025a)</summary>

[Li H, Wang J, Deng Z, et al. ECA-CNN-Driven RUL Prediction for Lithium-Ion Batteries: A Charging Data Deep Learning Approach[C]//2025 CAA Symposium on Fault Detection, Supervision, and Safety for Technical Processes (SAFEPROCESS). IEEE, 2025: 1-5.](https://ieeexplore.ieee.org/document/11268112)

The paper uses Batch-1 and Batch-3 data for validation. The first battery from each batch is used as the test set, and the remaining batteries as the training set. Data from the first N cycles is used as input to predict the RUL, where N is 50, 100, and 200 respectively. The results are as follows:

<img src="./Figures/Li2025a-1.png" alt="Description" width="50%"/>

</details>

---



# SOC estimation

<details>
<summary id="wang2025a">
Wang et al. (2025a)
</summary>

[Wang X, Yi Y, Yuan Y, et al. Enhanced state of charge estimation in lithium-ion batteries based on Time-Frequency-Net with time-domain and frequency-domain features[J]. Energy, 2025: 134722.](https://doi.org/10.1016/j.energy.2025.134722)


This paper uses the battery data of Batch-1 and Batch-3 to verify the proposed TFN method.
The task is SOC estimation;



**Batch-3 Results Visualization**：

<img src="./Figures/Wang2025a-1.jpg" alt="Description" width="50%"/>

The Table of Batch-3 results：

<img src="./Figures/Wang2025a-2.png" alt="Description" width="70%"/>

The Table of Batch-1 results：

<img src="./Figures/Wang2025a-3.png" alt="Description" width="70%"/>




</details>

---




# Other Tasks

<details>
<summary id="tang2024a">
Tang et al. (2024a)
</summary>

[Tang A, Xu Y, Tian J, et al. Physics-informed battery degradation prediction: Forecasting charging curves using one-cycle data[J]. Journal of Energy Chemistry, 2024.](https://doi.org/10.1016/j.jechem.2024.10.018)

The task of this article is to predict the charging curve, using one-cycle's V-Q curve to predict the V-Q curve of multiple future cycles.
The data of Batch-1 and Batch-2 were used for verification.
In each batch, the data of batteries #1, #3, #4, #5, #6, and #7 are used for training, and the data of #2 and #8 are used for testing.
The prediction length is 150 cycles.

**Results Visualization**：

<img src="./Figures/Tang2024a-1.png" alt="Description" width="50%"/>

</details>


<details>
<summary id="tang2024b"> Tang et al. (2024b) </summary>

[Tang A, Xu Y, Liu P, et al. Deep learning driven battery voltage-capacity curve prediction utilizing short-term relaxation voltage[J]. eTransportation, 2024: 100378.](https://doi.org/10.1016/j.etran.2024.100378)

The article uses the `relaxation voltage` curve to predict the `V-Q curve`, 
and uses the data of Batch-1 and Batch-2 for verification.

Note that the article only gives the value of `maximum RMSE`, which is 0.046 and 0.055 respectively, and does not give the average value.

**Results Visualization**：

<img src="./Figures/Tang2024b-1.png" alt="Description" width="70%"/>

</details>