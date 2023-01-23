# 数据表

版本：1.16.5，命名：offical

## 通用数据表

下表中整理汇总了原版 79 个生物群系的 23 个属性。（不包含对于所有生物群系都相同的属性和部分特有属性，参见后文）

<iframe src="../resources/data.htm" width=800 height=640></iframe>

-----

接下来的表格中 SE 代表 specialEffects

## 相同的属性

下面这些属性对于所有原版生物群系都有相同的值。

| 属性                                       | 值   |
| ------------------------------------------ | ---- |
| SE.ambientMoodSettings.blockSearchExtent   | 8    |
| SE.ambientMoodSettings.soundPositionOffset | 2    |
| SE.ambientMoodSettings.tickDelay           | 6000 |

## 下界特有属性

下面这些属性为下界生物群系特有。

 - nether_wastes 
 - soul_sand_valley
 - crimson_forest
 - warped_forest 
 - basalt_deltas 

### 相同的属性

下面这些属性对于所有下界生物群系都有相同的值。

| 属性                                   | 值     |
| -------------------------------------- | ------ |
| SE.ambientAdditionsSettings.tickChance | 0.0111 |
| SE.backgroundMusic.minDelay            | 12000  |
| SE.backgroundMusic.maxDelay            | 24000  |
| SE.backgroundMusic.replaceCurrentMusic | false  |

### 相似的属性

下面这些属性对于所有下界生物群系都有相似的值。

将表中 \[biome] 替换成下界生物群系的名字即为该下界生物群系该属性的值。

| 属性                                   | 值                         |
| -------------------------------------- | -------------------------- |
| SE.ambientAdditionsSettings.soundEvent | ambient.\[biome].additions |
| SE.ambientLoopSoundEvent               | ambient.\[biome].loop      |
| SE.backgroundMusic.event               | music.nether.\[biome]      |

### 其他属性

这些属性为部分下界生物群系特有。

| 生物群系         | SE.ambientParticleSettings.probability | SE.ambientParticleSettings.options |
| ---------------- | -------------------------------------- | ---------------------------------- |
| soul_sand_valley | 0.00625                                | minecraft:ash                      |
| crimson_forest   | 0.025                                  | minecraft:crimson_spore            |
| warped_forest    | 0.01428                                | minecraft:warped_spore             |
| basalt_deltas    | 0.118093334                            | minecraft:white_ash                |


| 生物群系         | mobSettings.mobSpawnCosts                                    |
| ---------------- | ------------------------------------------------------------ |
| soul_sand_valley | skeleton:{energyBudget=0.15,charge=0.7},  <br/>ghast:{energyBudget=0.15,charge=0.7},  <br/>enderman:{energyBudget=0.15,charge=0.7},  <br/>strider:{energyBudget=0.15,charge=0.7} |
| warped_forest    | enderman:{energyBudget=0.12,charge=1.0}                      |
