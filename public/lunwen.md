## 2.2    学生满意度模型构建

​	The performance involved in the above two formulas includes students’ personalized learning expectation performance and current performance. The calculation process of the two performances is similar, and this article will explain the calculation process.

> 上述两个公式中涉及的performance包括学生个性化学习的期望表现（expectation performance）和当前表现（current performance）。这两种表现的计算过程类似，本文将对此计算过程进行说明。

​	The adaptability attribute of learning style is composed of the diversity of learning methods RR and the richness of learning resources B, and the diversified attribute of evaluation criteria is composed of the diversity of evaluation methods C, the combination of process and results Y, self-evaluation and mutual evaluation G. In order to more accurately reflect the adaptability of learning styles and the diversification of evaluation criteria, this article uses different weights to reflect the importance of each parameter in each attribute.

> 学习风格的适应性属性由学习方法的多样性RR和学习资源的丰富性B组成，评价标准多样化属性由评价方法的多样性C、过程与结果结合Y、自我评价与互评G组成。为了更准确地反映学习风格的适应性和评价标准的多样化，本文采用不同权重来体现各参数在每个属性中的重要性。

​	Compared with most complex multi-attribute decision-making algorithms for calculating weights, fuzzy analytic hierarchy process is more suitable for describing uncertainties such as parameter fuzziness, and the weights obtained by this algorithm can more closely express students’ personalized needs. Therefore, this article uses the fuzzy analytic hierarchy process to calculate the weight of learning method diversity and learning resource richness within the adaptability of learning style, and the weight of evaluation method diversity, process and result combination, self-evaluation, and mutual evaluation within the diversity of evaluation criteria.

> 与大多数计算权重的复杂多属性决策算法相比，模糊层次分析法更适合描述参数模糊性等不确定因素，且通过该算法获得的权重能更贴切地表达学生的个性化需求。因此，本文采用模糊层次分析法来计算学习方法多样性与学习资源丰富性在"学习风格适应性"中的权重，以及评价方法多样性、过程与结果结合、自我评价与互评在"评价标准多样化"中的权重

​	Firstly, the target problem of whether students’ personalized learning needs meet expectations is stratified, that’s, it is divided into three layers: target layer, criterion layer and program layer. The target layer is the adaptability of learning styles and the diversified student performance of evaluation standards. The criterion layer is the decision factors that affect the adaptability of learning styles and the diversification of evaluation standards. The program layer is the normalized value of each parameter in each candidate classroom teaching decision. Figure 1 shows a schematic diagram of the hierarchical structure. 

> 首先，将"学生个性化学习需求是否满足期望"这一目标问题进行层次化处理，即划分为目标层、准则层和方案层三个层次。目标层是学习风格的适应性和评价标准多样化的学生表现；准则层是影响学习风格适应性和评价标准多样化的决策因素；方案层则是各候选课堂教学决策中各参数的归一化数值。图1展示了该层次结构的示意图。

​	With the general calculation method of fuzzy judgment matrix, the five parameters of diversity of learning methods RR, richness of learning resources B, diversity of evaluation methods D, combination of process and results Y, self-evaluation and mutual evaluation G in the criterion layer are divided into two groups, respectively constructing matrices to characterize the importance of the adaptability of learning styles and the diversification of evaluation criteria in the target layer. Through the comparison and analysis among the parameters, quantitative scale values$S_{x,y}$，can be obtained. Table 1 shows the applicable comparison scale. It’s essential to further obtain the fuzzy judgment matrix$S=s_{xy}*\left(d*d\right)$,and substitute the two attributes of learning style adaptability and evaluation standard diversification to obtain the corresponding fuzzy complementary judgment matrices $S_{rt}$ and $S_{rp}$.This article obtains $S_{rt}$ and $S_{rp}$ based on the scale method, namely:

> 采用模糊判断矩阵的通用计算方法，将准则层中的五个参数——学习方法多样性RR、学习资源丰富性B、评价方法多样性D、过程与结果结合Y、自评与互评G分为两组，分别构建矩阵来表征目标层中学习风格适应性与评价标准多样化的重要性。通过参数间的两两对比分析，可获得定量标度值$S_{x,y}$，表1展示了适用的比较标度。需进一步获取模糊判断矩阵$S=s_{xy}*(d*d)$，并代入学习风格适应性和评价标准多样化这两个属性，得到相应的模糊互补判断矩阵$S_{rt}$与$S_{rp}$。本文基于标度法获得$S_{rt}$和$S_{rp}$，即：



![image-20250516141148132](https://db.xinghai.ink/Typora/1747375912793645.png)

<div><sup style="display:block;text-align:center;">Fig. 1. Schematic diagram of hierarchical structure</sup></div>


<div style="text-align:center">Table 1. Comparison metrics</div>

| Scale Value             | Definition          | Description                                               |
| ----------------------- | ------------------- | --------------------------------------------------------- |
| 0.9                     | Extremely important | The former is extremely important compared to the latter. |
| 0.8                     | Very important      | The former is very important compared to the latter.      |
| 0.7                     | More important      | The former is more important than the latter.             |
| 0.6                     | Slightly important  | The former is slightly important compared to the latter.  |
| 0.5                     | As important as     | The former is as important as the latter.                 |
| 0.1, 0.2, 0.3, 0.4, 0.5 | Inverse comparison  | Inverse comparison of the above comparisons               |





> ![image-20250516143915056](https://db.xinghai.ink/Typora/17473775591117587.png)
>
> <div><sup style="display:block;text-align:center;">图1. 层次结构示意图</sup></div>
>
> <div style="text-align:center">表1. 比较标度</div>
>
> | 标度值                  | 定义     | 描述                   |
> | ----------------------- | -------- | ---------------------- |
> | 0.9                     | 极其重要 | 前者与后者相比极其重要 |
> | 0.8                     | 非常重要 | 前者与后者相比非常重要 |
> | 0.7                     | 比较重要 | 前者比后者重要         |
> | 0.6                     | 稍微重要 | 前者与后者相比稍微重要 |
> | 0.5                     | 同等重要 | 前者与后者同等重要     |
> | 0.1, 0.2, 0.3, 0.4, 0.5 | 逆向比较 | 上述比较的逆向比较     |


$$
S_{rt} = \begin{array}{ccc} 
  & R & B \\
R & 0.4 & 0.5 \\
B & 0.5 & 0.6

\end{array}
$$

$$
S_{rp} = \begin{array}{cccc}
  &  C  &  Y  &  G  \\
C & 0.5 & 0.4 & 0.7 \\
C & 0.6 & 0.5 & 0.7 \\
G & 0.3 & 0.3 & 0.5

\end{array}
$$

Calculate the weight of each parameter based on the general formula for solving the weight of the fuzzy complementary judgment matrix, let $\sum_{x=1}^{m}q_x=1,q_x\ge0,x=1,2,...,d$, the number of matrix rows is represented by d, the x-th row and the y-th column are represented by x and y, then:
$$
q_x = \frac{\sum\limits_{b=1}^{m}S_{x,y} + \frac{2}{m}-1}{d(d-1)},x=1,2,...,d
$$


> 基于模糊互补判断矩阵求解权重的一般公式，计算各参数的权重。设 $\sum_{x=1}^{m}q_x=1$，且 $q_x\ge0$（$x=1,2,...,d$），其中矩阵的行数用 $d$ 表示，第 $x$ 行第 $y$ 列分别用 $x$ 和 $y$ 表示，则有：
> $$
> q_x = \frac{\sum\limits_{b=1}^{m}S_{x,y} + \frac{2}{m}-1}{d(d-1)},x=1,2,...,d
> $$
>
>
> |                  |      |
> | ---------------- | ---- |
> | 评价方法的多样性 | C    |
> | 自我评价与互评   | G    |
> | 学习资源丰富性   | B    |
> | 学习方法多样性   | R    |
> | 过程与结果结合   | Y    |





Combining the above three formulas, the adaptability of learning style and the diversified weight vector of evaluation criteria can be obtained:
$$
q_{rt} = \begin{array}{cc}
 R   &  B \\
0.55 & 0.45
\end{array}
$$

$$
q_{rp} = \begin{array}{ccc}
C & Y & G \\
0.412 & 0.371 & 0.217
\end{array}
$$


​	It’s assumed that the weight vector of the adaptability $rt$ of the learning style is represented by $q_{rt}$,and the weight vector of the diversification $rp$ of the evaluation standard is represented by $q_{rp}$,Therefore, the weights of learning method diversity R and learning resource richness B in $rt$ are 0.55 and 0.45 respectively. In $rp$, the weights of evaluation method diversity degree C, process and result combination Y, self-evaluation and mutual evaluation degree G $are$ 0.412, 0.371 and 0.217 respectively. Through the consistency check, it can be seen that the adaptability of the learning style and the diversified fuzzy judgment matrix of the evaluation standard are consistent, and the weight value results are completely reasonable.







> 结合上述三个公式，可得出学习风格的适应性与评价准则的多样化权重向量：
> $$
> q_{rt} = \begin{array}{cc}
>  R   &  B \\
> 0.55 & 0.45
> \end{array}
> $$
>
> $$
> q_{rp} = \begin{array}{ccc}
> C & Y & G \\
> 0.412 & 0.371 & 0.217
> \end{array}
> $$
>
> ​	假设学习风格适应性 $rt$ 的权重向量由 $q_{rt}$ 表示，评价标准多样化 $rp$ 的权重向量由 $q_{rp}$ 表示。因此在 $rt$ 中，学习方法多样性 R 和学习资源丰富度 B 的权重分别为 0.55 和 0.45；在 $rp$ 中，评价方法多样性 C、过程与结果结合度 Y、自评与互评度 G 的权重分别为 0.412、0.371 和0.217。通过一致性检验可见，学习风格适应性与评价标准多样化的模糊判断矩阵具有一致性，且权重值结果完全合理。
>
> 

​	 The normalized value of price is defined as the composite value of the personalized attributes of the teaching objective. It’s assumed that the personalized attribute value of the teaching goal of classroom teaching decision $i $ is denoted by $\alpha_{i,td}$, and the price is denoted by D. Given the normalized values and weights of the diversity of evaluation methods, the combination of process and results, self-evaluation and mutual evaluation, the diversity of learning methods, and the richness of learning resources, the comprehensive value of the adaptive attribute of learning style and the diversified attribute of evaluation criteria is the sum of the weight and the normalized value SQ of the corresponding parameters of the two attributes. Assuming that the comprehensive values of personalization of teaching objectives td, adaptability of learning styles $rt$,and diversification of evaluation criteria rp for the i-th classroom teaching decision are represented by $\alpha_{i,td}$, $\alpha_{i,rt}$ and $\alpha_{i,rp}$, then:
$$
\alpha_{i,td} = SQ_{i,D}
$$

$$
\alpha_{i,rt} = q_R \times SQ_{i,R}\,+\, q_B \times SQ_{i,B}
$$

$$
\alpha_{i,rp} = q_c \times SQ_{i,c}\,+\, q_Y \times SQ_{i,Y}\,+\,q_G \times SQ_{i,G}
$$



> 价格的归一化值定义为教学目标的个性化属性综合值。假设课堂教学决策 $i$ 的教学目标个性化属性值记为 $\alpha_{i,td}$，价格记为 D。根据评价方法多样性、过程与结果结合度、自评与互评度、学习方法多样性以及学习资源丰富度的归一化值与权重，学习风格适应性和评价准则多样化属性的综合值为两属性对应参数的权重与归一化值 SQ 之和。假设第 $i$ 个课堂教学决策的教学目标个性化 td、学习风格适应性 $rt$ 和评价准则多样化 rp 的综合值分别表示为 $\alpha_{i,td}$、$\alpha_{i,rt}$ 和 $\alpha_{i,rp}$，则：
>
> 
> $$
> \alpha_{i,td} = SQ_{i,D}
> $$
>
> $$
> \alpha_{i,rt} = q_R \times SQ_{i,R}\,+\, q_B \times SQ_{i,B}
> $$
>
> $$
> \alpha_{i,rp} = q_c \times SQ_{i,c}\,+\, q_Y \times SQ_{i,Y}\,+\,q_G \times SQ_{i,G}
> $$



​	Substitute the six parameters of the current candidate classroom teaching decision-making, and obtain the comprehensive value of the individualization of the teaching objectives, the adaptability of the learning style, and the diversified attributes of the evaluation criteria of all the current candidate classroom teaching decisions, which this article defines it as the current performance of students’ personalized learning, including the current performance of students’ personalized learning $\alpha_{i,t}$ in the case of personalized teaching objectives, the current performance of students’ personalized learning in the case of adaptive learning styles $\alpha_{r,it}$ and the current performance of students’ personalized learning in the case of diversified evaluation standards $\alpha_{i,rp}$.

​	 $n$ group of parameter data and the results of teachers making classroom teaching decisions are obtained from historical data when students are faced with $n$ overlapping classroom teaching decisions. When the $n$ group of data is substituted into the above formula, it can calculate the personalization of teaching objectives, the adaptability of learning styles, and the diversification of evaluation standards when making classroom teaching decisions for n groups of students with personalized learning needs, that’s, the comprehensive value set of the three attributes $\psi_w = \{\alpha_{1,w},\alpha_{2,w},...,\alpha_{m,w}\}$,Among them, $w$ is the three attributes of personalization of teaching objectives, adaptability of learning styles, and diversification of evaluation standards. Considering that there will be a small part of data distortion, this article averages the comprehensive values of each attribute obtained from $f$ times overlapping classroom teaching decision-making situations. It’s assumed that the comprehensive values of personalization of teaching objectives, adaptability of learning styles, and diversification of evaluation standards in the $i$-th overlapping situation are represented by $\beta_{i,w}$, respectively, and the average value of the comprehensive values of students’ demand for classroom teaching decision-making attributes under the historical situation $f$ overlapping is represented by $\beta_w$, which is defined herein as expected performance of personalized learning.
$$
\beta_w = \frac{1}{f} \sum\limits_{i=1}^{f}a_{i,w}
$$
​	Substituting the value of the set $\psi_w$ into the above formula, it’s possible to obtain the expected performance $\beta_{td}$ of students’ personalized learning in the case of personalized teaching objectives, the expected performance $\beta_{rt}$ of personalized learning in the case of adaptive learning style and the expected performance $\beta_{rp}$ in the case of diversified evaluation standards.



> ​	代入当前候选课堂教学决策的六个参数，获得所有当前候选课堂教学决策的教学目标个性化、学习风格适应性及评价准则多样化属性的综合值，本文将之定义为学生个性化学习的当前表现，包括教学目标个性化情形下的学生个性化学习当前表现 $\alpha_{i,t}$、学习风格自适应情形下的学生个性化学习当前表现 $\alpha_{r,it}$ 以及评价标准多样化情形下的学生个性化学习当前表现 $\alpha_{i,rp}$。
>
> ​	从学生面临 $n$ 次重叠课堂教学决策时的历史数据中，可获得 $n$ 组参数数据及教师制定课堂教学决策的结果。当将 $n$ 组数据代入上述公式时，可计算出针对 $n$ 组具个性化学习需求的学生制定课堂教学决策时，其教学目标个性化、学习风格适应性及评价标准多样化的综合值集合 $\psi_w = \{\alpha_{1,w},\alpha_{2,w},...,\alpha_{m,w}\}$，其中 $w$ 为教学目标个性化、学习风格适应性和评价标准多样化这三个属性。考虑到存在小部分数据失真，本文对 $f$ 次重叠课堂教学决策情境下获得的各属性综合值取平均。假设第 $i$ 次重叠情境中教学目标个性化、学习风格适应性与评价标准多样化的综合值分别表示为 $\beta_{i,w}$，则历史情境 $f$ 次重叠下学生对课堂教学决策属性的需求综合值平均值记为 $\beta_w$，本文将其定义为个性化学习的预期表现。
> $$
> \beta_w = \frac{1}{f} \sum\limits_{i=1}^{f}a_{i,w}
> $$
> 将集合 $\psi_w$ 的值代入上述公式，可获得教学目标个性化情形下学生个性化学习的预期表现 $\beta_{td}$、学习风格自适应情形下个性化学习的预期表现 $\beta_{rt}$ 以及评价标准多样化情形下的预期表现 $\beta_{rp}$。



## 2.3  课堂教学决策优化

​	Classroom teaching decision-making for students’ personalized learning needs to comprehensively consider improving teaching quality, cultivating students’ independent learning ability, discovering students’ potential, enhancing students’ participation, paying attention to students’ emotional development, promoting cooperation and communication among students, and adapting to multiple factors such as diversified evaluation standards, carry out overall classroom teaching decision-making planning, make scientific use of available teaching resources, and rationally organize and arrange teaching content to ensure that the classroom teaching effect reaches the expected level. Therefore, classroom teaching decision-making for students’ personalized learning needs focuses on whether teachers can pay attention to students’ personalized needs, reflects respect and satisfaction for students’ differences in teaching decisions, and ensures the teaching effect level of each link of the classroom within an acceptable range to the greatest extent.

​	The multi-objective decision-making model of classroom teaching herein mainly realizes three optimization objectives of maximizing the quality of classroom teaching, maximizing the attention of students’ personalized learning needs, and maximizing students’ dissatisfaction. Based on the determined optimization goal of classroom teaching decision-making, three objective functions are set for the classroom teaching decision-making model, namely objective function G<sub>1</sub>:Maximize the overall quality of classroom teaching within the duration of classroom teaching; objective function G<sub>2</sub> : Maximize attention to students’ personalized learning needs within the duration of classroom teaching; G<sub>3</sub> : Minimize student dissatisfaction within the duration of classroom teaching. In order to facilitate quantitative analysis, this article divides the duration of classroom teaching. Figure 2 shows the process of dividing the duration of classroom teaching.

![image-20250516200752259](https://db.xinghai.ink/Typora/17473972752991233.png)

<div style="text-align:center"><sup>Fig. 2. Classroom teaching duration division process </sup></div>

​	It’s assumed that the index code of classroom teaching quality is represented by $i, j$, the number of classroom teaching link is represented by $l$, the degree of personalized learning needs of students is represented by $K_l$ , the weight of the importance of teaching link $l$ is represented by $\theta_l$ , and the teaching quality of the classroom in the quality status i of the teaching link l is represented by $O_{li}$ after the optimization of the corresponding teaching decision, the duration of classroom teaching is represented by $P$, the p-th period within the duration of classroom teaching is represented by $p$, the proportion of the duration of teaching link at the end of the $p$-th period in quality state $i$ to the duration of classroom teaching is represented by $S_{ip}$, the teaching link $l$ at the end of the $p$-th period in the quality state $i$ is implemented to optimize the proportion of teaching decisions to the duration of classroom teaching is represented by $a_{lip}$ and student dissatisfaction in the teaching link in the quality state i is indicated by $D_i $. The specific objective function is given by the following formula:
$$
MaximizeG_1 = \sum\limits_{k=1}^{n}\sum\limits_{p=1}^{P}\sum\limits_{i=1}^{10}\theta_{i(p-1)}a_{lip}O{li}K_l
$$

$$
MaximizeG_2 = \sum\limits_{l=1}^n\sum\limits_{t=1}^P(S_{1p}+S_{2p})K_l
$$

$$
MinimizeG3 = \sum\limits_{l=1}^n\sum\limits_{p=1}^P\sum\limits_{i=1}^{10}S_{i(p-1)}a_{lip}D_i K_l
$$

​	Assuming that after the teaching environment with the teaching quality state $j$ implements the optimal teaching decision, the transition probability from state $j$ to state $i$ is represented by $P_{lji}$, the dissatisfaction of students in the entire classroom teaching duration is represented by $Y$, and the fluctuation coefficient of student dissatisfaction is represented by $X\%$. The following formula gives the method of calculating the proportion of the duration of teaching link in each teaching quality status at the end of each period within the duration of classroom teaching to the duration of classroom teaching.
$$
S_ip = \sum\limits_{l=1}^n \left[ (1-a_{lip})S_{i(p-1)}T_{lii} + \sum\limits_{j=1}^{10}a_{ljp}S_{jji}P_{lji} \right]i=1,\forall_P
$$

$$
S_{it} = \sum\limits_{l=1}^n \left[ (1-s_{lip})S_{i(p-1)}T_{lii} + (1-a_{l(i-1)p}S_{(i-1)(p-1)}T_{l(i-1)i} + \sum\limits_{j=i}^{10}a_{ljp}S_{j(t-1)}P_{lji} \right] 1 \neq 1, \forall_{p}
$$

​	The constraints of the model are given by the following formula. The following formula constrains the dissatisfaction of students within the duration of classroom teaching.
$$
\sum\limits_{l=1}^{n}\sum\limits_{i=1}^{10}\sum\limits_{p=1}^{10}
$$
![image-20250516200832465](https://db.xinghai.ink/Typora/1747397315901491.png)
