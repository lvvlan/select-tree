<template>
    <div id="select-tree" style="width: 300px;">
        <Select
            v-model="selectVal"
            style="width: 100%;"
            multiple
            popper-class="select-tree__popper"
            @click.native="handleSelectFocus"
            @remove-tag="handleRemoveTag"
        />
        <Tree
            ref="tree"
            style="width: 100%;"
            show-checkbox
            node-key="id"
            :data="data"
            :default-checked-keys="defaultTreeKeys"
            @check="handleCheckClick"
        />
    </div>
</template>

<script>
    import Select from 'element-ui/lib/select'
    import Tree from 'element-ui/lib/tree'
    import 'element-ui/lib/theme-chalk/icon.css'
    import 'element-ui/lib/theme-chalk/select.css'
    import 'element-ui/lib/theme-chalk/tree.css'

    export default {
        components: { Select, Tree },
        props: {
            value: {
                type: Array,
                default: function () {
                    return []
                }
            },
            data: {
                type: Array,
                default: function () {
                    return []
                }
            }
        },
        data () {
            return {
                selectVal: [],
                defaultTreeKeys: [],
                treeVisble: false,
                tempData: []
            }
        },
        methods: {
            setSelectData () {
                this.$data.selectVal = this.$refs.tree.getCheckedNodes(true).map(o => o.label)
                this.tempData = this.$refs.tree.getCheckedNodes(true)
                this.emitData()
            },
            setTreeData (v) {
                let val = this.$data.tempData.filter(o => o.label !== v)
                this.$data.tempData = val
                this.$refs.tree.setCheckedKeys(val.map(o => o.id))
                this.emitData()
            },
            emitData () {
                this.$emit('input', this.$refs.tree.getCheckedNodes(true).map(o => o.id))
                this.$emit('change', this.$refs.tree.getCheckedNodes(true))
            },
            handleDocumentClick () {
                this.$data.treeVisble = false
                this.$refs.tree.$el.style.maxHeight = '0'
                document.removeEventListener('click', this.handleDocumentClick)
            },
            handleSelectFocus () {
                if (this.$data.treeVisble) {
                    this.$refs.tree.$el.style.maxHeight = '0'
                } else {
                    this.$refs.tree.$el.style.maxHeight = '300px'
                    document.addEventListener('click', this.handleDocumentClick)
                }
                this.$data.treeVisble = !this.$data.treeVisble
            },
            handleCheckClick () {
                this.setSelectData()
            },
            handleRemoveTag (v) {
                this.setTreeData(v)
            }
        },
        created () {
            this.$data.defaultTreeKeys = this.value
        },
        mounted () {
            this.setSelectData()
        }
    }
</script>

<style scoped>
    #select-tree .el-tree {
        max-height: 0;
        overflow: hidden;
        transition: all ease-in .5s;
        overflow-y: scroll;
    }
</style>
<style>
    .select-tree__popper {
        display: none;
    }
</style>
