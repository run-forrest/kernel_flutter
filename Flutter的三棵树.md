### 1. 三棵树
分别为 Widget tree ， element tree， render tree
#### 1. Widget Tree
开发者最能感知的widget
#### 2. Element Tree
每个Wiget都会有对应的Element，并存在一颗对应的element tree，实际上，element tree才是内存中真实存在的数据，
widget tree和render tree 都是由element tree 驱动生成的。正是这样，element tree 扮演了flutter中virtual dom的管理者角色。
element tree中，renderObjectElemnt类型的节点会产生RenderObject，并构成最终的render tree。对开发者来说，render tree是最底层的UI描述。
但是对Engine来说，Render tree 是FrameWork对UI层最上层，最抽象的描述。
#### 简单总结：
Widget Tree:存放渲染内容、它只是一个配置数据结构，创建是非常轻量的，在页面刷新的过程中随时会重建
Element 是分离 Widget Tree 和真正的渲染对象的中间层， Widget Tree 用来描述对应的Element 属性,同时持有Widget和RenderObject，存放上下文信息，通过它来遍历视图树，支撑UI结构。
RenderObject (渲染树)用于应用界面的布局和绘制，负责真正的渲染，保存了元素的大小，布局等信息。

Widget是Widget Tree的所有节点的基类。
Widget子类主要分为三类。
1. RenderObjectWidget子类，具体来说分为SingleChildRenderObjectWidget(单子节点容器)，LeafRenderObjectWidget(叶子节点)，MultiChildRenderObjectWidget(多子节点容器)，
    共同特点是都对应一个RenderObject的子类，可以进行Layout，Paint等逻辑。
2. StatelessWidget，StatefulWidget，它们是开发者最常用的Widget，自身不具备绘制能力，但是可以组织和配置RenderObjectWidget类型的Widget
3. ProxyWidget，具体来说又分为ParentDataWidget和InheritedWidget，特点是为其子节点提供额外的数据，例如InheritedWidget

Element
1. 每个element都有一个对应的widget，反过来也成立，即通过createElement方法
2. BuildContext就是一个element对象

RenderObject
1. 每个子类都对应一个RenderObjectWidget类型的Widget节点
2. RenderView是一个特殊的RenderObject，是整个RenderTree的根节点
3. RenderObject是RenderAbstractViewport，RenderViewport会实现其借款，并间接继承自RenderBox
4. RenderBox和RenderSliver是Flutter中最常见的RenderObject，RenderBox负责行列等常规布局，RenderSliver负责列表内每个Item布局
