<template>
    <el-table
        :data="tableData" :span-method="objectSpanMethod"
        style="width: 100%" border>
        <el-table-column
            prop="productTemplateName"
            label="商品"
            width="180">
        </el-table-column>
        <el-table-column
            prop="orderItemKey"
            label="商品规格"
            width="180">
        </el-table-column>
        <el-table-column
            prop="productTemplateKey"
            label="产品名称">
        </el-table-column>
        <el-table-column
            prop="sku"
            label="其他信息">
        </el-table-column>
    </el-table>
</template>
<script>
export default {
    name: "attendanceHomepage",
    data() {
        return {
            tableData:[{
                    productTemplateName: "芝士仙贝*3",
                    orderItemKey: "11026",
                    productTemplateKey: "11",
                    sku: "1128"
                },
                {
                    productTemplateName: "芝士仙贝*3",
                    orderItemKey: "11026",
                    productTemplateKey: "12",
                    sku: "1128"
                },
                {
                    productTemplateName: "芝士仙贝*30",
                    orderItemKey: "110261",
                    productTemplateKey: "13",
                    sku: "1128"
                },
                {
                    productTemplateName: "芝士仙贝*30",
                    orderItemKey: "110261",
                    productTemplateKey: "14",
                    sku: "1128"
                },
                {
                    productTemplateName: "芝士仙贝*30",
                    orderItemKey: "110261",
                    productTemplateKey: "15",
                    sku: "1128"
                },
                {
                    productTemplateName: "芝士仙贝*30",
                    orderItemKey: "1102613",
                    productTemplateKey: "16",
                    sku: "1128"
                }],
            proarr: [],
            propos: 0,
            orderarr: [],
            orderpos: 0,
        }
    },
    mounted() {
        this.proarr = []
        this.orderarr = []
        for (let i = 0; i < this.tableData.length; i++) {
            if (i === 0) {
                this.proarr.push(1)
                this.propos = 0
                this.orderarr.push(1)
                this.orderpos = 0
            } else {
                // 判断当前元素与上一个元素是否相同（商品名）
                if (this.tableData[i].productTemplateName == this.tableData[i-1].productTemplateName) {
                    this.proarr[this.propos] +=1
                    this.proarr.push(0)
                } else {
                    this.proarr.push(1)
                    this.propos = i
                }
                // 判断当前元素与上一个元素是否相同（规格）
                if (this.tableData[i].orderItemKey == this.tableData[i-1].orderItemKey) {
                    this.orderarr[this.orderpos] +=1
                    this.orderarr.push(0)
                } else {
                    this.orderarr.push(1)
                    this.orderpos = i
                }
            }
        }
    },
    methods: {
        objectSpanMethod({ row, column, rowIndex, columnIndex }) {
            // console.log(row,column,rowIndex,columnIndex)
            if (columnIndex === 0) { // 第一列
                const _row = this.proarr[rowIndex]
                const _col = _row > 0 ? 1 : 0
                return {
                    rowspan: _row,// 跨行
                    colspan: _col // 跨列
                }
            }
            if (columnIndex === 1) { // 第二列
                const _row = this.orderarr[rowIndex]
                const _col = _row > 0 ? 1 : 0
                return {
                    rowspan: _row,// 跨行
                    colspan: _col // 跨列
                }
            }
        }
    }
}
</script>
