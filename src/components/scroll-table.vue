<template>
    <el-table
            :ref="tableRef"
            :data="tableData"
            :border="isBorder"
            :stripe="isStripe"
            :row-class-name="highlight"
            style="width: 100%">
        <el-table-column type="index" width="50" v-if="isShowIndex"></el-table-column>
        <slot></slot>
    </el-table>
</template>
<script>
    export default {
        props: {
            // table basic option
            // 表格border
            isBorder: {
                type: Boolean,
                default: false
            },
            // 表格斑马线
            isStripe: {
                type: Boolean,
                default: false
            },
            // data
            // 需要表格滚动的时候，为了独立设置top tableRef 必传
            tableRef: {
                type: String,
                default: ''
            },
            isShowIndex: {
                type: Boolean,
                default: false
            },
            tableData: {
                type: Array,
                default: function () {return []}
            },
            // auto scroll option
            isAutoScroll: {
                type: Boolean,
                default: false
            },
            // auto highlight
            isHighlight: {
                type: Boolean,
                default: false
            },
            // default tr height
            moveDistance: {
                type: [Number, String],
                default: 45
            },
            intervalTime: {
                type: Number,
                default: 1500
            },
            intervalCallback: {
                type: Function,
                default: function () {}
            }
        },
        data () {
            return {
                activeIndex: 0
            }
        },
        watch: {
            'top': function (value) {
                if (this.isAutoScroll) {
                    if (typeof this.$refs[this.tableRef].bodyWrapper !== 'undefined') {
                        this.$refs[this.tableRef].bodyWrapper.style.top = value
                    }
                }
            },
            immediate: true
        },
        computed: {
            top() {
                return this.isAutoScroll ? -this.activeIndex * this.moveDistance + 'px' : '0px' // 定义移动的单元高度
            }
        },
        mounted () {
            if (this.isAutoScroll) {
                setInterval(() => {
                    // 自定义滚动 出勤率
                    if (this.activeIndex < this.tableData.length && this.tableData.length > 0/* this.towerListArr.length */) {
                        this.activeIndex += 1
                        this.intervalCallback && this.intervalCallback(this.activeIndex)
                    } else {
                        this.activeIndex = 0
                    }
                }, this.intervalTime)
            }
        },
        methods: {
            highlight (row) {
                if (this.isHighlight && row.rowIndex === this.activeIndex) {
                    return 'highlight-bg'
                } else {
                    return ''
                }
            }
        }
    }
</script>
