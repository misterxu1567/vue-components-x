> 基于vue的自定义对话框

### NPM

``` bash
npm install vue-confirm-x -D
```
### Example

```
<template>
    <div id="app">
        <Confirm :msg="msg" animation="scale-fade" @callback="feedbackFn" v-if="status"></Confirm>
    </div>
</template>
    export default {
        name: 'App',
        components: {
            Confirm
        },
        data () {
            return {
                msg:{
                    title: '我是标题',
                    text: '我是描述',
                    btnSure: '确认',
                    btnCancel: '取消'
                },
                status: false
            }
        },
        methods: {
            showFn () {
                this.state = true;
            },
            // 回调函数
            feedbackFn (state) {
                // 隐藏
                !state ? this.status = false : '';
            }
        }
    }

```
## Api
### 参数
| Name                 | Type      | Default      | Description                                                        |
|----------------------|-----------|--------------|--------------------------------------------------------------------|
| msg                  | `Object`  | `{ title: '我是标题',text: '我是描述',btnSure: '确认',btnCancel: '取消' }`                   | 对话框的显示文案 |
| animation            | `String`  | `slide-fade`  | 对话框显示动画（slide-fade / scale-fade）        |
| feedbackFn           | `Function`|               | 回调函数       |
| state                | `Boolean` |               | 回调函数内的参数，true表示确认，false表示取消 |

### 版本迭代说明

v1.1.0 优化了动画，并添加了一个动画选择类，修复了上个版本的按钮文案错位
