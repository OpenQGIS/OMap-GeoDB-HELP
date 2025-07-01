# `Sino-GeoDB 「九州」地理数据库` 数据解析

> [Sino-GeoDB 「九州」地理数据库](https://his.lreept.space/openqgis/omap-geodb/)，是一款完全基于开源数据库OpenStreetMap（简称OSM）进行本土化适配的华夏九州范围的综合类地理数据库。

</br>

### 1.什么是「九州」地理数据库？

九州地理数据库（全称：Sino-GeoDB），属于OMap-GeoDB（中文：超常规地理数据）的分支之一，其目的是创建一个完整华夏九州范围的**免费开源**的地理数据库，帮助大家降低数据获取门槛。

</br>
</br>

### 2.「九州」地理数据库的优势？

#### 1). ​​华夏全域完整覆盖
      
`Sino-GeoDB「九州」地理数据库` 依据官方地理边界标准构建，全面覆盖包括港澳台地区、南海诸岛等**全部法定领土范围**。所有数据均为经过**脱敏处理**，确保在保障信息安全的前提下，实现对华夏全域的完整表达。

#### 2). 最新的日期
     
a. 目前所谓的“全国数据库”下载，这些数据早已停止更新，其时间戳落后（数据仅截止于2024.8），严重影响了数据的时效性和可用性。
     
b. 分省数据虽在持续更新，其覆盖范围有限，且部分省份的边界数据存在误差，难以支撑全国尺度的统一应用。
     
c. 华夏的GISer缺乏一个覆盖全国、结构统一、更新及时的边界数据产品，`Sino-GeoDB「九州」地理数据库` 完美地填补了这一空白。

#### 3). 更强的数据属性
     
在保留常规标签（如名称、类型等）的基础上，数据库以制图应用为核心出发点，补充了多项实用属性字段（分类数据、高度、层数、桥隧名），显著提升了数据的可视化表现力与分析适配性。（详细字段说明详见文档后文）

</br>
</br>

## 九州数据库与GPKG（地理包）

### **产品体系：**

九州地理数据库当前共包含**15小项**合计**7大类**。

| 数据标准名               | 数据类别 | 数据结构                                               |
| ------------------------ | -------------- | ------------------------------------------------ |
| oData-air_system           | 空中系统 | 【线】机场跑道、缆车系统                         |
| oData-building           | 建筑数据 | 【面】建筑数据                                         |
| oData-land_series       | 土地数据 | 【点】山峰、温泉；【线】山脊；【面】土地利用；【面】自然覆盖 |
| oData-railway_series    | 铁路数据 | 【点】铁路、地铁站点；【线】详细标签轨道线               |
| oData-roads              | 道路数据 | 【线】道路数据                                         |
| oData-transport    | 交通     | 【点】电塔、变压器；【线】电线；【面】变电站               |
| oData-water&damn_series | 水系数据 | 【线】水系；【线】大坝；【面】水系面；【面】大坝             |

### **数据格式：**

QGIS与OSM同属于开源产品，数据首发格式以`*.GPKG（地理包）`进行发布。支持拖入QGIS即可一键加载。更多内容关于GPKG可以访问B站视频`[https://www.bilibili.com/video/BV1gM4m167PS]`。

### **读取和转换：**

1. 读取|将gpkg文件直接拖拽至QGIS中即可完成加载；ArcGIS Pro 3.0也支持对gpkg直接加载。
2. 转换|在QGIS中加载gpkg后，在需要转换的图层`【右键】`>>`【导出】`>>`【要素另存为】或【选中要素另存为】`，在弹出窗口的`【格式】`项选择`【ESRI形状文件】`**即可导出为SHP文件**。
3. **警告**|SHP文件的大小可能远超过gpkg文件本身的大小，请注意计算机磁盘容量。

## 九州数据库各类说明

### 目录

1. [🛫 空中系统](#section1)
2. [🏘️ 建筑数据](#section2)
3. [🌳 土地数据](#section3)
4. [🚉 铁路数据](#section4)
5. [🚘️ 道路数据](#section5)
6. [🚘️ 交通设施](#section6)
7. [🌊 水系大坝](#section7)

</br>

## 1.🛫 空中系统<a id="section1"></a>

| 数据标准名               | 数据类别 | 数据结构                      |
| -------------------------- | ---------- | -------------------------------------------------------- |
| oData-air_system           |空中系统 | 【线】机场跑道;【线】缆车系统 |

### 1.1 机场跑道数据示范

|序号| 字段名    | 属性值         | 解释                 |
| :------: | :-----------: | :----------------: | :---------------------- |
|1| ~~name~~      | ~~null~~             | ~~空值~~   |
|2| ~~aerialway~~ | ~~null~~             | ~~空值~~ |
|3| aeroway   | runway/taxiway…    | 机场跑道、滑行道……            |
|4| ref       | 15/33             | 跑道编号             |
|5| construct | T/F           | T为在建            |

#### 1.1.1 aeroway字段详解

| 英文值           | 中文翻译         | 含义说明                                      |
|------------------|------------------|-----------------------------------------------|
| runway           | 跑道             | 飞机起飞和降落的主要跑道                      |
| stopway          | 停止道           | 用于飞机因紧急情况中断起飞的延长段            |
| taxiway          | 滑行道           | 连接跑道和停机位、机库的地面通行路线          |
| parking_position | 停机位           | 飞机停放位置，通常在航站楼附近                |
| jet_bridge       | 登机桥           | 连接航站楼与飞机的伸缩通道                    |
| highway_strip    | 公路跑道         | 用作临时飞机起降的直线路段公路                |

### 1.2 缆车数据示范

|序号| 字段名    | 属性值         | 解释                 |
| :------: | :-----------: | :----------------: | :----------------- |
|1| name      | 金花桥索道 | 索道名 |
|2| aerialway | gondolacable_car,gondola | 各类索道类型 |
|3| ~~aeroway~~   | ~~null~~          | ~~空值~~            |
|4| ~~ref~~       | ~~null~~           | ~~空值~~              |
|5| construct | T/F        | F为已建成            |

#### 1.1.2 aerialway字段详解

| 英文值           | 中文翻译         | 含义说明                                      |
|------------------|------------------|-----------------------------------------------|
| cable_car        | 缆车             | 通常为大型车厢，可运载多人，运行在两条缆索上         |
| gondola          | 吊厢缆车         | 封闭式小车厢，通常连续运行，常用于旅游和滑雪场       |
| mixed_lift       | 混合式索道       | 吊椅和吊厢混合使用的索道                        |
| chair_lift       | 吊椅缆车         | 开放式椅子，一般用于滑雪场，乘客坐在椅子上上升       |
| drag_lift        | 拖曳式缆车       | 乘客被拖着向上滑行的索道通用类型                   |
| t-bar            | T型拖曳缆车      | T 形杆件拖曳乘客，常用于滑雪                     |
| j-bar            | J型拖曳缆车      | J 形杆件拖曳乘客，通常单人使用                    |
| platter          | 圆盘拖曳缆车     | 圆盘拖杆夹在双腿之间，乘客站立滑行上坡              |
| rope_tow         | 拖绳缆车         | 抓住移动的绳索被拖拽上坡，常用于初学滑雪者           |
| magic_carpet     | 魔毯传送带       | 像传送带一样的装置，站在其上移动，适合初学者使用     |
| zip_line         | 高空滑索         | 利用滑轮在高空缆索上快速滑行                      |
| goods            | 货运缆车         | 专门运送货物的缆车，不载客                       |

</br>

## 2.🏘️ 建筑数据<a id="section2"></a>

建筑数据：包含建筑物理楼层数`levels`、物理高度`height `、物理空间位置`location`，增加了建筑的符号图层`layer`更适合建筑叠加渲染。

### 2.1 建筑数据示例

| 字段名   | 属性值         | 解释                                   |
| :----------: | :----------------: | :---------------------------------------- |
| name     | 锦城广场       | 建筑名                                 |
| building | subway_sation | 地铁站建筑               |
| levels   | 1              | 建筑楼层数                             |
| height   | 3              | 建筑高度（单位米）                               |
| layer    | -2             | 建筑所在的图层顺序，针对重叠建筑使用   |
| location | underground    | 建筑物的物理空间位置（地下、水上……） |

### 2.2 建筑数据分类

#### 2.2.1 BldgClass 字段解析

建筑数据采用`BldgClass（一级分类）`和`building（二级分类）`的结构做支撑，其中`BldgClass（一级分类）`共分为10大类：

|序号| BldgClass                | 建筑一级分类      |
|---|-------------------------|------------------|
| 1 | Accommodation           | 住宅             |
| 2 | Commercial              | 商业建筑         |
| 3 | Religious               | 宗教建筑         |
| 4 | Civic/amenity           | 便民建筑         |
| 5 | Agricultural/plant production | 农业建筑   |
| 6 | Sports                  | 体育建筑         |
| 7 | Storage                 | 储藏建筑         |
| 8 | Transport               | 停车/车棚建筑    |
| 9 | Power/technical buildings | 特殊建筑  |
| 10 | Other buildings         | 其他建筑         |

#### 2.2.2 building 字段详解

> ##### 1.Accommodation 住宅建筑
> 
> apartments（公寓楼）, barracks（营房）, bungalow（平房）, cabin（小木屋）, detached（独立住宅）, dormitory（宿舍）, farm（农舍）, ger（蒙古包）, hotel（酒店）, house（房屋）, houseboat（船屋）, residential（住宅类建筑）, semidetached_house（联排双拼住宅）, static_caravan（固定式房车）, stilt_house（高脚屋）, terrace（排屋）, tree_house（树屋）, trullo（特鲁洛圆顶屋）

> ##### 2.Commercial 商业建筑
> 
> commercial（商业建筑）, industrial（工业建筑）, kiosk（亭子/小卖部）, office（办公楼）, retail（零售建筑）, supermarket（超市）, warehouse（仓库）

> ##### 3.Religious 宗教建筑
> 
> religious（宗教建筑）, cathedral（大教堂）, chapel（小教堂）, church（教堂）, kingdom_hall（王国聚会所）, monastery（修道院）, mosque（清真寺）, presbytery（神父住所）, shrine（神殿/圣地）, synagogue（犹太教堂）, temple（庙宇/寺庙）

> ##### 4.Civic/amenity 便民建筑
> 
> bakehouse（烘焙屋）, bridge（桥梁建筑）, civic（市政建筑）, college（学院）, fire_station（消防站）, government（政府大楼）, gatehouse（门卫室）, hospital（医院）, kindergarten（幼儿园）, museum（博物馆）, public（公共建筑）, school（学校）, toilets（公共厕所）, train_station（火车站）, transportation（交通设施建筑）, university（大学）

> ##### 5.Agricultural/plant production 农用建筑
> 
> barn（谷仓）, conservatory（暖房/温室）, cowshed（牛棚）, farm_auxiliary（农场附属建筑）, greenhouse（温室）, slurry_tank（粪液池）, stable（马厩）, sty（猪圈）, livestock（牲畜棚舍）

> ##### 6.Sports 体育建筑
> 
> grandstand（看台）, pavilion（展馆）, stable（马厩）, farm_auxiliary（农场附属建筑）, farm_auxiliary（农场附属建筑）, barn（谷仓）

> ##### 7.Storage 仓储建筑
> 
> allotment_house（农舍）, boathouse（船屋）, hangar（机库）, hut（小屋）, shed（棚屋）

> ##### 8.Transport 交通建筑
> 
> carport（车棚）, garage（车库）, garages（车库，复数）, parking（停车场）, train_station（火车站）, subway_station（地铁站）, tram_station（有轨电车站）, bus_station（公交车站）

> ##### 9.Power/technical buildings 特殊建筑
> 
> digester（沼气池）, service（设备间）, tech_cab（技术柜）, transformer_tower（变电站）, water_tower（水塔）, storage_tank（储罐）, silo（筒仓）

> ##### 10.Other buildings 其他建筑
> 
> beach_hut（海滩小屋）, bunker（地堡）, castle（城堡）, construction（施工建筑）, container（集装箱房）, guardhouse（岗亭）, military（军事建筑）, outbuilding（附属建筑）, pagoda（宝塔）, quonset_hut（拱形活动屋）, roof（屋顶建筑）, ruins（废墟）, ship（船屋）, tent（帐篷）, tower（塔楼）, triumphal_arch（凯旋门）, windmill（风车）, destroyed（已毁建筑）

</br>

## 3.🌳 土地系列<a id="section3"></a>

| 数据标准名               | 数据类别 | 数据结构       |  
| -------------------------- | ---------- | ----------------    |  
| oData-land_series       | landuse_polygon | 【面】土地利用     |  
| oData-land_series       | natural_line    | 【点】自然特征点   |  
| oData-land_series       | natural_point   | 【线】自然特征线   |  
| oData-land_series       | natural_polygon | 【面】自然覆盖    |  

### 3.1 landuse_polygon 土地利用-面

#### 3.1.1 LandClass 字段解析

用地以及分类分类数据：**开发用地** `developed_land（建设用地）, rural_and_agricultural_land（农林用地）, other_landuse（其他用地）`；**娱乐用地** `sustenance（生活服务）, education（教育）, transportation（交通）, financial（金融）, healthcare（医疗）, entertainment_arts_culture（文娱艺术）, public_service（公共服务）, facilities（设施）, waste_management（垃圾处理）, others_amenity（其他便利设施）` ; **休闲用地** `leisure（休闲）`；**旅游用地** `tourism（旅游）` 4大类
| LandClass                     | 用地一级分类             |  
|------------------------------|------------------|  
| Accommodation                | 住宅             |  
| Developed Land               | 建设用地         |  
| Rural and Agricultural Land  | 农林用地         |  
| Other Landuse                | 其他用地         |  
| Sustenance                   | 商业餐饮         |  
| Education                    | 教育             |  
| Transportation               | 交通设施         |  
| Financial                    | 金融             |  
| Healthcare                   | 康养用地         |  
| Entertainment, Arts & Culture| 文体娱乐         |  
| Public Service               | 公共服务         |  
| Facilities                   | 基础设施         |  
| Waste Management             | 环卫设施         |  
| Others Amenity               | 其他服务设施     |  
| Leisure                      | 休闲绿地         |  
| Tourism                      | 旅游用地         |  

#### 3.1.2 landuse 详细解读1-开发用地

> ##### developed land 建设用地
> 
> commercial（商业）, construction（建筑工地）, education（教育）, fairground（集市/展会场）, industrial（工业）, residential（住宅）, retail（零售）, institutional（机构）

> ##### rural and agricultural land 农用地
> 
> aquaculture（水产养殖）, allotments（分块菜地）, farmland（农田）, farmyard（农家场院）, paddy（稻田）, animal_keeping（牲畜饲养）, flowerbed（花坛）, forest（森林）, logging（伐木区）, greenhouse_horticulture（温室园艺）, meadow（草甸）, orchard（果园）, plant_nursery（苗圃）, vineyard（葡萄园）

> ##### Other landuse 其他土地利用
> 
> aquaculture（水产养殖）, allotments（分块菜地）, farmland（农田）, farmyard（农家场院）, paddy（稻田）, animal_keeping（牲畜饲养）, flowerbed（花坛）, forest（森林）, logging（伐木区）, greenhouse_horticulture（温室园艺）, meadow（草甸）, orchard（果园）, plant_nursery（苗圃）, vineyard（葡萄园）

####  3.1.3 landuse 详细解读2-娱乐用地

> ##### Sustenance 餐饮用地
> 
> bar（酒吧）, bbq（烧烤点）, biergarten（啤酒花园）, cafe（咖啡馆）, drinking_water（饮用水点）, fast_food（快餐店）, food_court（美食广场）, ice_cream（冰淇淋店）, pub（酒馆）, restaurant（餐厅）

> ##### Education 教育用地
> 
> commercial（商业）, construction（建筑工地）, education（教育）, fairground（集市/展会场）, industrial（工业）, residential（住宅）, retail（零售）, institutional（机构）

> ##### Transport 交通用地
> 
> bicycle_parking (自行车停放点), bicycle_rental (自行车租赁点), boat_rental (船只租赁点), bus_station (公交车站), car_rental (汽车租赁点), car_sharing (共享汽车点), car_wash (洗车点), charging_station (充电站), ferry_terminal (轮渡码头), fuel (加油站), gritting_station (撒砂站), motorcycle_parking (摩托车停放点), parking (停车场), parking_entrance (停车场入口), taxi (出租车), ticket_validator (票务验证机)

> ##### Financial 金融用地
> 
> atm (自动取款机), bank (银行), bureau_de_change (货币兑换点)

> ##### Healthcare 康养用地
> 
> baby_hatch (婴儿安全岛), clinic (诊所), dentist (牙科诊所), dialysis (透析中心), doctors (医生诊所), hospital (医院), nursing_home (养老院), pharmacy (药房), social_facility (社会福利机构), veterinary (兽医诊所)

> ##### Entertainment, Arts & Culture 文娱用地
> 
> arts_centre (艺术中心), cinema (电影院), community_centre (社区中心), conference_centre (会议中心), events_venue (活动场所), music_venue (音乐场馆), nightclub (夜总会), planetarium (天文馆), social_centre (社交中心), studio (工作室/演播室), theatre (剧院)

> ##### Public Service 公服用地
> 
> courthouse (法院), embassy (大使馆), fire_station (消防站), police (警察局), post_box (邮筒), post_depot (邮政仓库), post_office (邮局), prison (监狱), rangers_station (护林站), townhall (市政厅)

> ##### Facilities 设施用地
> 
> bench (长椅), clock (时钟), crematorium (火葬场), diving_platform (跳水台), drinking_water (饮用水点), fountain (喷泉), grave_yard (墓地), hunting_stand (狩猎台), marketplace (集市), phone (公共电话), place_of_worship (宗教场所), recycling (回收站), shelter (庇护所), shower (淋浴间), table (野餐桌), toilet (公共厕所), water_point (取水点), watering_place (牲畜饮水处)

> ##### Waste Management 废物管理用地
> 
> recycling (回收站), waste_basket (垃圾桶), waste_disposal (垃圾处理点), waste_transfer_station (垃圾转运站)

> ##### Others amenity 其他设施用地
> 
> animal_boarding (宠物寄养所), animal_shelter (动物收容所), boat_storage (船只存放处), dojo (道场), game_feeding (动物喂食点), give_box (爱心捐赠箱), internet_cafe (网吧), kitchen (公共厨房), loading_dock (装卸平台), public_bath (公共澡堂), self_storage (自助仓储), stripclub (脱衣舞俱乐部)

####  3.1.3 landuse 详细解读3-休闲用地

> ##### leisure 休闲用地
> 
> adult_gaming_centre（成人游戏中心），amusement_arcade（游乐场），bandstand（音乐台），beach_resort（海滩度假村），common（公共绿地），dance（舞蹈），dog_park（狗狗公园），escape_game（密室逃脱），fitness_centre（健身中心），fitness_station（健身站），garden（花园），golf_course（高尔夫球场），hacker_space（黑客空间），ice_rink（溜冰场），marina（码头），miniature_golf（迷你高尔夫），nature_reserve（自然保护区），park（公园），picnic_table（野餐桌），pitch（运动场），playground（游乐场），public_bath（公共浴室），sauna（桑拿房），slipway（滑道），sports_centre（体育中心），stadium（体育场），summer_camp（夏令营），swimming_area（游泳区），swimming_pool（游泳池），track（跑道），water_park（水上乐园），wildlife_hide（野生动物观察点）

####  3.1.3 landuse 详细解读4-旅游用地

> ##### tourism 旅游用地
> 
> alpine_hut（高山小屋），apartment（公寓），artwork（艺术品），attraction（景点），bed_and_breakfast（民宿），camp_site（露营地），caravan_site（房车营地），chalet（木屋别墅），gallery（画廊），guest_house（宾馆），hostel（青年旅舍），hotel（酒店），information（信息中心），motel（汽车旅馆），museum（博物馆），picnic_site（野餐区），theme_park（主题公园），view_point（观景点），wilderness_hut（荒野小屋），zoo（动物园）

### 3.2 natural_polygon 自然地块-面

#### 3.2.1 NatureClass 字段解析

| NatureClass                  | 自然用地一级分类     |  
|------------------------------|------------------   |  
| Vegetation                   | 天然植被            |  
| Water related                | 水相关              |
| Geology related              | 地理相关            |

#### 3.2.2 Nature 字段解析

> ##### Vegetation 天然植被
> 
> grass（草地），grassland（草原），heath（荒野），scrub（灌木丛），tree（树木），tree_row（树列），wood（树林），shrubbery（灌木丛）

> ##### Water related 水相关
> 
> atoll（环礁），bay（海湾），beach（海滩），blowhole（喷水洞），coastline（海岸线），fjord（峡湾），geyser（间歇泉），glacier（冰川），hot_spring（温泉），island（岛屿），marsh（沼泽），mud（泥滩），reef（礁石），shoal（浅滩），spring（泉），strait（海峡），water（水域），wetland（湿地），riverbed（河床）

> ##### Geology related 地理相关
> 
> bare_rock（裸岩），cape（海角），cave_entrance（洞穴入口），cliff（悬崖），crater（火山口），dune（沙丘），earth_bank（土坡），fell（荒山），hill（丘陵），isthmus（地峡），landform（地貌），moraine（冰碛），peak（山峰），peninsula（半岛），ridge（山脊），rock（岩石），saddle（鞍部），sand（沙地），scree（碎石坡），sinkhole（天坑），stone（巨石），valley（山谷），volcano（火山），wilderness（荒野），mountain_range（山脉），mesa（台地），desert（沙漠），caldera（破火山口），dunes（沙丘群），gorge（峡谷），landslide（滑坡），shingle（砾石滩）

</br>

## 4.🚉 铁路数据<a id="section4"></a>
| 数据标准名               | 数据类别 | 数据结构       |  
| ------------------------ | ---------- | ----------------    |  
| oData-railway_series    | railway_line    | 【线】铁路线     |  
| oData-railway_series    |  railway_point  | 【点】铁路站点   |  

涵盖各项完整的高速铁路、普速铁路、废弃铁路、地铁、轻轨、观光轨道数据。

### 4.1 railway_line 铁路线

#### 4.1.1 railway_line 数据示例
| 序号 | 字段名     | 属性值     | 解释             |
| :--: | :--------: | :--------------: | :--------------- |
| 1    | name       | 西成高铁    | 名称             |
| 2    | railway    | rail        | 铁路类型         |
| 3    | layer      | -1          | 数据所在符号层图层 |
| 4    | construct  | NULL        | 建设状态         |
| 5    | service    | F           | 是否为服务线路（F为否） |
| 6    | highspeed  | T           | 是否为高速铁路（T为是）  |
| 7    | maxspeed   | 250         | 最大速度250km/h   |
| 8    | usage      | main        | 使用类型（主线、侧线…）  |
| 9    | bridge     | F           | 是否为桥梁结构（T为是） |
| 10   | tunnel     | T           | 是否为隧道结构（T为是） |
| 11   | altName    | 房家湾隧道   | 桥隧名         |

> ##### railway 标签解析
> 
> rail（普通铁路）, construction（建设中）, disused（废弃）, abandoned（被遗弃）, traverser（横移台）, engine_shed（机车库）, subway（地铁）, proposed（提议中的）, tram（有轨电车）, planned（规划中）, razed（已拆除）, light_rail（轻轨）, monorail（单轨铁路）, narrow_gauge（窄轨）, yes（存在铁路）, turntable（转车台）, funicular（缆索铁路）, platform_edge（站台边缘）, halt（小站）, miniature（微缩铁路）, crane（起重机）, preserved（保存良好的/博物馆线路）, tram_stop（有轨电车站）, dismantled（已拆解）, wash（洗车设施）, container_terminal（集装箱码头）, ventilation_shaft（通风井）, historic（历史遗迹）,  stop（停车点）, yard（编组场）, buffer_stop（缓冲挡）, ferry（轮渡）

### 4.2 railway_point 铁路站点

#### 4.2.1 railway_point 数据示例
| 序号 | 字段名     | 属性值     | 解释             |
| :--: | :--------: | :--------------: | :--------------- |
| 1    | name       | 成都东     | 站点名            |
| 2    | station    | rail        | 普通铁路站点      |

> ##### station 标签解析
> 
> station（车站）, subway（地铁）, train（列车）, monorail（单轨铁路）, tram（有轨电车）, tram_stop（有轨电车站）

</br>

## 7.🌊 水系大坝<a id="section7"></a>

| 数据标准名               | 数据类别 | 数据结构       |  
| ------------------------ | ---------- | ----------------    |  
| oData-water&dam_series | waterway           | 【面】水系线     |  
| oData-water&dam_series | waterway_polygon   | 【点】水域面   |  
| oData-water&dam_series | dam_line           | 【线】大坝   |  
| oData-water&dam_series | dam_polygon        | 【面】大坝   |

### 7.1 waterway 水系线

#### 7.1.1 waterway 数据示例

|序号| 字段名    | 属性值         | 解释                 |
| :------: | :-----------: | :----------------: | :----------------- |
|1| name          | 锦江     | 水系名     |
|2| waterway      | river    | 水系分类    |
|3| tunnel        | T/F      | T为隧道结构 |
|4| bridge        | T/F      | T为桥梁结构 |
|5| layer         | 0        | 数据所在符号层图层|
|6| intermittent  | T/null   | T为间歇性水流 |
|7| salt          | T/null   | T为咸水       |

> ##### waterway 属性详解
> 
> waterway（水道），canal（运河），ditch（沟渠），river（河流），drain（排水渠），stream（溪流），pressurised（压力管道），fish_pass（鱼道），tidal_channel（潮汐通道），fairway（航道）

### 7.2 water_polygon 水域面

| WaterClass       | 水域一级分类 | 水域二级分类       |  
| ---------------- | ---------- | ----------------    |  
| Water       | 水域相关           | 除冰川、湿地外其他所有水域数据    |  
| Glacier     | 冰川               | 只包含冰川数据  |  
| Wetland     | 湿地               | 只涵盖湿地数据   |  

#### 7.2.1 water_polygon 数据示例

|序号| 字段名    | 属性值         | 解释                 |
| :------: | :-----------: | :----------------: | :----------------- |
|1| name          | 丹江口水库    | 水系名     |
|2| WaterClass    | water        | 水域以及类型    |
|3| water         | reservoir    | 水库 |
|4| intermittent  | T/null      | T为间歇性水流 |
|5| salt          | T/null      | T为咸水       |

> ##### water 属性详解
> 
> basin（蓄水池），canal（运河），cenote（天然井），ditch（沟渠），drain（排水沟），fairway（航道），fish_pass（鱼道），harbour（港口），lagoon（潟湖），lake（湖泊），lock（船闸），moat（护城河），oxbow（牛轭湖），pond（池塘），rapids（急流），reflecting_pool（倒影池），reservoir（水库），river（河流），stream（溪流），stream_pool（溪潭），wastewater（废水池），water（水域）

### 7.3 dam_line 大坝（线）

#### 7.1.1 dam_line 数据示例

|序号| 字段名    | 属性值         | 解释                 |
| :------: | :-----------: | :----------------: | :----------------- |
|1| name          | XX大坝     | 大坝名    |
|2| dam      | dam    | 种类    |

> ##### dam(dam_line) 属性详解
> 
> dam（水坝），weir（堰），waterfall（瀑布），lock_gate（闸门），sluice_gate（泄水闸），floodgate（防洪闸），debris_screen（拦污栅）

### 7.2 dam_polygon 大坝（面）

#### 7.2.1 water_polygon 数据示例

|序号| 字段名    | 属性值         | 解释                 |
| :------: | :-----------: | :----------------: | :----------------- |
|1| name          | XX大坝     | 大坝名    |
|2| dam      | dam    | 种类    |

> ##### dam(dam_polygon) 属性详解
> 
> bdam（水坝），weir（堰），sluice_gate（泄水闸），waterfall（瀑布），lock_gate（闸门）
