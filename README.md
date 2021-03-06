##EnterAnimation进场动画

### 用法
<pre><code>
var EnterAnimation = require('enter-animation');
var React = require('react');
React.render(&lt;EnterAnimation enter-transition={"left"}&gt
&lt;div&gtanim1&lt;/div&gt
&lt;div&gtanim2&lt;/div&gt
&lt;div&gtanim3&lt;/div&gt
&lt;/EnterAnimation&gt, container);

</code></pre>

### api
动画默认`right`

EnterAnimation标签下：


|参数             |类型    |详细                                                 |
|-----------------|-------|----------------------------------------------------|
|enter-transition|string/ array|执行动画的参数，有array和string两种类型，</br>下面详解；默认为null  |
|enter-delay|number|整个区块的延时，默认为0；</br>同startAnimation的delay|
|enter-interval|number|递增延时值，默认0.1|


dom标签下：


|参数             |类型    |详细                                                 |
|-----------------|-------|----------------------------------------------------|
|enter-data|object|同下面data参数详细 |

注：如enter-transition有值，则忽略子节点enter-data的数据；相反则遍历子节点上的enter-data的数据；在多没有数据时默认动画为`right`

##startAnimation的动画参数(EnterAnimation.to)；

页面进场动画的类，通过ＣＳＳ来快速完成页面刷新后的动画进场或子块的动画进场；

### 用法
<pre><code>
//js触发式：
var EnterAnimation=requre('enter-animation');
EnterAnimation.to(node,string);
EnterAnimation.to(node,data,delay);</code></pre>

### 参数说明

|参数             |类型    |详细                                                 |
|-----------------|-------|----------------------------------------------------|
|node             |string|要执行动画的dom（class,tag,id）;必要;  |
|data             |string / array|执行动画的参数，有array和string两种类型，下面详解；默认为null|
|delay            |number|整个区块的延时，默认为0                                |
|interval         |递增延时值。默认0.1|
|hideen           |boolean|在开始动画前隐藏掉html,默认为true;                     |

####data参数（string|array）;

支持css样式，和style直接添加动画；

为string时，自动遍历node下的子节点来执行data样式；

为array时，树状形dom结构，以([],new Array)为一档标签；
如：

<pre><code>&lt;div class="a"&gt;
&lt;div class="b"&gt;&lt;/div&gt;
&lt;div class="c"&gt;&lt;/div&gt;
&lt;/div&gt;</code></pre>

node用的是".a",做b,c的动画，那data为：[]为最外层div;
<pre><code>[
{type:"left"},
{type:"left"}
]</code></pre>

如果元素为多个时：

<pre><code>&lt;div class="a"&gt;
&lt;ul&gt;
&lt;li&gt;&lt;span&gt;&lt;/span&gt;&lt;/li&gt;
&lt;li&gt;&lt;span&gt;&lt;/span&gt;&lt;/li&gt;
&lt;li&gt;&lt;span&gt;&lt;/span&gt;&lt;/li&gt;
&lt;/ul&gt;
&lt;/div&gt;</code></pre>

处理每个li里的span的动画时，data为:

<pre><code>[
[{type:"left"}],
[{type:"left"}],
[{type:"left"}]
]</code></pre>


#####data参数详细

|参数             |默认值           |详细                                                 |
|-----------------|----------------|----------------------------------------------------|
|type            |null            |内置动画样式：<br/>`left` `right` `top` `bottom` `scale` `scaleFrom` `scaleX` `scaleY`;|
|style            |null           |style样式，如transform: translateX(100px),每个样式必须以;结束；`type`有值此项无效|
|direction        |"enter"         |动画进场或出场样式,以`enter``leave`两值;默认为"enter",|
|duration         |0.5             |动画的时间；|
|ease             |cubic-bezier(0.165, 0.84, 0.44, 1);|样式缓动;|
|delay            |0               |动画的延时;默认0,依照结构递增以上的`interval`|
|queueId          |0               |动画的线程，可为多线程|
