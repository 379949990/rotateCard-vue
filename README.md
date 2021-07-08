# rotateCard-vue



#### 这是一个适用于Vue框架的翻转卡片组件的简单封装。



#### 使用方式：

##### 				将rotateCard.vue文件添加至项目并在需要的地方作为组件引入即可。



- ##### rotate-card组件宽高默认为父元素的宽高；

- ##### rotate-item-front元素为卡片正面展示的内容，可直接定义事件或添加样式；
- ##### Rotate-item-back元素为卡片背面展示的内容，可直接定义事件或添加样式；
- ##### rotate-card组件默认为横向翻转，如需纵向翻转可向rotate-card添加属性rotate=“x”或rotate=“X”；
- ##### rotate-card组件默认触发翻转的行为为“click”，“mouseleave”时会自动回正；



#### 示例代码：

```vue
<template>
	<div class="rotate-card-box">
    <rotate-card>
      <rotate-item-front class="rotate-card-front">
        正面内容
      </rotate-item-front>
      <rotate-item-back class="rotate-card-back">
        背面内容
      </rotate-item-back>
    </rotate-card>
  </div>
</template>

<script>
	import rotateCard from "./rotateCard.vue";
  export default {
    data() {},
    components: { 
      rotateCard,
    },
   	// ...
  }
</script>

<style>
  .rotate-card-box {
    width: 360px;
    height: 480px;
  }
  .rotate-card-front {
    background-color: #dc8f8f;
    // ...
  }
  .rotate-card-back {
    background-color: #3c8399;
    // ...
  }
</style>
```

