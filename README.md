# 树表控件 treeTable v 1.4.2

作者: benzhan(詹潮江)

[demo](https://sogrey.github.io/jquery.treeTable.js/treeTable%20v1.4.2/demo/treeTable.html)

## 简介

treeTable是跨浏览器、性能很高的jquery的树表组件，它使用非常简单，只需要引用jquery库和一个js文件，接口也很简单。

#### 优点

- 兼容主流浏览器: 支持IE6和IE6+, Firefox, chrome, Opera, Safari
- 接口简洁: 在普通表格的基础上增加父子关系的自定义标签就可以
- 组件性能高: 内部实现了只绑定了table的事件、使用了css sprite合并图片等
- 提供两种风格: 通过参数来设置风格

#### 接口

##### 配置参数


- `theme`: string {主题，有两个选项：default、vsStyle. 默认:default}
- `expandLevel`: int {树表的展开层次. 默认:1}
- `column`: int {可控制列的序号. 默认:0，即第一列}
- `onSelect`: function {拥有controller自定义属性的元素的点击事件，return false则中止展开. 默认值:
function($treeTable, id) {       //$treeTable 当前树表的jquery对象.       //id 当前行的id            //返回false，则直接退出，不会激发后面的beforeExpand和子节点的展开       return true; }
- `beforeExpand`: {展开子节点前触发的事件, 默认值：
function($treeTable, id) {       //$treeTable 当前树表的jquery对象.       //id 当前行的id }

##### 属性说明

- `id`: string 行的id
- `pId`: string 父行的id
- `controller`: bool 指定某一个元素是否可以控制行的展开
- `hasChild`: bool 指定某一个tr元素是否有孩子（动态加载需用到）
- `isFirstOne`: bool 指定某一个tr元素是否是第一个孩子（自动生成属性，只读）
- `isLastOne`: bool 指定某一个tr元素是否是最后一个孩子（自动生成属性，只读）
- `prevId`: string 前一个兄弟节点的id（自动生成属性，只读）
- `depth`: string 当前行的深度（自动生成属性，只读）


##### 使用方式


`$("#元素id").treeTable({})` 如:

引用的文件

	<script src="/script/jquery.js" type="text/javascript"> </script> 
	<script src="/script/treeTable/jquery.treeTable.js" type="text/javascript"> </script>

js代码

    <script type="text/javascript">
        $(function(){
            var option = {
                theme:'vsStyle',
                expandLevel : 2,
                beforeExpand : function($treeTable, id) {
                    //判断id是否已经有了孩子节点，如果有了就不再加载，这样就可以起到缓存的作用
                    if ($('.' + id, $treeTable).length) { return; }
                    //这里的html可以是ajax请求
                    var html = '<tr id="8" pId="6"><td>5.1</td><td>可以是ajax请求来的内容</td></tr>'
                             + '<tr id="9" pId="6"><td>5.2</td><td>动态的内容</td></tr>';

                    $treeTable.addChilds(html);
                },
                onSelect : function($treeTable, id) {
                    window.console && console.log('onSelect:' + id);
                    
                }

            };
            $('#treeTable1').treeTable(option);
        });
    </script> 
