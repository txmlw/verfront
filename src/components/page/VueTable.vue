<template>
    <div class="table">
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item><i class="el-icon-menu"></i> 表格</el-breadcrumb-item>
                <el-breadcrumb-item>Vue表格组件</el-breadcrumb-item>
            </el-breadcrumb>
        </div>
        <datasource language="en" :table-data="getData" :columns="columns" :pagination="information.pagination"
                :actions="actions"
                v-on:change="changePage"
                v-on:searching="onSearch"></datasource>
    </div>
</template>

<script>
    import axios from 'axios';
    import Datasource from 'vue-datasource';
    export default {
        data: function(){
            const self = this;
            return {
                url: '/queryListJson',
                information: {
                    pagination:{},
                    data:[]
                },
                queryInfo: {
                    currentPage:1,
                    perPageRows:15,
                    condition:{"pname":"SVN用户名"}
                },
                columns: [
                    {
                        name: '代码',
                        key: 'pcode',
                    },
                    {
                        name: '名称',
                        key: 'pname',
                    },
                    {
                        name: '类型',
                        key: 'ptype',
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
            Datasource
        },
        methods: {
            changePage(values) {
                this.information.pagination.currentPage = values.page;
                this.information.pagination.perPageRows = values.perpage;
                this.queryInfo.currentPage = values.page;
                this.queryInfo.perPageRows = values.perpage;
                //this.information.data = this.information.data;
                axios.post(this.url, this.queryInfo).then( (res) => {
                    this.information = res.data;
                })
            },
            onSearch(searchQuery) {
                this.query = searchQuery;
                axios.post(this.url, this.queryInfo).then( (res) => {
                    this.information = res.data;
                })
            }
        },
        computed:{
            getData(){
                const self = this;
                return self.information.data.filter(function (d) {
                    return d;
                    //if(d.name.indexOf(self.query) > -1){

                    //}
                })
            }
        },
        beforeMount(){
            if(process.env.NODE_ENV === 'development'){
                this.url = '/queryListJson';
            };
            axios.post(this.url, this.queryInfo).then( (res) => {
                this.information = res.data;
            })
        }
    }
</script>

<style src="../../../static/css/datasource.css"></style>