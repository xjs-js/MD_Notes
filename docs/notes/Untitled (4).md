---
tags: [Notebooks/no_one]
title: Untitled (4)
created: '2019-09-25T12:00:38.259Z'
modified: '2019-09-25T12:01:18.608Z'
---

# Untitled (4)
```cpp
<script src="//unpkg.com/vue/dist/vue.js"></script>
<script src="//unpkg.com/element-ui@2.12.0/lib/index.js"></script>
<div id="app">
<template>
  <el-table
    :data="tableData"
    style="width: 100%">
    <el-table-column type="expand" prop="names">
      <template slot-scope="scope">
        <el-table :data="scope.row.names">
          <el-table-column prop="name" label="名称">
              <template slot-scope="scope">
                <span>{{scope.row.name}} </span>
            </template>
            </el-table-column>
          <el-table-column prop="num" label="数量">
              <template slot-scope="scope">
                <span>{{scope.row.num}} </span>
            </template>
            </el-table-column>
          </el-table>
      </template>
    </el-table-column>
    <el-table-column
      label="商品 ID"
      prop="id">
    </el-table-column>
    <el-table-column
      label="商品名称"
      prop="name">
    </el-table-column>
    <el-table-column
      label="描述"
      prop="desc">
    </el-table-column>
  </el-table>
</template>
</div>
```

```cpp
@import url("//unpkg.com/element-ui@2.12.0/lib/theme-chalk/index.css");
.demo-table-expand {
    font-size: 0;
  }
  .demo-table-expand label {
    width: 90px;
    color: #99a9bf;
  }
  .demo-table-expand .el-form-item {
    margin-right: 0;
    margin-bottom: 0;
    width: 50%;
  }
```

```
var Main = {
    data() {
      return {
        tableData: [{
          names:[{name: 'apple', num:1}, {name: 'android', num:2}],
          id: '12987122',
          name: '好滋好味鸡蛋仔',
          category: '江浙小吃、小吃零食',
          desc: '荷兰优质淡奶，奶香浓而不腻',
          address: '上海市普陀区真北路',
          shop: '王小虎夫妻店',
          shopId: '10333'
        }, {
          names:[{name: 'apple1', num:1}, {name: 'androi2d', num:2}],
          id: '12987123',
          name: '好滋好味鸡蛋仔',
          category: '江浙小吃、小吃零食',
          desc: '荷兰优质淡奶，奶香浓而不腻',
          address: '上海市普陀区真北路',
          shop: '王小虎夫妻店',
          shopId: '10333'
        }, {
          names:[{name: 'apple', num:1}, {name: 'android', num:2}],
          id: '12987125',
          name: '好滋好味鸡蛋仔',
          category: '江浙小吃、小吃零食',
          desc: '荷兰优质淡奶，奶香浓而不腻',
          address: '上海市普陀区真北路',
          shop: '王小虎夫妻店',
          shopId: '10333'
        }, {
          names:[{name: 'apple', num:1}, {name: 'android', num:2}],
          id: '12987126',
          name: '好滋好味鸡蛋仔',
          category: '江浙小吃、小吃零食',
          desc: '荷兰优质淡奶，奶香浓而不腻',
          address: '上海市普陀区真北路',
          shop: '王小虎夫妻店',
          shopId: '10333'
        }]
      }
    }
  }
var Ctor = Vue.extend(Main)
new Ctor().$mount('#app')
```
