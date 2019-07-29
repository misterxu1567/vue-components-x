> 基于vue的全局loading

### NPM

``` bash
npm install vue-loading-x --save-dev
```
### Example

```
/*在main.js内*/
import Loading from 'vue-loading-x';
vue.use(Loading);

/*在组件内*/
new Vue({
    methods: {
        showLoading () {
            this.$loadingX.show();
        },
        hideLoading () {
            this.$loadingX.hide();
        }
    }
})

```
## Api
### 参数
| Name                 | Type      | Default      | Description                                                        |
|----------------------|-----------|--------------|--------------------------------------------------------------------|
| show                  | `Function`  |       | 显示         |
| hide                  | `Function`  |       | 隐藏         |


