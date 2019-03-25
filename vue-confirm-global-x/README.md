> 基于vue的自定义 全局 对话框

### NPM

``` bash
npm install vue-confirm-global-x -D
```
### Example

```
import Confirm form 'vue-confirm-global-x';
vue.use(Confirm);

new Vue({
    methods: {
        showFn () {
            this.$confirm({
                title: '我是标题',
                text: '我是描述',
                btnSure: '确认',
                btnCancel: '取消',
            }).then(()=>{
                alert('确认')
            }, ()=>{
                alert('取消')
            })
        }
    }
})

```
## Api
### 参数
| Name                 | Type      | Default      | Description                                                        |
|----------------------|-----------|--------------|--------------------------------------------------------------------|
| then                 | `Function`|              | 第一个参数为执行确认回调，第二个为执行取消回调       |

### 其他说明
此组件全局引入一次，绑定于当前vue实例下，如果想使用某个页面单独引用的类型可移步查询 vue-confirm
