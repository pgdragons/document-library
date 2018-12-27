1. Mint-UI
2. 9 宫格布局：

* 在 src/components/home 中使用

> Home.vue

```
<ul>
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
  <li>5</li>
  <li>6</li>
</ul>

.grid ul {
  margin: 0;
  padding: 0;
}
.grid li {
  list-style: none;
  float: left;
  width: 33.3%;
  backgorund-color: yellowgreen;
  text-align: center;
  height: 30px;
}
```

3. 组件封装

* 在 components 文件夹下新建 common
* 在 common 下新建 MyUl.vue

> MyUl.vue

```
<template>
  <ul>
    <slot></slot>
  </ul>
</template>
<script>
  export default {
    name: 'my-ul',
    data() {
      return {

      }
    }
  }
</script>
<style scoped>
ul {
  margin: 0;
  padding: 0;
}
</style>
```

MyLi.vue
```
<template>
  <li>
    <slot></slot>
  </li>
</template>
<script>
  export default {
    name: 'my-li',
    data() {
      return {

      }
    }
  }
</script>
<style scoped>
li {
  list-style: none;
  float: left;
  width: 33.3%;
  backgorund-color: yellowgreen;
  text-align: center;
  height: 30px;
}
</style>
```

* main.js 中引用自己的组件

> main.js

```
// 引入自己的 ul 和 li 组件
import MyUl from '@/components/Common/MyUl'
import MyLi from '@/components/Common/MyLi'

// 注册全局组件
Vue.component(MyUl.name, MyUl);
Vue.component(MyLi.name, MyLi);
```

* 在页面中使用

> Home.vue

```
<div class="grid">
  <my-ul>
    <my-li v-for="grid in grids">
      <a href="grid.url">
        <span :class="grid.className"></span>
        <span>{{grid.title}}</span>
      </a>
    </my-li>
  </my-ul>
</div>

data() {
  return {
    grids: [
      { className: "cms-news", title: "新闻资讯", url: "baidu.com" },
      { className: "cms-photo", title: "图文分享", url: "jsliang.top" },
    ]
  }
}
```