# PRD__FinalProject

### Product Requirements
Target release|2018/12/31
:---|:---
Epic|一个能够准确、高效预约门诊的APP（以广东省惠州市为试行点）
Document status| DRAFT
Document owner| Wu Xindan
Designer/Developer| Wu Xindan
AI|推荐系统尝试——根据用户输入内容推荐挂号科室（基于内容的推荐方法）
API|高德地图API——[搜索POI](https://lbs.amap.com/api/webservice/guide/api/search/)、[路径规划](https://lbs.amap.com/api/webservice/guide/api/direction)、[输入提示](https://lbs.amap.com/api/webservice/guide/api/inputtips)

### Background and strategic fit
- 背景：医院是每天人流最多的地方之一；大多数患者需要1-4h的等候才能进行最基本的诊断。目前惠州没有公众号或APP对市区所有医院门诊的资料做整合，而低效的门诊效率为市民就医带来诸多不便。
- 战略契合：通过对各个医院的数据进行整合，以内容为主的推荐抓取高德地图API对每个医院位置进行定位，为市民提供最便捷、高效的就医方案选择。

### Goals
- 通过智能推荐为用户选择合适的医院（距离/专科水平）、正确的挂号科（E.g. 当病人需要看乳腺增生时，需要挂外科而不是妇科）
- 为用户省掉不必要的等候时间

## Product prototype


### Assumptions
- 用户所在地为广东省惠州市
- 用户通过手机端使用此功能
- 各医院公开门诊就医的详细情况（E.g.:科室，医生安排，上班时间，挂号费，预计等候时间等）

### Requirements
|#|Title|User story|Importance|Notes
:---|:----|:-----|:------|:------
1|准确挂号|患者复查乳腺结节时按常识挂妇科就诊，排队半小时后被医生告知需重新挂外科就诊。|通过APP，可以根据不同的症状帮助用户进行科室选择，提高效率。|E.g.:发烧时不同的紧急症状需要正确判断挂内科还是呼吸科，以求及时高效的诊断。/乳腺科在大多数人的常识里属于妇科，但事实上，大多数医院有专门的外科——乳腺外科的设置。
2|缩短耗时|患者早起7点出门，20Min到达医院，挂号排到16，初步诊断的排队时长长达46Min。此后被告知挂错科，重新挂号后总排队时长长达3H。|通过APP告知患者排队等候所需时间及预计诊断开始时间，减少不必要的时间消耗，提高就诊效率。|选择就诊科室及医生后显示排队人数，等候时间，预计开始时间等细节。

### Questions
|Question|Outcome
:----|:----
整合医院门诊资料|便于用户了解各医院的专科水平，在需要时能第一时间做出最合适的选择
智能推荐|
提供线上门诊挂号|提供更加便利的挂号方式，避免用户早起排队挂号
提供当前排队人数信息及预测就诊时间|用户了解自己所在序号，通过合理预测能够更加合理的安排时间。

### Not doing
- 线上初步诊断：取消该功能，避免因数据不够庞大而带来的误诊或耽误用户的诊断治疗
- 路线规划：取消该功能；加入导航过于繁杂，目前的知识水平或许不够操作庞大复杂的输入输出。
- 扩大覆盖率：下一版希望尝试加入多个市区，扩大APP的使用率（除惠州市外，加入其他城市，争取更多的用户及流量）

## Manifest
[高德地图搜索POI](https://lbs.amap.com/api/webservice/guide/api/search/)
[高德地图API-输入提示](https://lbs.amap.com/api/webservice/guide/api/inputtips)
