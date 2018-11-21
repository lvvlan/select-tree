https://img.shields.io/badge/select--tree-npm-orange.svg

# Vue组件：select-tree

[![npm](https://img.shields.io/badge/select--tree-npm-orange.svg)](https://www.npmjs.com/package/select-tree)

一个 select-tree Vue组件，基于element-ui

## 安装

```bash
npm install select-tree
```

## 用法

```js
<div id="app">
    <select-tree v-model="val" :data="myData" @change="handleChange" />
</div>

interface TreeItem {
    id: number,
    label: string,
    children: Array<TreeItem>
}

val: Array<number> = [3, 5];

myData: Array<TreeItem> = [{
        id: 1,
        label: '一级 1',
        children: [{
            id: 4,
            label: '二级 1-1',
            children: [{
            id: 9,
            label: '三级 1-1-1'
            }, {
            id: 10,
            label: '三级 1-1-2'
            }]
        }]
        }, {
            id: 2,
            label: '一级 2',
            children: [{
                id: 5,
                label: '二级 2-1'
            }, {
                id: 6,
                label: '二级 2-2'
            }]
        }, {
            id: 3,
            label: '一级 3',
            children: [{
                id: 7,
                label: '二级 3-1'
            }, {
                id: 8,
                label: '二级 3-2'
            }]
        }]

handleChange (v) {
    console.log('选中值', v)
    console.log(this.$data.val)
} 

```

## 许可证

[MIT](http://hotoo.mit-license.org/)