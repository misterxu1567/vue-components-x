> 基于vue的自定义拖动条

<br/>
<img src="https://raw.githubusercontent.com/misterxu1567/img-static/master/slider.png" alt="自定义拖动条" width="100">

### NPM

``` bash
npm install @misterxu/vue-slider-x --save-dev
```
### Example

```

/*在组件内*/
<SliderVertical 
    v-model="value"
    :max="100"
    :min="0"
/>

// js
import SliderVertical from "@misterxu/vue-slider-x";

export default {
  name: "",
  components: {
    SliderVertical
  },
  data() {
    return {
      value: 40
    };
  },
  methods: {},
  watch: {
    // 监听拖动条变化
    value: function(newVal) {
      // ...
    }
  }
};


```
## Api
### 参数
| Name                 | Type      | Default      | Description                                                        |
|----------------------|-----------|--------------|------------|
| max                  | `Number`  |  100         | 最大值      |
| min                  | `Number`  |   0          | 最小值      |
| color                | `String`  |   #22d6af    | 拖动条颜色      |
| type                 | `String`  | 默认为垂直     | horizontal => 水平       |


