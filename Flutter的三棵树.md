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
