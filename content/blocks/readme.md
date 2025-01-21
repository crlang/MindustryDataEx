解释来源

> https://www.bilibili.com/read/readlist/rl451504
> https://mindustrygame.github.io/wiki/

数据来源

> https://github.com/Anuken/Mindustry/tree/master/core/src/mindustry/content/Blocks.java
> https://github.com/Anuken/Mindustry/tree/master/core/assets/bundles/bundle_zh_CN.properties

# 物品

> color: 物品在分类器、反向分类器、物品源上的着色

> explosiveness: 爆炸性，和屏幕抖动幅度、受到的伤害有关

> hardness: 作为矿物时的钻探难度，钻头 tier 大于 hardness 均可钻探

> radioactivity: 只和裂变发电机(RTG)发电量有关，不和核反应堆的发电量和爆炸威力有关

> cost: 建造耗时，具体公式见下：

```
全部物品cost总和 * 方块buildCostMultiplier
```

> healthScaling: 影响方块默认生命值见下：

```
全部物品本值总和 * 40 = 方块默认血量
```

> lowPriority: 钻头钻探优先级(如沙子为 false，若铅和沙在同一地板，优选钻取铅)

> buildable: 若为 false，在 incinerateNonBuildable 为 false 的核心方块会被直接销毁（如 Erekir 的全部核心方块）

> hidden: 是否隐藏

# 钻头

## blastDrill/爆破钻头 -> Drill

> drillTime: 钻头速率，计算整体挖掘效率用如下公式并取两位小数，hardnessDrillMultiplier 一般取 50

```
60/(钻头drillTime + 钻头hardnessMultiplier * 物品hardness) * 格子总数
```

> tier: 钻头等级，大于物品 hardness 即可钻探

> warmupSpeed: 钻头满效率预热(效率从 0 线性增加到上限)

> liquidBoostIntensity: 液体加速效果，也和上方上限有关

## impactDrill/冲击钻头 -> BurstDrill

> drillTime: 每次出货时间

> shake: 出货时摇晃力度

> blockedItem: 不可挖掘的物品

> researchCostMultiplier: 研究消耗倍率

> fogRadius: 探雾范围

## plasmaBore/光束钻头 -> BeamDrill

> range: 光束长度(包含矿物一格)

> research: 科技树相关，见后

# 运输

## conveyor/传送带 -> Conveyor

> speed: 运送速度，越大越快

> displayedSpeed: 详情页显示运输速度

> buildCostMultiplier: 建造时间倍率，公式见上文 item

## plastaniumConveyor/塑钢传送带 -> StackConveyor

> outputRouter : 传送带末尾是否像路由器一样

传输速率公式

```
保留小数(itemCapacity * speed * 60,2)
```

## armoredConveyor/装甲传送带 -> ArmoredConveyor

## junction/交叉器 -> Junction

> capacity: 物品容量

> speed: 物品穿过所需时间

## itemBridge/传送带桥 -> BufferedItemBridge

> range: 延展范围

> arrowSpacing: 箭头间距

> bufferCapacity: 一次性输出物品个数(?

## phaseConveyor/相织布传送带桥 -> ItemBridge

## massDriver/质量驱动器 -> MassDriver

> reload: 重载时间

> range: 传输范围

# 传输

## 能量节点/PowerNode

> maxNodes: 最大连接数

> laserRange: 连接范围/格

# 存储

## 电池/Battery

> consumes.powerBuffered: 电池容量(不用 \* 60)

# 发电

## 火力发电机 -> 燃烧发电机/BurnerGenerator

> powerProduction: 1.00(这里和 consumes.powerBuffered 不一样，需 \* 60)

> itemDuration: 持续产能时间/帧

## 地热发电机 -> 地热发电机/ThermalGenerator

> attribute: 方块所占底部格子给予的属性(见后)

## 温差发电机 -> 单类发电机(?)/SingleTypeGenerator

> hasLiquids: 拥有液体(一般为初始化，不用填写)

> hasItems: 拥有物品(同上)

> consumes.items: 物品消耗器

> consumes.items.items: 消耗的物品

> consumes.liquid: 液体消耗器

> consumes.\*.optional: 作为可选输入(这里不解，将原定义&注释贴在上)

> consumes.\*.boost: 作为增益输入

## RTG 发电机 -> 衰变发电机/DecayGenerator

## 太阳能板 -> 太阳能发电/SolarGenerator

## 钍反应堆 -> 核能发电机/NuclearReactor

> heating: 每帧加热(heating \* 物品数量(fullness??))

> consumes.liquid.liquid: 消耗的液体

> consumes.liquid.amount: 使用液体容量(\* 60)

> consumes.\*.update: ?

## 冲击反应堆 -> 冲击发电机/ImpactReactor

> consumes.power: 消耗能量(\* 60)

# 工厂

## 小硅 -> 普通工厂/GenericCrafter

> outputItem: 输出单种类物品

> craftTime: 制作时间

> hasPower: 能否拥有能量(游戏自带初始化，一般不填，但是在工厂里几乎全要填)

> hasLiquid: 能否拥有液体(同上)

> drawer: 添加贴图(?)

## 大硅 -> 属性工厂/AttributeCrafter

> itemCapacity: 物品容量

> boostScale: 增益倍率(?)

## 冷冻液混合器 -> 液体转换器/LiquidConverter

> outputLiquid: 输出液体

> hasItems: 能否拥有物品(同 hasPower)

> rotate: 是否可旋转(同上)

> solid: 是否为固体(同上)

## 分离机 -> 分离机/Separator

> results: 每个产出物品概率(而非数量)

## 焚烧炉 -> 焚烧炉/Incinerator

## 液体

> pumpAmount: 每个泵的泵量

> consumeTime: 项目消耗之间的间隔（如果适用）。

> liquidCapacity: 如果 hasLiquids = true，这个方块可以携带的最大液体总量

> liquidPressure: 更高的数字增加液体输出速度； TODO 移除并更换更好的液体系统

# 单位工厂

## 地面单位工厂 -> UnitFactory/单位工厂

> plans.unit: 生产的单位

> plans.time: 生产时间

> plans.requirements: 生产所消耗的物资

# 重构工厂

## tankAssembler/坦克装配厂 -> UnitAssembler/装配工厂

> droneType: 用来装载的单位

> dronesCreated: 装载单位数量

> droneConstructTime: 装载单位被制造耗时

> areaSize: 建造区域边长

## 倍乘级单位重构工厂 -> Reconstructor/重构工厂

> constructTime: 升级时间

> upgrades.\*.0: 升级前机甲

> upgrades.\*.1: 升级后机甲

### 物品对照

item.copper.name = 铜
item.lead.name = 铅
item.coal.name = 煤炭
item.graphite.name = 石墨
item.titanium.name = 钛
item.thorium.name = 钍
item.silicon.name = 硅
item.plastanium.name = 塑钢
item.phase-fabric.name = 相织布
item.surge-alloy.name = 巨浪合金
item.spore-pod.name = 孢子荚
item.sand.name = 沙
item.blast-compound.name = 爆炸混合物
item.pyratite.name = 硫化物
item.metaglass.name = 钢化玻璃
item.scrap.name = 废料
item.fissile-matter.name = 裂变产物
item.beryllium.name = 铍
item.tungsten.name = 钨
item.oxide.name = 氧化物
item.carbide.name = 碳化物
item.dormant-cyst.name = 休眠囊肿

liquid.water.name = 水
liquid.slag.name = 矿渣
liquid.oil.name = 石油
liquid.cryofluid.name = 冷冻液
liquid.neoplasm.name = 瘤液
liquid.arkycite.name = 芳油
liquid.gallium.name = 镓
liquid.ozone.name = 臭氧
liquid.hydrogen.name = 氢气
liquid.nitrogen.name = 氮气
liquid.cyanogen.name = 氰气

unit.dagger.name = 尖刀
unit.mace.name = 战锤
unit.fortress.name = 堡垒
unit.nova.name = 新星
unit.pulsar.name = 恒星
unit.quasar.name = 耀星
unit.crawler.name = 爬虫
unit.atrax.name = 毒蛛
unit.spiroct.name = 血蛭
unit.arkyid.name = 毒蛊
unit.toxopid.name = 天蝎
unit.flare.name = 星辉
unit.horizon.name = 天垠
unit.zenith.name = 苍穹
unit.antumbra.name = 月影
unit.eclipse.name = 日蚀
unit.mono.name = 独影
unit.poly.name = 幻型
unit.mega.name = 巨像
unit.quad.name = 雷霆
unit.oct.name = 要塞
unit.risso.name = 梭鱼
unit.minke.name = 飞鲨
unit.bryde.name = 戟鲸
unit.sei.name = 蛟龙
unit.omura.name = 海神
unit.retusa.name = 潜螺
unit.oxynoe.name = 电鳗
unit.cyerce.name = 江豚
unit.aegires.name = 玄武
unit.navanax.name = 龙王
unit.alpha.name = 阿尔法
unit.beta.name = 贝塔
unit.gamma.name = 伽马
unit.scepter.name = 权杖
unit.reign.name = 王座
unit.vela.name = 灾星
unit.corvus.name = 死星

unit.stell.name = 围护
unit.locus.name = 循迹
unit.precept.name = 准绳
unit.vanquish.name = 征服
unit.conquer.name = 领主
unit.merui.name = 天守
unit.cleroi.name = 天赐
unit.anthicus.name = 天灾
unit.tecta.name = 天理
unit.collaris.name = 天帝
unit.elude.name = 挣脱
unit.avert.name = 遮蔽
unit.obviate.name = 消散
unit.quell.name = 遏止
unit.disrupt.name = 悲怆
unit.evoke.name = 苏醒
unit.incite.name = 策动
unit.emanate.name = 发散
unit.manifold.name = 货运无人机
unit.assembly-drone.name = 装配无人机
unit.latum.name = Latum
unit.renale.name = Renale
