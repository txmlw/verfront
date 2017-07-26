<template>
    <div>
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item><i class="el-icon-date"></i> 设置</el-breadcrumb-item>
                <el-breadcrumb-item>Svn设置</el-breadcrumb-item>
            </el-breadcrumb>
        </div>
        <div class="form-box">
            <el-form ref="form" :model="form" label-width="80px" id="fm">
                <el-form-item label="应用系统">
                    <el-checkbox-group v-model="form.systemcode">
                        <el-checkbox label="承保" name="systemcode"></el-checkbox>
                        <el-checkbox label="理赔" name="systemcode"></el-checkbox>
                        <el-checkbox label="双核" name="systemcode"></el-checkbox>
                        <el-checkbox label="收付" name="systemcode"></el-checkbox>
                    </el-checkbox-group>
                </el-form-item>
                <el-form-item label="Svn 地址">
                    <el-input v-model="form.svnUrl"></el-input>
                </el-form-item>
                <el-form-item label="Svn 用户">
                    <el-input v-model="form.svnUser"></el-input>
                </el-form-item>
                <el-form-item prop="password" v-model="form.svnPwd" label="Svn 密码">
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
            return {
                form: {
                    svnUrl: '',
                    svnUser: '',
                    svnPwd: '',
                    systemcode: ['承保'],
                }
            }
        },
        methods: {
            submitForm() {
                this.$ajax({
                    method: 'post',
                    url: '/setting/svnSave',
                    data: {
                        firstName: 'Fred'
                    }
                })
                this.$message.success('提交成功！');
            }
        }
    }
</script>