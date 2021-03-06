# Udacity--A-B_Test

## 项目背景
在进行此试验时，优达学城当前的主页上有两个选项：“开始免费试学”和“访问课程资料”。如果学生点击“开始免费试学”，系统将要求他们输入信用卡信息，然后他们将进入付费课程版本的免费试学。14 天后，将对他们自动收费，除非他们在此期限结束前取消试用。若学生点击“访问课程材料”，他们将能够观看视频和免费进行小测试，但是他们不会获得导师指导或认证证书，无法提交最终项目来获取反馈。

在此试验中，优达学城测试了一项变化，如果学生点击“开始免费试学”，系统会问他们有多少时间投入到这个课程中。如果学生表示每周 5 小时或更多，将按常规程序进行登录。如果他们表示一周不到 5 小时，将出现一条消息说明优达学城的课程通常需要更多的时间投入才能成功完成，并建议学生可免费访问课程资料。在这里，学生可选择继续进行免费试学，或免费访问课程资料。

我们假设这会为学生预先设定明确的期望，从而减少因为没有足够的时间而离开免费试学，并因此受挫的学生数量，同时不会在很大程度上减少继续通过免费试学和最终完成课程的学生数量。如果这个假设最后为真，优达学城将改进整体的学生体验和提升导师为能够完成课程的学生提供帮助支持的能力。

分组单位为 cookie，尽管学生参加的是免费试学，但在登录后他们的用户 id 便被跟踪。同一个用户 id 不能两次参加免费试学。对于不参加免费试学的用户，他们的用户 id 不会在试验中被跟踪，即使他们在访问课程概述页面时登录了网站。

## 度量

你会选择以下哪个度量来对此试验进行测量，为什么？对于选择的每个度量，请说明你是否会将它用作不变度量或评估度量。每个度量的实际显著性边界——即在它成为有意义的业务变化前必须观察的差异，在括号中给出。所有实际显著性边界作为绝对变化给出。

任何提及“唯一 cookie”的地方，其唯一性按天决定。（在两个不同日期进行访问的同一个cookie 将计算两次。）用户 id 自动唯一，因为网站不允许同一个用户 id 参与两次。

• cookie 的数量：即访问课程概述页面的唯一 cookie 的数量。（d 最小 =3000）

• 用户 id 的数量：即参与免费试学的用户数量。（d 最小 =50）

• 点击次数：即点击“开始免费试学”按钮的唯一 cookie 的数量（在免费试学筛选器触发前发生）。（d 最小 =240）

• 点进概率：即点击“开始免费试学”按钮的唯一 cookie 的数量除以查看课程概述页的唯一 cookie 的数量所得的比率（d 最小 =0.01）

• 总转化率：即完成登录并参加免费试学的用户 id 的数量除以点击“开始免费试学” 按钮的唯一cookie 的数量所得的比率。（d 最小 =0.01）

• 留存率：即在 14 天的期限过后仍参加课程（因此至少进行了一次付费）的用户 id数量除以完成登录的用户 id 的数量。（d 最小 =0.01）

• 净转换率：即在 14 天的期限后仍参与课程的用户 id 的数量（因此至少进行了一次付费）除以点击了“开始免费试学”按钮的唯一 cookie 的数量所得的比率。（d 最小 =0.0075）

## 一、试验设计
### （一）指标选择
#### 1、列出你将在项目中使用的不变指标和评估指标。

不变指标：选用Number of cookies、Number of clicks和Click-through-probability
评估指标：选用 Gross Conversion 和 Net Conversion

#### 2、对于每个指标，解释你为什么使用或不使用它作为不变指标或评估指标。此外，说明你期望从评估指标中获得什么样的试验结果。

Number of cookies：该数据产生于用户登录网站，不会因实验组中新增的页面而发生变化，因此选为不变指标。
Number of user-ids：该数据产生于试验发生之后，会受到试验的影响，所以它不能作为不变指标，但它可以作为评估指标。但是，由于实验组和对照组的cookie数量不一定完全相同，也就是说两组中用户ID数量的不同可能是由于实验的影响，也可能是由于两组cookie的不同造成的。所以使用用户ID数量的区别不能够很好的评估试验的效果。在一个比例化的评估指标（总转化率）存在的情况下，我们可以不选择用户ID的数量作为评估指标。综上，用户ID既不是不变指标，也不是评估指标。
Number of clicks：该数据产生于用户点击"免费试用课程"这个事件，不会因实验组中新增的页面而发生变化，因此选为不变指标。
Click-through-probability：该指标是Number of clicks与Number of cookies的比例，两个不变指标之商也必然是不变指标。
Gross conversion：为完成登录并报名参加免费试用的用户ID的数量与点击"开始免费试用"按钮的唯一cookie的数量之比。通过比例指标的运用，可以较好的弱化试验组与对照组之间因cookies数量不完全相同所造成的影响，因此选为评估指标。
Retention：是参加了"免费试用课程"14天以后自动收费的用户ID数量与注册参加"免费试用课程"的用户ID数量的比例。但是，本实验的unit of diversion是cookies，而Retention的unit of analysis是user-id，unit of diversion与unit of analysis不相同，无法确保引流的一致性，从而造成分析变异性与经验变异性不匹配，若时间允许，该指标可采用经验方法计算，本文拟直接舍弃。
Net conversion：是参加了"免费试用课程"14天以后自动收费的用户ID数量与点击"开始免费试用"按钮的唯一 cookie 的数量之比。该指标同样受到试验影响且为比例指标，因此选为评估指标。

期望从评估指标中获得的试验结果：
若试验组的Gross conversion显著低于控制组，则表明新增的页面能够有效阻止学习时间不足的用户进行注册；
若试验组的Net conversion不显著低于控制组，则表明新增的页面使付费用户减少的程度不大。

### （二）测量标准偏差
#### 1、列出你的每个评估指标的标准偏差。

Gross conversion的Standard deviation 为 0.0202。
Net conversion的Standard deviation为0.0156。

#### 2、对于每个评估指标，说明你是否认为分析估计与经验变异是类似还是不同（如果不同，在时间允许的情况下将有必要进行经验估计）。简要说明每个情况的理由。

本实验选择的分组单元是cookie，评估指标Gross conversion及Net conversion的分析单元也均为cookie，可以确保引流的一致性，所以这两个指标的分析差异性匹配经验差异性。

### （三）规模
#### 1、样本数量和功效，说明你是否会在分析阶段使用 Bonferroni 校正，并给出实验正确设计所需的页面浏览量。

不会在分析阶段使用Bonferroni校正，因为Gross conversion和Net conversion具有关联性，使用Bonferroni校正得到的结果过于保守。
使用alpha=0.05，（1-beta）=0.8。
Gross conversion：dmin=0.01，Baseline conversion rate = 20.625%，根据在线计算器得到一组实验所需Gross conversion的样本量为25835，两组实验所需的样本量为51676，然后转化为需要的页面浏览量 = 51676/0.08 = 645950
Net conversion：dmin = 0.075，Baseline conversion rate = 10.93125%，根据在线计算器得到一组实验所需Net conversion 的样本量为27413，两组实验所需的样本量为54826，然后转化为需要的页面浏览量 = 54826/0.08 = 685325
考虑到所需页面浏览量要同时覆盖两个指标，因此选择两个页面浏览量中较大的一个，即685325。

#### 2、持续时间和暴光比例。说明你会将多少百分比的页面流量转入此试验，以及鉴于此条件，你需要多少天来运行试验。

一般来说，A/B testing的实验时间是持续几个星期至一个月之内。根据所需的页面浏览量（685325）及每天的页面浏览量（40000），曝光的流量部分为57.2%时所需天数为30天，符合要求。因此选择曝光比例为57.2%，试验持续时间为30天。

#### 3、说明你选择所转移流量部分的原因。你认为此试验对优达学城来说有多大风险？

不选择对所有流量开展实验的原因主要是出于以下几个方面：
一是安全性。推出这个新的页面弹窗，我们不确定它是否能在所有浏览器中正常运行，也不确定用户将有什么反应，所以选择仅向部分用户开展实验。
二是随机分配分组单元时，为了避免异常数据（例如节假日等等）对试验结果的误导，也倾向于压缩发送流量比例，在合理范围内延长持续时间，从而尽可能的了解用户在不同日期的差异。

对此实验，优达学城并没有太大的风险，因为：
第一，即使学生每周学不到五小时，他们只是被页面的变更提醒引导到了另外的一个页面，如果今后有需要学生仍然可以进入免费试学、登陆并可能完成课程，不会因此影响用户使用网站的习惯；
第二，没有在页面展示上有过大的改动，不会对用户产生感情上的冲击，用户也不需要花长时间去适应页面的改变。
第三，该试验没有关于数据库及后台的改变，不用担心数据的丢失及由于后台的失误导致网页奔溃用户无法访问网页等大问题。
第四，此试验也不会对用户的个人信息安全造成风险，因为不论网页是否增加了提醒，用户在确认参加免费试学时都需要输入信用卡信息，而很明显系统一定会保护用户的个人信息。
第五，该试验同样也没有道德上的风险。

## 二、试验分析
#### （一）合理性检查。对于每个不变指标，对你在95%置信区间下期望观察到的值、实际观察的值及指标是否通过合理性检查给出结论。

Number of cookies：控制组总计有345543个观测值，试验组总计有344660个观测值。对于每一个观测值，它被发送至控制组和试验组的几率均为50%，且事件之间相互独立，因此符合二项分布特征。在alpha = 0.05水平下，SE = ((0.5*0.5) / (N-con + N-exp))^0.5 = 0.0006，margin of error = SE * Z-score = 0.0006 * 1.96 = 0.0012，围绕0.5为中心的置信区间为(0.4988,0.5012)。实际观测值= N-con / (N-con + N-exp) = 0.5006，位于置信区间之内，因此Number of cookies通过Sanity check。
Number of clicks：控制组总计有28378个观测值，试验组总计有28325个观测值。对于每一个click事件，它被发送至控制组和试验组的几率均为50%，且事件之间相互独立，因此符合二项分布特征。在alpha = 0.05水平下，SE = ((0.5*0.5) / (N-con + N-exp))^0.5 = 0.0021，margin of error = SE * Z-score = 0.0021 * 1.96 = 0.0041，围绕0.5为中心的置信区间为(0.4959,0.5041)。实际观测值= N-con / (N-con + N-exp) = 0.5005，位于置信区间之内，因此Number of clicks通过Sanity check。
Click-through-probability：控制组的P-con = X-con / N-con = 0.0821，试验组的P-exp = X-exp / N-exp = 0.0822。试验组与控制组的差异：P-exp - P-con = 0.0822 - 0.0821 = 0.0001。两组的合并概率P-pool = (X-con + X-exp) / (N-con + N-exp) = 0.0822，合并标准误差SE-pool = (P-pool * (1 - P-pool) * ( 1/N-con + 1/N-exp))^0.5 = 0.0007，则Margin of error = SE-pool * Z-score = 0.0007 * 1.96 =0.0013，围绕0为中心的置信区间为(-0.0013, 0.0013)。两组的差异0.0001位于置信区间之内，因此Click-through-probability通过Sanity check。
所有不变指标均通过Sanity check。

#### （二）结果分析
#### 1、效应大小检验。对于每个评估指标，对试验和对照组之间的差异给出 95% 置信区间。说明每个指标是否具有统计和实际显著性。

Gross conversion：
P-pool = (X-con + X-exp) / (N-con + N-exp) = (3785+3423) / (17293+17260) = 0.2086
SE-pool = (P-pool*(1-P-pool)*(1/N-con + 1/N-exp))^0.5 = 0.0044
Margin of error = SE-pool * Z-score = 0.0086
d-hat = P-exp - P-con = X-exp/N-exp - X-con/N-con = -0.0206
CI: ( -0.0291 , -0.0120 )
置信区间不包括0，具有统计显著性，不包含最小实质显著性边界-0.01，具有实质显著性。

Net conversion:
P-pool = (X-con + X-exp) / (N-con + N-exp) = (2033+1945) / (17293+17260) = 0.1151
SE-pool = (P-pool*(1-P-pool)*(1/N-con + 1/N-exp))^0.5 = 0.0034
Margin of error = SE-pool * Z-score = 0.0067
d-hat = P-exp - P-con = X-exp/N-exp - X-con/N-con = -0.0049
CI: ( -0.0116 , 0.0019 )
置信区间包括0，不具有统计显著性，包含最小实质显著性边界-0.0075，不具有实质显著性。

#### 2、符号检验。对于每个评估指标，使用每日数据进行符号检验，然后报告符号检验的 p 值以及结果是否具有统计显著性。

Gross conversion:
将每日试验组与控制组的Gross conversion做差，为正值的有4天，全部观测天数为23天，使用在线计算器得到双尾p值为0.0026，小于alpha = 0.05，因此具有统计显著性。

Net conversion:
将每日试验组与控制组的Net conversion做差，为正值的有10天，全部观测天数为23天，使用在线计算器得到双尾p值为0.6776，远大于alpha = 0.05，因此不具有统计显著性。


#### 3、汇总。说明你是否使用了 Bonferroni 校正，并解释原因。若效应大小假设检验和符号检验之间存在任何差异，描述差异并说明你认为导致差异的原因是什么。

未使用Bonferroni校正。因为Gross conversion与Net conversion具有相关性，而Bonferroni校正在此种情况下过于保守。此外，如果要进行Bonferroni校正的话，除了判断指标是否相互独立，我们还要判断几个评估指标之间是"与"还是"或"的关系。如果指标之间是相互独立的，但是得出最终结论是"与"的关系，这样我们进行Bonferroni校正也会过于保守。在本试验中我们希望这两个试验结果同时满足，因此也不需要使用Bonferroni校正。
效应大小假设检验与符号检验之间未存在差异。

## 三、建议

Gross conversion具有统计和实际显著性，是我们希望看到的结果。但是Net conversion的置信区间包含负数，根据此处的计算结果(-0.0116, 0.0019)，也就是说有很大的概率Net conversion会减少，并且有一定的概率Net conversion的减少会超过实际显著性0.0075。因此我们无法说明"降低的程度不大"。所以不建议发布该变更。


## 四、后续试验

对你会开展的后续试验进行概括说明，你的假设会是什么，你将测量哪些指标，你的转移单位将是什么，以及做出这些选择的理由。

在此试验的基础上，对于那些参加了14天免费课程却点击取消的用户增加弹窗，询问是否愿意接受更为专业的教练辅导和项目审阅服务，并在弹窗中附往期毕业学员成功就职名企的简述和详细页面链接。若点击是，提示学员将在14天免费试用到期后自动扣款，若点击否，则关闭弹窗确认取消课程。
假设：参加免费课程的学员有可能因为课程内容难度过大而放弃，也有可能因为学习课程后能否顺利就业等存有疑虑。通过提示用户付费后能够接受更为专业的辅导和服务及往期毕业学员成功就职名企的信息，能够有效打消拟取消课程用户的疑虑，增加试用用户付费比例。
测量指标包括：
1.	参加14天免费课程的user-ids数量
2.	14天免费课程结束后自动扣费的user-ids数量
3.	付费率：即14天免费课程结束后自动扣费的user-ids数量占参加14天免费课程的user-ids数量的比例
转移单位：由于以上测量指标全部为user-ids的数量，所以转移单位自然选择user-ids的数量。

