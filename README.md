# AI算法创新赛-人车目标检测竞赛

## 赛题介绍

### 1.赛题名称

人车目标检测竞赛

### 2.赛题背景

随着时代的进步,视觉目标检测技术在生产生活中发挥着越来越重要的作用。人、车是现代社会最为重要的组成对象，实现人、车目标的精确快速检测对构建智慧城市和平安社会具有重要意义。本赛题旨在基于TPU平台对真实场景下采集的行人和车辆图片进行目标检测与识别。

### 3.赛题任务

本次赛题提供的数据集中包含3018张真实场景下的行人和车辆图片，其中训练集包含2885张带有标签的图片，测试集包含133张不带有标签的图片。参赛者需要在训练集上自行训练网络，检测并识别测试集中三类目标：机动车、行人和非机动车。

### 4.数据介绍

数据集下载链接：http://219.142.246.77:65000/sharing/q2c8cbYZG

本次赛题提供的数据集包含image和label两个文件夹。image文件夹由2885张训练集和133张测试集组成；label文件夹中包含2885个带有对应每张图片全部标签的txt文件。标签共包括三种类别：机动车、行人和非机动车。数据标签格式如下：

```
<class_id> <ct_x> <ct_y> <w> <h>
```

标签对应id：0:car, 1:person, 2:bike

E.g. 

```
0 0.4284 0.6977 0.2984 0.5361 
1 0.2784 0.6125 0.0380 0.0361 
2 0.6706 0.7072 0.0255 0.0645
```

### 5.提交要求

参赛者在训练完成并对测试集图片进行推理后，将测试集图片的检测结果以与训练集标签同名的txt文件保存，并上传至result_submit/文件夹下，具体保存方式见result_submit/README.md。上传格式实例如下所示：

```
<class_name> <confidence> <left> <top> <right> <bottom>
```

E.g.

```
car 0.399786 3 642 125 690
person 0.395193 1549 621 1686 796
bike 0.386811 373 647 395 701
```

P.S. 我们在scripts/文件夹中为选手提供脚本，可将`<class_id> <confidence> <ct_x> <ct_y> <w> <h>` 格式转换为提交所需的 `<class_name> <confidence> <left> <top> <right> <bottom>` 格式。

1. 将检测结果保存至input/detection-results

2. 将测试图片保存至images/

3. 运行如下指令

   ```
   python3 convert_gt_yolo.py
   ```
选手提交成绩后，若审核无误将会每日于result_submit/readme.md中更新分数，每周于赛事官网页面更新分数
### 6.评分标准

**初赛：**

通过mAP(mean Average Precison)指标评测模型精度。mAP即各类别APIoU=0.5的平均值，其中APIoU=0.5为IoU阈值为0.5 的平均精度。初赛最终得分计算公式为：score=mAP*100，分数高者为优。

**复赛：**

1、通过与初赛相同的mAP(mean Average Precison)指标评测模型精度。

2、通过模型推理时间i_time评测模型性能，i_time为测试集图片推理的平均时间，单位为ms。

3、最终得分计算公式为：score=mAP*100+(1000-i_time)*0.1，分数高者为优。

## 赛程安排

本次大赛分为报名&组队、初赛、复赛、决赛四个阶段，具体安排和要求如下：

**报名&组队**（2022.10.1-2022.11.20）

1. 报名方式：登录算能官网，注册个人信息，报名参赛。个人报名信息要求准确有效，否则会被取消参赛资格。大赛不收取任何报名费用。
2. 组队说明：每支参赛队伍由1-3人组成，只需队长在官网报名，由队长填写《参赛队伍信息表》提交至算能邮箱da.teng@sophgo.com。报名截止之后，将不再允许添加或更改任何队伍成员。
3. 竞赛官方渠道主要包括：
   - 算能官网：www.sophgo.com
   - 微信公众号：SOPHGO算能
   - 竞赛官方交流群

**初赛**（2022.10.1-2022.11.30）

1. 报名成功后，参赛队伍通过大赛官网下载数据集，本地调试算法，在线提交结果。若参赛队伍在一天内多次提交结果，新结果版本将覆盖旧版本。
2. 初赛采用AB榜，提供训练数据集，供参赛选手训练算法模型；提供测试数据集，供参赛选手提交评测结果参与排名。
3. 初赛A榜：10月1日10:00-11月26日20:00。每队每天有3次提交结果的机会，系统进行实时评测并返回成绩，排行榜每小时进行更新，按照评测指标从高到低排序。排行榜将选择参赛队伍在本阶段的历史最优成绩进行排名展示。
4. 初赛A榜淘汰：11月27日12:00，初赛A榜未产出成绩队伍或未按要求完成实名认证队伍，将被取消初赛B榜参赛资格。
5. 初赛B榜：11月28日10:00-20:00。系统将在11月27日20:00更换测试数据，参赛队伍需再次下载数据文件。本阶段提供2次提交结果的机会，系统进行实时评测并返回成绩，排行榜每小时进行更新，并选择参赛队伍在本阶段的历史最优成绩进行排名展示。初赛提交截止时间11月28日20:00。
6. 初赛结束，以B榜成绩作为初赛成绩依照，要求TOP30团队提交代码审核，代码提交截止时间11月10日12:00。组委会将审核并取消存在人工标注、相互抄袭等行为队伍的比赛资格，晋级空缺名额后补。初赛成绩符合要求且通过实名认证的排名前20名的参赛队伍将进入复赛。

**复赛**（2022.12.1-2022.12.31）

1. 复赛阶段所需的测试数据、SDK和Docker镜像通过算能官网下载，要求参赛选手将训练好的本地模型和测试数据在提供的TPU平台上进行推理。
2. 复赛评测：12月6日-12月31日。复赛以在TPU平台上推理的精度和性能作为评测标准。12月6日-12月10日，系统每天提供3次实时评测，供选手进行提交测试，排行榜不展示排名情况。12月11日-12月31日，A榜系统每天提供3次实时评测，B榜系统每天提供1次实时评测，每日更新排行榜，按照评测指标从高到低排序。排行榜将选择参赛队伍在本阶段的历史最优成绩进行排名展示。复赛提交截止时间12月31日12:00，排行榜最后一次刷新时间是1月3日23:00。
3. 复赛结束前的12月27日-12月31日，选手需保证排行榜最优成绩对应提交的是完整的端到端代码（包含数据处理和模型训练等）。复赛结束后，若提交的代码不是完整代码，会直接淘汰。如果最后一周出现无法复现的最优成绩可在复赛结束前联系组委会协助删除最优记录，复赛结束后不再受理。
4. 复赛结束，以榜单成绩作为复赛成绩依照。组委会将对排行榜TOP10参赛队伍进行最优提交成绩的模型和完整代码审核（包含数据处理和模型训练）。随后，组委会将审核榜单预测结果并与最优提交进行比对，要求能复现榜单最优成绩，不接受随机成绩。对于未提交、复现未成功或审核不通过的队伍，将取消决赛资格和比赛奖励。最终，审核通过的队伍，取复赛成绩换算分值，复赛得分排名前6的参赛队伍将晋级决赛。

注：复赛得分公式=(x-xmin) / (xmax-xmin)，其中x为原始得分，xmin为第30名的得分，xmax为第一名的得分。

**决赛**（2023年1月1日-1月15日）

1. 决赛将以答辩会的形式进行，晋级决赛团队需提前准备答辩材料，包括路演PPT、参赛总结、算法核心代码。
2. 答辩会现场，每支队伍面对评委有15分钟的路演时间和10分钟的答辩时间。评委将根据选手的技术思路、理论深度和现场表现进行综合评分。
3. 决赛分数将根据参赛队伍的算法成绩和答辩成绩加权得出。评分权重：复赛成绩占70%，决赛答辩成绩占30%。综合复赛、决赛的成绩加权，评选出大赛奖项。
4. 决赛时间和其他安排另行通知。

## 参赛对象

本次大赛面向全球开放，不限年龄国籍，高等院校在校学生（包括高职高专、本科、研究生）以及科研机构和企业从业人员均可参赛。

注：大赛主办和技术支持单位如有机会接触赛题和相关数据的人员不允许参赛；

## 奖项设置

1. **初赛奖项**

   初赛最终排行榜的前10名队伍颁发初赛名次证书。

2. **复赛与决赛奖项**

   赛道的奖金池均为50万元人民币，所有奖金均为税前金额。

   | 奖项名称 | 数量 | 对象         | 奖励方法                        |
   | -------- | ---- | ------------ | ------------------------------- |
   | 一等奖   | 1    | 决赛第1名    | 奖金2万元人民币，颁奖获奖证书   |
   | 二等奖   | 2    | 决赛第2-3名  | 奖金1.5万元人民币，颁奖获奖证书 |
   | 二等奖   | 3    | 决赛第4-6名  | 奖金8千元人民币，颁奖获奖证书   |
   | 优秀奖   | 14   | 复赛第7-20名 | 奖金2千元人民币，颁奖获奖证书   |

## 大赛组织

主办单位：TPU编程竞赛委员会

## 赛事声明

1. 为了确保整个大赛顺利、公正地进行，以及保证参赛选手的合法权益，参赛选手报名时应阅读和确认大赛官网上的参赛协议，自觉遵守协议规定。
2. 在大赛举办过程中，竞赛规程可能会有少量的变更和调整，所有内容均以大赛官网为准。
3. 本大赛规程的最终解释权归TPU编程竞赛委员会所有。
