# 废稿

这里收录了一些 [2.2 节](../2-the-overworld/2.2-main-layer.md) 舍不得删掉的废稿，是本文在 1.15 -> 1.16 更新之后中失效的内容。

### 相似生物群系

这里我们引入相似生物群系的概念。

出于易于理解的目的，相似可以近似解释为：

- 相同的生物群系相似

- 类别相同且均不为 none 的生物群系相似

但是 Mojang 为平顶山生物群系做了特化，导致判断相似的方法是一个不对称的方法（即存在 `a` 和 `b` 两个生物群系使得，`areSimilar(a, b) != areSimilar(b, a)`），因此下面给出我整理后的等效方法：

```Java
boolean areSimilar(Biome biome1, Biome biome2) {
   if (biome1 == biome2) return true;
   return biome1 == WOODED_BADLANDS_PLATEAU || biome1 == BADLANDS_PLATEAU
         ? biome2 == WOODED_BADLANDS_PLATEAU || biome2 == BADLANDS_PLATEAU
         : biome1.getCategory() != Category.NONE 
         && biome2.getCategory() != Category.NONE
         && biome1.getCategory() == biome2.getCategory();
}
```

可以看出，当 `biome1` 为恶地高原或者繁茂恶地高原时，`biome2` 也必须是恶地高原或者繁茂恶地高原才能相似。但是 `biome2` 为恶地高原或者繁茂恶地高原却不需要 `biome1` 是恶地高原或者繁茂恶地高原，（根据后面的分支）只需要类别是恶地即可相似。

我不想用左相似、右相似这样奇怪的说法来区分这两种情况，下文所述的

> a 相似于 b

指的就是 `areSimilar(a, b)`。

> 相似于 b 的生物群系

指的是 `areSimilar(/*这些生物群系*/, b) == true`

### 边缘

#### 失落的属性：温度类别

**温度类别**也是世界生成时用到的属性之一，而且仅在世界生成中使用。它不是_指定_的，而是根据类别、温度这两个属性_计算_出来的。分为海洋、冷、中和暖。

然而不幸的是，唯一使用它的地方不是别处，正是决定是否生成山地边缘的代码。结果你也知道了，经过化简得出：山地边缘一定不会生成。是具体是什么原因导致了山地边缘的消失呢？

山地边缘作为一个 1.7.2 开始就不再生成的边缘生物群系，在世界生成的代码里，并非真的消失——实际上 MC 第一个试图生成的边缘生物群系就是它！但结果总是失败，为什么呢？

这里直接上代码可能会好理解一些，但是不借助代码也可以讲清楚。对 _山地生物群系_（常量）和四周（車）每一个区域的生物群系调用下面的函数，如果**全部**为 true，说明自己不能变成山地边缘。

```Java
boolean cannotBecomeMtEdge(Biome biome1, Biome biome2) {
   if (areSimilar(biome1, biome2)) return true;
   TemperatureCategory type1 = biome1.getTemperatureCategory();
   TemperatureCategory type2 = biome2.getTemperatureCategory();
   return type1 == type2 
       || type1 == TemperatureCategory.MEDIUM 
       || type2 == TemperatureCategory.MEDIUM;
}
```

这个函数会在这些情况下为 true：

- 两个生物群系相似，即相似于 _山地生物群系_
- 温度类别相同，或其中一个是中

如果表面上观察，一切似乎很合理。不过，山地生物群系的温度类别是什么？相信读者读到这里，答案呼之欲出了：中。没错，无论另一个生物群系的温度类别是什么，最后一个语句都相当于一个`return true`。进而得到这个函数相当于`areSimilar(biome1, biome2) ? true : true`：这两个生物群系相似也是 true，不相似也是 true，说白了永远是 true——因此直接排除了所有的区域！山地边缘自此成了笑话：后文其实仍有关于山地边缘的判断、尝试，我于是一并忽略、删去。