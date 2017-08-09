<template>
    <div>
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item><i class="el-icon-date"></i> 设置</el-breadcrumb-item>
                <el-breadcrumb-item>Svn设置</el-breadcrumb-item>
            </el-breadcrumb>
        </div>
        <div class="form-box">
            <el-form ref="form" :model="formData" label-width="80px" id="fm">
                <el-form-item label="应用系统">
                    <el-checkbox-group v-model="formData.systemcode">
                        <el-checkbox label="承保" name="systemcode"></el-checkbox>
                        <el-checkbox label="理赔" name="systemcode"></el-checkbox>
                        <el-checkbox label="双核" name="systemcode"></el-checkbox>
                        <el-checkbox label="收付" name="systemcode"></el-checkbox>
                    </el-checkbox-group>
                </el-form-item>
                <el-form-item label="Svn 地址">
                    <el-input v-model="formData.svnUrl"></el-input>
                </el-form-item>
                <el-form-item label="Svn 用户">
                    <el-input v-model="formData.svnUser"></el-input>
                </el-form-item>
                <el-form-item prop="password" v-model="formData.svnPwd" label="Svn 密码">
                    <el-input type="password"></el-input>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary" @click="submitForm()">提交</el-button>
                    <el-button>取消</el-button>
                </el-form-item>
            </el-form>
        </div>

    </div>
</template>

<script>
    export default {
        data: function(){
            const self = this;
            return {
                formData: {
                    svnUrl: '',
                    svnUser: '',
                    svnPwd: '',
                    systemcode: '承保',
                    codetype:'Svn_St',
                    status:'1'
                }
            }
        },
        methods: {
            submitForm() {
                debugger;
                console.log(this.formData);
                this.$ajax({
                    method: 'post',
                    url: '/tconfig/add',
                    data:this.formData
                    //data: {"codecode":this.formData.svnUrl,"codename":this.formData.svnUser,"codetype":"Svn_St","codevalue":this.formData.systemcode[0],"status":"1"}
                })
                this.$message.success('提交成功！');
            }
        }
    }
</script>