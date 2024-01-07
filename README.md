<font size="6">Message.js</font>

**插件描述：**
一款优雅的原生JS页面消息提示插件，兼容性良好，无任何依赖。



**声明：**
此插件非笔者原创，笔者只做了部分内容的修改，以符合个人需求。以下为原插件来源信息：

- 原作者：或许吧（jesseqin）

- 转载地址：https://www.jq22.com/jquery-info23550

![message.js](https://raw.githubusercontent.com/WhiteSevs/Message.js/master/assets/intro-zh.jpg)

**使用：**

目前是把`CSS`集成到`JS`文件中了。

**html引入：**

```html
<!-- your html -->
<script src="../src/message.js"></script>
<script>
    var configs = {};
    // configs 为配置参数，可省略
    Qmsg.info("这是提示消息",configs);
</script>
```
**油猴引入**
```html
// @require https://github.com/WhiteSevs/Message.js/raw/master/src/message.js
```


**全局配置**

在引入message.js之前可以通过全局变量 QMSG_GLOBALS.DEFAULTS 来进行配置

```javascript
window.QMSG_GLOBALS = {
    DEFAULTS: {
        showClose:true,
        timeout: 5000
    }
}
```

或者通过`Qmsg.config({})`来动态修改全局配置`(建议用这个)`:

```javascript
Qmsg.config({
    showClose:true,
    timeout: 5000
})
```

所有支持的配置信息如下:

| 参数名  | 类型  | 描述                                  | 默认  |
| ----------- | --------- | ----------------------------------------- | --------- |
| animation | Boolean | 是否使用弹出动画 | true |
| autoClose | Boolean | 是否自动关闭 | true |
| content | Number |  提示的消息内容  | 空 |
| html | String | 是否将内容作为 html 渲染 | false|
| position     | Function  | 弹出位置 topleft、top、topright、left、center、right、bottomleft、bottom、bottomright，不区分大小写 | top |
| maxNums     | Number    | 页面中最多显示消息(autoClose: true)的数量 | 5         |
| onClose | Function | 关闭时的回调函数 | null |
| showClose | Boolean   | 是否显示关闭图标 | false |
| showIcon | Boolean | 是否显示左边的图标 | true |
| showMoreContent | Boolean | 是否显示更多内容(换行) | false |
| showReverse | Boolean | 是否使弹出方式逆反 | false |
| timeout | Number | 自动关闭时，消息的持续显示时间，单位 ms | 2500 |
| type | String | 弹出类型 | info |
| zIndex | Number | z-index的层级 | 50000 |


**Qmsg支持的方法**

```javascript
Qmsg.config() // 配置
Qmsg.info() // 信息
Qmsg.warning() // 警告
Qmsg.error() // 错误
Qmsg.success() // 成功
Qmsg.loading() // 加载中
```

以上方法均可传递 1-2 个参数，如下：

```javascript
Qmsg.loading("我是加载条");
Qmsg.info("给你个眼神，你懂得",{
    showClose:true,
    onClose:function(){
        console.log('我懂了')
    }
})
Qmsg.error({
    content:"1+1=3",
    timeout:5000
})
```

**注意：**`Qmsg.loading()`默认设置`autoClose = false`，一般来说需要手动关闭：

```javascript
var loadingMsg = Qmsg.loading('我是加载条');
// do something
loadingMsg.close();
```

如需要自动关闭则需要如下调用:

```javascript
Qmsg.loading("我是加载条",{
    autoClose:true
})
// 或者
Qmsg.loading({
    autoClose:true,
    content:"我是加载条"
})
```

**Qmsg.closeAll()**

关闭所有消息，包括`autoClose = false`的消息

```javascript
var aMsg = Qmsg.info("这是个info消息")
```

**close()**

关闭当前消息，会触发`onClose`回调函数。

```javascript
aMsg.close()
```

**destroy()**

销毁消息，不会触发`onClose`回调函数。

```javascript
aMsg.destroy()
```
**setText(text:String)**

对已弹出的内容进行修改

```javascript
aMsg.setText("这是进行修改的info消息")
```

**setHTML(html:String)**

对已弹出的内容进行修改

```javascript
aMsg.setHTML("<a href='javascript:;' target='_blank'>这是进行修改的info消息超链接</a>")
```

**关闭左边的图标显示**

```javascript
Qmsg.config({
    showIcon: false
})
Qmsg.info("这个没有图标")
// 或者
Qmsg.info("这个没有图标",{
    showIcon: false
})
```

**设置九宫格位置弹出**

```javascript
Qmsg.info("左上角",{
    position: "topleft"
})

Qmsg.info("顶部",{
    position: "top"
})

Qmsg.info("右上角",{
    position: "topright"
})

Qmsg.info("左边",{
    position: "left"
})

Qmsg.info("中间",{
    position: "center"
})

Qmsg.info("右边",{
    position: "right"
})

Qmsg.info("左下角",{
    position: "bottomleft"
})

Qmsg.info("底部",{
    position: "bottom"
})

Qmsg.info("右下角",{
    position: "bottomright"
})
```