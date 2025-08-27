---
title: 「翻译」Waterfowl and ABCs
published: 2025-03-23
description: 'Alex  Martelli 对 `goose typing` 的解释。'
image: ''
tags: [翻译, 书摘, Python]
category: '翻译'
draft: false 
lang: ''
---

> I’ve been credited on Wikipedia for helping spread the helpful meme and sound-bite “duck typing” (i.e, ignoring an object’s actual type, focusing instead on ensuring that the object implements the method names, signatures, and semantics required for its intended use).
> In Python, this mostly boils down to avoiding the use of isinstance to check the object’s type (not to mention the even worse approach of checking, for example, whether type(foo) is bar—which is rightly anathema as it inhibits even the simplest forms of inheritance!).
> The overall duck typing approach remains quite useful in many contexts—and yet, in many others, an often preferable one has evolved over time. And herein lies a tale...

我在Wikipedia上被认可，因为帮助传播了有用的梗和口号“鸭子类型”（即忽略对象的实际类型，而是专注于确保该对象实现了其预期使用所需的方法名称、签名和语义）。

在Python中，这主要涉及避免使用isinstance来检查对象的类型（更不用说甚至更邪恶的做法是检查例如type(foo)是否为bar——这被正确地视为可耻的，因为它阻止了最简单形式的继承！）。

整体上，鸭子类型方法在许多环境中仍然非常有用，而且随着时间的推移，在许多其他情况下已经出现了一个通常更可取的方法。这里就涉及到一个故事...

> In recent generations, the taxonomy of genus and species (including, but not limited to, the family of waterfowl known as Anatidae) has mostly been driven by pheneticsan approach focused on similarities of morphology and behavior...chiefly, observable traits. The analogy to “duck typing” was strong.
> However, parallel evolution can often produce similar traits, both morphological and behavioral ones, among species that are actually unrelated, but just happened to evolve in similar, though separate, ecological niches. Similar “accidental similarities” happen in programming, too—for example, consider the classic object-oriented programming example:

在近代史上，种属和物种的分类（包括但不限于以鸭形目Waterfowl的家族Anatidae）主要是由形态学和行为相似性导向的表观方法驱动...而这些主要关注可观察到的特征。与“鸭子类型”有很强的类比。

然而，并行演化经常会在实际上没有关系的物种之间产生相似的形态学和行为特征，尽管它们发生在相似但独立的生态尼切中。编程中也会发生类似的“偶然相似”——例如，考虑经典的面向对象编程示例：

```python
class Artist:
    def draw(self): ...

class Gunslinger:
    def draw(self): ...

class Lottery:
    def draw(self): ...
```

> Clearly, the mere existence of a method named draw, callable without arguments, is far from sufficient to assure us that two objects x and y, such that x.draw() and y.draw() can be called, are in any way exchangeable or abstractly equivalent -- nothing about the similarity of the semantics resulting from such calls can be inferred. Rather, we need a knowledgeable programmer to somehow positively assert that such an equivalence holds at some level!

显然，仅存在一个名为draw的没有参数的方法调用是远远不够保证我们两个对象x和y，使得可以调用x.draw()和y.draw()，它们在任何方式上都是可以交换或抽象等效--关于从这些调用产生的语义相似性不能推断出任何东西。我们需要一个有知识的程序员来以某种积极肯定的方式声明此类等价关系在某个层面上是成立的！

> In biology (and other disciplines), this issue has led to the emergence (and, on many facets, the dominance) of an approach that’s an alternative to phenetics, known as cladistics—focusing taxonomical choices on characteristics that are inherited from common ancestors, rather than ones that are independently evolved. (Cheap and rapid DNA sequencing can make cladistics highly practical in many more cases in recent years.)

在生物学（和其他学科）中，这一问题引发了一个与表观法相悖但却占据主导地位的方法的出现，这种方法称为系统发育学或谱系发育学——它将分类选择集中在从共同祖先继承的特征上，而不是独立演化的特征。（低廉快速的DNA测序可以使得近年来在更多情况下让系统发育学变得非常实用。）

> For example, sheldgeese (once classified as being closer to other geese) and shelducks (once classified as being closer to other ducks) are now grouped together within the subfamily Tadornidae (implying they’re closer to each other than to any other Anatidae, as they share a closer common ancestor). Furthermore, DNA analysis has shown, in particular, that the white-winged wood duck is not as close to the Muscovy duck (the latter being a shelduck) as similarity in looks and behavior had long suggested—so the wood duck was reclassified into its own genus, and entirely out of the subfamily!

例如，雁鸭属的水鸭蹼鸭（以前被归类为更接近其他雁）和豚鸭蹼鸭（以前被归类为更接近其他鸭子）现在都被归入同一个亚科Tadornidae之中（这意味着它们彼此相似超过任何其他的Anatidae，因为它们有共同的靠近的祖先）。进一步地，DNA分析显示，特别是白翅鸭和木鸭（后者是蹼鸭中的种类之一）并不像外观和行为长期暗示那样接近肯苏维鸭，因此木鸭被重新分类到了自己的属中，完全离开了亚科！

> Does this matter? It depends on the context! For such purposes as deciding how best to cook a waterfowl once you’ve bagged it, for example, specific observable traits (not all of them—plumage, for example, is de minimis in such a context), mostly texture and flavor (old-fashioned phenetics!), may be far more relevant than cladistics. But for other issues, such as susceptibility to different pathogens (whether you’re trying to raise waterfowl in captivity, or preserve them in the wild), DNA closeness can matter much more.

这有影响吗？这取决于上下文！例如，对于已经射杀的水鸭来说，为了决定如何最好地烹饪它，特定可观察到的特征（不是全部，比如羽毛在这种情况下就无关紧要），主要是质地和味道（老式的表现法！），可能比系统发育学更相关。但对于其他问题，例如对不同病原体的抗性（无论你是想在野外保护还是在人工养殖下饲养水鸭），DNA接近程度可能就更重要了。

> So, by very loose analogy with these taxonomic revolutions in the world of waterfowls, I’m recommending supplementing (not entirely replacing—in certain contexts it shall still serve) good old duck typing with...goose typing!

综上所述，根据水鸭类别的这些革命性变化，我建议在不完全替代（在某些情况下它仍会发挥作用）情况下，使用旧式鸭子类型结合...鹅子类型进行补充！

> What goose typing means is: isinstance(obj, cls) is now just fine...as long as cls is an abstract base class—in other words, cls’s metaclass is abc.ABCMeta.

所谓的鹅子类型，指的是：只要cls是一个抽象基类——换句话说，cls的元类是abc.ABCMeta，即isinstance(obj, cl)就可以正常运行。

> You can find many useful existing abstract classes in collections.abc (and additional ones in the numbers module of The Python Standard Library).

你可以在collections.abc模块中找到许多有用的现成抽象类（Python标准库的numbers模块中也有其他一些）。

> Among the many conceptual advantages of ABCs over concrete classes (e.g., Scott Meyer’s “all non-leaf classes should be abstract”; see Item 33 in his book, More Effective C++, Addison-Wesley), Python’s ABCs add one major practical advantage: the register class method, which lets end-user code “declare” that a certain class becomes a “virtual” subclass of an ABC (for this purpose, the registered class must meet the ABC’s method name and signature requirements, and more importantly, the underlying semantic contract—but it need not have been developed with any awareness of the ABC, and in particular need not inherit from it!). This goes a long way toward breaking the rigidity and strong coupling that make inheritance something to use with much more caution than typically practiced by most object-oriented programmers.

在抽象类相比具体类方面，概念上有许多优势（例如Scott Meyer的“所有非叶子类都应该是抽象的”；请参见其书《More Effective C++》中的第33条）。Python的ABC提供了一个重要的实用优势：register方法，它让最终用户代码可以“声明”某个类成为ABC的“虚拟”子类（为此，注册的类必须满足ABC的方法名称和签名的要求，更重要的是底层的语义契约——但它不需要任何对ABC的意识或特别从中继承！）。这在很大程度上打破了继承带来的严格性和强耦合，使得继承成为一种必须谨慎使用而不是常规实践的面向对象编程者通常会使用的工具。

> Sometimes you don’t even need to register a class for an ABC to recognize it as a subclass!
> That’s the case for the ABCs whose essence boils down to a few special methods. For example:

```python
>>> class Struggle:

... def __len__(self): return 23
...
>>> from collections import abc
>>> isinstance(Struggle(), abc.Sized)
True
```

> As you see, abc.Sized recognizes Struggle as “a subclass,” with no need for registration, as implementing the special method named __len__ is all it takes (it’s supposed to be implemented with the proper syntax—callable without arguments—and semantics—returning a nonnegative integer denoting an object’s “length”; any code that implements a specially named method, such as __len__, with arbitrary, noncompliant syntax and semantics has much worse problems anyway).

显然，abc.Sized将Struggle识别为“子类”，而无需注册，只要实现名为__len__的特殊方法就足够了（应该按照正确的语法实现——不带参数可调用，按照正确的含义——返回一个非负整数表示对象的“长度”；任何使用伪造的、不符合规范的语法和含义实现特殊方法名称，比如__len__，都会有更大的问题）。

> So, here’s my valediction: whenever you’re implementing a class embodying any of the concepts represented in the ABCs in numbers, collections.abc, or other framework you may be using, be sure (if needed) to subclass it from, or register it into, the corresponding ABC. At the start of your programs using some library or framework defining classes which have omitted to do that, perform the registrations yourself; then, when you must check for (most typically) an argument being, e.g, “a sequence,” check whether:

所以，这是我的告别词：当你在任何实现数字、collections.abc或其他框架中表示概念的类中加入代码时，确保（如果需要）从相应的ABC继承它，或将它注册进去。在使用一些未能这样做的库或框架定义类的程序开始时，自行执行注册；然后，当你必须检查（通常是）一个参数是否是，例如“一种序列”时，检查以下情况：

```python
isinstance(the_arg, collections.abc.Sequence)
```

> 不要在生产代码中定义自定义的 ABC（或元类）。如果你觉得有这样的冲动，我敢打赌可能是因为某人刚买了一把新锤子，他开始看待所有问题都像是钉子的症状——你（以及未来的代码维护者）会更快乐地坚持使用简单直接的代码，避免陷入这种深度迷茫。再见！

不要在生产代码中定义自定义的 ABC（或元类）。如果你觉得有这样的冲动，我敢打赌可能是因为某人刚买了一把新锤子，他开始看待所有问题都像是钉子的症状——你（以及未来的代码维护者）会更快乐地坚持使用简单直接的代码，避免陷入这种深度迷茫。再见！
