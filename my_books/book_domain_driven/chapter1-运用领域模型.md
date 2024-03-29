```
运用领域模型：提出领域驱动开发的基本目标，这些目标是后面几部分所讨论的实践的驱动因素。
```

```
地图就是模型，模型被用来描绘人们所关注的现实或想法的某个方面。
模型是一种简化，是对现实的解释-把与解决问题密切相关的方面抽象出来，而忽略无关的细节。

每个软件程序是为了执行用户的某项活动，或者是满足用户的某种需求。
这些用户应用软件的问题区域就是软件的  领域。

领域模型并非某种特殊的图，而是这种图所要传达的思想。绝不单单是领域专家头脑中的知识，而是对这类知识严格的组织切有选择的抽象。
```

#### 序

模型在领域驱动设计中的作用：

       	1. 模型和设计的核心互相影响。
        	2. 模型是土堆所有成员使用的通用语言的中枢。
       3. 模型是浓缩的知识。



#### 1. 消化知识

有效建模的要素
1. 模型和实现的绑定
2. 建立了一种基于模型的语言
3. 开发一个蕴含丰富知识的模型
4. 提炼模型
5. 头脑风暴和实验

#### 2. 交流与语言的使用

​	运用通用语言，能够减少开发人员与领域专家之间的翻译成本。都使用通用语言来描述问题，能够在运用的过程中相互理解促进，完善领域模型。

#### 3. 绑定模型和实现

1. 领域驱动设计  要求模型补进能够指导早期的分析工作，还应该成为设计的基础。这种设计方法对于代码的编写有这重要的意义。
2. 如果模型对于程序的实现来说闲的不太实用时，我们必须重新设计它。而如果模型无法忠实的描述领域的关键概念，也必须重新设计它。
3. 软件系统哥哥部分的设计应该忠实的反应领域模型，以便体现出着二者之间的明确对应关系。
