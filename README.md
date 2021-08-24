# virtual-list
optimization for a large amount of data that needs to be rendered as list items
### 提示
项目是一个demo，可以直接运行
### 关于
这是根据学习virtual-scroll源码的思想来实现的，可以支持自定义列数和预渲染的个数
### 关于使用
如果需要的话可以提出其中的virtualList.vue来使用，virtualList.vue与外部是低耦合的。
#### API
<font color="#09C7F7">size</font>:每个元素的高度，这个版本只支持等高的元素<br>
<font color="#09C7F7">remain</font>:可视区域的元素个数<br>
<font color="#09C7F7">items</font>:传入的数据源，类型为数组<br>
<font color="#09C7F7">columns</font>:展示的列数<br>
<font color="#09C7F7">preRender</font>:预渲染的元素个数<br>
<font color="blur">slot->#item</font>: 支持每一个元素自定义内容<br> 
**注意：其中remain和preRender必须是columns的整数倍，不然会引起错误**
