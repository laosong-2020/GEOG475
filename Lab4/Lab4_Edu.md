# GEOG 475 Advanced GIS Lab4 - Education Meterial

>**Topic**: Criteria Based Modeling
>
>**100 points**
>
>**Author:** Zhenlei Song
>
>**Contact:** [songzl@tamu.edu](mailto:songzl@tamu.edu)

> Note: The methodologies introduced in this document came from this peer-reviewed paper:
> [Song, Z., Chapman, P., Tao, J., Chang, P., Gao, H., Liu, H., … Zhang, Z. (2024). Mapping the Unheard: Analyzing Tradeoffs Between Fisheries and Offshore Wind Farms Using Multicriteria Decision Analysis. Annals of the American Association of Geographers, 114(3), 536–554. https://doi.org/10.1080/24694452.2023.2285371](https://doi.org/10.1080/24694452.2023.2285371)

## Multi-Criteria Decision Analysis (MCDA)

Multicriteria decision analysis (MCDA) is a mathematical decision-making framework that combines many decision criteria to meet one or several objectives that support decision-making (Shao et al. 2020).

### Weighted Sum Method (WSM)

given a set of $m$ alternatives, denoted as $A_1, A_2, A_3, … , A_m$, and a set of $n$ decision criteria, denoted as $C_1, C_2, C_3, … , C_n$, it is assumed that a decision-maker has to determine the weight value $\omega_⁢j (\text{for }i = 1,2,3, … , m \text{ and }j = 1, 2, 3, … , n) $of each alternative in terms of each criterion (Fishburn 1967).

For each row of data set $X$ with $x_j$, values are defined, along with the criteria weight matrix $W$ (the weight of the relative performance of the decision criteria). Usually, these weights are normalized to add up to one, and the alternatives are ranked. If there are $m$ alternatives and $n$ criteria, the score calculated using `WSM` for the $i$th decision alternative can be represented as the equation below (Fishburn 1967; Thakkar 2021), 

$$
    Q_{i}^{WSM} = \sum_{j=1}^{n} \omega_{i,j} x_j
$$

where:

- $\omega_{i,j}$ is the weight for the $j$th criteria in the ith decision alternative;
- $x_j$ is the data value of the $j$th column (attribute);
- $Q_{i}^{WSM}$ is the `WSM` score for the ith decision alternative.

### Weighted Product Method (WPM)

The `weighted product method (WPM)` is similar to the `WSM`. The main difference is that instead of addition in the model, there is multiplication. Each alternative is compared with the others by multiplying a number of ratios, one for each criterion. Each ratio is raised to the power equivalent of the relative weight of the corresponding criterion (Triantaphyllou and Mann 1989). In `WPM`, under the same problem conditions, the score for the $i$th decision alternative can be expressed as the equation below,

$$
    Q_{WPM,i} = \prod_{j=1}^{n} x_j^{\omega_{i,j}}
$$
where:

- $\omega_{i,j}$ represents the weight for the $j$th criteria in the ith decision alternative;
- $x_j$ represents the data value of the $j$th column (attribute);
- $Q_{i}^{WPM}$ represents the `WPM` score for the $i$th decision alternative (Thakkar 2021).

### Weighted Aggregated Sum Product Assessment (WASPAS)

The `WSM` and `WPM` are widely used in `MCDM` processes, but each has limitations. `WSM`’s main disadvantage is its assumption of additive criteria, overlooking potential interactions, whereas `WPM` assumes criteria are multiplicative, which might neglect interactions and distort results with zero values. The `WASPAS` method seeks to balance these models’ strengths and weaknesses by providing a weighted average of both approaches, offering more comprehensive and flexible decision-making outcomes (Zavadskas et al. 2012). `WASPAS` is preferred to the variety of available methods because of its ability to increase the accuracy of ranking. `WASPAS` leads to the highest accuracy of estimation for optimization of the weighted aggregate function. It combines two well-known methods—the `WSM` and the `WPM` to provide a method with accuracy greater than the original two methods, with an optimization of the aggregation being conducted (Thakkar Citation2021). `WASPAS` uses a $\lambda$ value to coordinate the output share of the two models, which generally defaults to $0.5$ out of $1$; that is, equal reception of the outputs from `WSM` and `WPM`. The weighted score value calculated using the `WASPAS` method can be expressed in the equation below, 

$$
    Q_{WASPAS,i} = \lambda \cdot Q_{i}^{WSM} + (1 - \lambda) \cdot Q_{i}^{WPM}\\
    = \lambda \cdot \left( \sum_{j=1}^{n} \omega_{i,j} x_j \right) + (1 - \lambda) \cdot \left( \prod_{j=1}^{n} x_j^{\omega_{i,j}} \right)
$$

where:

- $\omega_{i,j}$ represents the weight for the $j$th criteria in the ith decision alternative;
- $x_{j}$ represents the data value of the $j$th column (attribute);
- $Q_{i}^{WASPAS}$ represents the `WASPAS` score for the ith decision alternative (Thakkar 2021).

### Other methods

There are many other methods for multi-criteria decision analysis, such as the `Analytic Hierarchy Process (AHP)`, `Technique for Order Preference by Similarity to Ideal Solution (TOPSIS)`, and `Simple Additive Weighting (SAW)`. Each method has its own advantages and disadvantages, and the choice of method depends on the specific problem and the preferences of the decision-maker.

Here are extra readings for those who are interested in learning more about multi-criteria decision analysis:

- `AHP`: Saaty, T. L. 1977. A scaling method for priorities in hierarchical structures. Journal of Mathematical Psychology 15 (3):234–81. doi: 10.1016/0022-2496(77)90033-5.
- `TOPSIS`: Uzun, B., M. Taiwo, A. Syidanova, and D. U. Ozsahin. 2021. The technique for order of preference by similarity to ideal solution (TOPSIS). In Application of multi-criteria decision analysis in environmental and civil engineering, ed. D. U. Ozsahin, H. Gökçekuş, B. Uzun, and J. LaMoreaux, 25–30. Cham, Switzerland: Springer Nature. doi: 10.1007/978-3-030-64765-0_4.

## Normalization & Reclassification

Because the way people apply different criteria onto the decision-making process is not always consistent, it is often necessary to normalize the data values of each criterion to a common scale. Normalization is the process of adjusting values in a dataset to a common scale, which allows for fair comparisons across different criteria. The most common normalization methods include:

- **Min-Max Normalization**: This method rescales the data to a fixed range, typically [0, 1]. The formula is given by:

$$
    x_{norm} = \frac{x - x_{min}}{x_{max} - x_{min}}
$$

- **Z-Score Normalization**: This method standardizes the data by removing the mean and scaling to unit variance. The formula is given by:

$$
    x_{norm} = \frac{x - \mu}{\sigma}
$$
where $\mu$ is the mean and $\sigma$ is the standard deviation of the dataset.

If the task desires the data to be discrete values instead of continuous values, reclassification is necessary. Reclassification is the process of grouping continuous data into discrete classes or categories.

Beside normalizing/reclassifying the magnitude of the data from multiple criteria, it is also important to unify the direction of the data values. For example, in some cases, a higher value is preferred (e.g., elevation), while in others, a lower value is preferred (e.g., distance to a road). In such cases, reclassification is necessary to ensure that all criteria are oriented in the same direction. This can be done by reversing the scale of the data values for criteria where lower values are preferred.

## Sensitivity Analysis

`Sensitivity analysis (SA)` refers to the process of examining the impact of changes in criteria weights or alternative evaluations on the overall decision outcome. It is a valuable technique for assessing the robustness and stability of the decision-making process (Saltelli et al. 2004; Z. Zhang et al. 2018). A numeric value often represents the sensitivity of each input called the sensitivity index (Iwanaga, Usher, and Herman 2022):

- `First-order` indexes (S1) measure the contribution of the output variance by a single model input alone;
- `Second-order` indexes (S2) measure the contribution of the output variance caused by the interaction between two model inputs;
- `total-order` index (ST) measures the contribution of the output variance caused by a model input, including both its `S1` effects (the input varying alone) and all higher order interactions (Herman and Usher 2017).

In practice, `ST` is commonly used when discovering the effects of each decision criterion on the decision modeling outputs. `S2` are used when discussing the correlation between different decision criteria in `MCDM` problems.

## References

- Song, Z., Chapman, P., Tao, J., Chang, P., Gao, H., Liu, H., … Zhang, Z. (2024). Mapping the Unheard: Analyzing Tradeoffs Between Fisheries and Offshore Wind Farms Using Multicriteria Decision Analysis. Annals of the American Association of Geographers, 114(3), 536–554. https://doi.org/10.1080/24694452.2023.2285371
- Shao, M., Z. Han, J. Sun, C. Xiao, S. Zhang, and Y. Zhao. 2020. A review of multi-criteria decision making applications for renewable energy site selection. Renewable Energy 157 (September):377–403. doi: 10.1016/j.renene.2020.04.137.
- Fishburn, P. C. 1967. Letter to the editor—Additive utilities with incomplete product sets: Application to priorities and assignments. Operations Research 15 (3):537–42. doi: 10.1287/opre.15.3.537.
- Thakkar, J. J. 2021. Weighted aggregated sum product assessment (WASPAS). In Multi-criteria decision making: Studies in systems, decision and control, vol. 336, 253–79. Singapore: Springer International. doi: 10.1007/978-981-33-4745-8_15.
- Triantaphyllou, E., and S. H. Mann. 1989. An examination of the effectiveness of multi-dimensional decision-making methods: A decision-making paradox. Decision Support Systems 5 (3):303–12. doi: 10.1016/0167-9236(89)90037-7.
- Zavadskas, E. K., Z. Turskis, J. Antucheviciene, and A. Zakarevičius. 2012. Optimization of weighted aggregated sum product assessment. Elektronika ir Elektrotechnika 122 (6):3–6. doi: 10.5755/j01.eee.122.6.1810.
- Saaty, T. L. 1977. A scaling method for priorities in hierarchical structures. Journal of Mathematical Psychology 15 (3):234–81. doi: 10.1016/0022-2496(77)90033-5.
- Uzun, B., M. Taiwo, A. Syidanova, and D. U. Ozsahin. 2021. The technique for order of preference by similarity to ideal solution (TOPSIS). In Application of multi-criteria decision analysis in environmental and civil engineering, ed. D. U. Ozsahin, H. Gökçekuş, B. Uzun, and J. LaMoreaux, 25–30. Cham, Switzerland: Springer Nature. doi: 10.1007/978-3-030-64765-0_4.
- Saltelli, A., S. Tarantola, F. Campolongo, and M. Ratto. 2004. Sensitivity analysis in practice: A guide to assessing scientific models. Sydney, Australia: Halsted Press EBooks.
- Zhang, X.-Y., X.-K. Wang, S.-M. Yu, J.-Q. Wang, and T.-L. Wang. 2018. Location selection of offshore wind power station by consensus decision framework using picture fuzzy modelling. Journal of Cleaner Production 202 (November):980–92. doi: 10.1016/j.jclepro.2018.08.172.
- Iwanaga, T., W. Usher, and J. Herman. 2022. Toward SALib 2.0: Advancing the accessibility and interpretability of global sensitivity analyses. Socio-Environmental Systems Modelling 4 (May):18155. doi: 10.18174/sesmo.18155.
- Herman, J., and W. Usher. 2017. SALib: An open-source Python library for sensitivity analysis. The Journal of Open Source Software 2 (9):97. doi: 10.21105/joss.00097