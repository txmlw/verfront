<template>
    <div class="table">
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item><i class="el-icon-menu"></i> 表格</el-breadcrumb-item>
                <el-breadcrumb-item>Vue表格组件</el-breadcrumb-item>
            </el-breadcrumb>
        </div>
        <el-table
                :data="resObj.data"
                style="width: 100%"
                :row-class-name="tableRowClassName">
            <el-table-column
                    prop="codecode"
                    label="配置代码"
                    width="180">
            </el-table-column>
            <el-table-column
                    prop="codename"
                    label="配置名称"
                    width="180">
            </el-table-column>
            <el-table-column
                    prop="codetype"
                    label="配置类型">
            </el-table-column>
        </el-table>
        <div class="block">
            <el-pagination
                    @size-change="handleSizeChange"
                    @current-change="handleCurrentChange"
                    :page-sizes="[5,10, 20, 50, 100,500]"
                    :page-size="queryInfo.perPageRows"
                    layout="total, sizes, prev, pager, next, jumper"
                    :total="resObj.pagination.total">
            </el-pagination>
        </div>
    </div>
</template>
<style>
    .el-table .info-row {
        background: #c9e5f5;
    }

    .el-table .positive-row {
        background: #e2f0e4;
    }
    div.block{
        padding-right: 5px;
    }
</style>

<script>
    import axios from 'axios';
    export default {
        data: function(){
            const self = this;
            return {
                url: '/tconfig/queryList',
                queryInfo: {
                    currentPage:1,
                    perPageRows:5,
                    condition:{"codename":"SVN用户名"}
                },
                resObj:{
                    success:false,
                    retMsg:"",
                    data:[],
                    pagination:{
                        total:0
                    }
                },
                columns: [
                    {
                        name: '代码',
                        key: 'codecode',
                    },
                    {
                        name: '名称',
                        key: 'codename',
                    },
                    {
                        name: '类型',
                        key: 'codetype',
                    }
                ],
                actions: [
                    {
                        text: 'Click',
                        class: 'btn-primary',
                        event(e, row) {
                            self.$message('选中的行数： ' + row.row.pcode);
                        }
                    }
                ],
                query:''
            }
        },
        components: {
            //Datasource
        },
        methods: {
            tableRowClassName(row, index) {
                if (index === 1) {
                    return 'info-row';
                } else if (index === 3) {
                    return 'positive-row';
                }
                return '';
            },
            handleSizeChange(val) {
                console.log(`每页 ${val} 条`);
                this.queryInfo.perPageRows = val;
                axios.post(this.url, this.queryInfo).then( (res) => {
                    this.tbData = res.data.data;
                })
            },
            handleCurrentChange(val) {
                console.log(`当前页: ${val}`);
                this.queryInfo.currentPage = val;
                axios.post(this.url, this.queryInfo).then( (res) => {
                    this.resObj = res.data;
                })
            },
            turnPage(){
                axios.post(this.url, this.queryInfo).then( (res) => {
                    this.resObj = res.data;
                })
            }
        },
        computed:{
        },
        beforeMount(){
            if(process.env.NODE_ENV === 'development'){
                this.url = '/tconfig/queryList';
            };
            axios.post(this.url, this.queryInfo).then( (res) => {
                this.resObj = res.data;
            })
        }
    }
</script>