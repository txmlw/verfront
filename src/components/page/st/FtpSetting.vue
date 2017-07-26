<template>
    <div>
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item><i class="el-icon-date"></i> 设置</el-breadcrumb-item>
                <el-breadcrumb-item>Ftp设置</el-breadcrumb-item>
            </el-breadcrumb>
        </div>
        <div class="form-box">
            <el-form ref="form" :model="form" label-width="80px">
                <el-form-item label="应用系统">
                    <el-checkbox-group v-model="form.systemcode">
                        <el-checkbox label="承保" name="systemcode"></el-checkbox>
                        <el-checkbox label="理赔" name="systemcode"></el-checkbox>
                        <el-checkbox label="双核" name="systemcode"></el-checkbox>
                        <el-checkbox label="收付" name="systemcode"></el-checkbox>
                    </el-checkbox-group>
                </el-form-item>
                <el-form-item label="Ftp 地址">
                    <el-input v-model="form.ftpUrl"></el-input>
                </el-form-item>
                <el-form-item label="协议">
                    <el-select v-model="form.ftpProtocl" placeholder="请选择">
                        <el-option key="ftp" label="Ftp" value="ftp"></el-option>
                        <el-option key="sftp" label="Sftp" value="sftp"></el-option>
                    </el-select>
                </el-form-item>
                <el-form-item label="端口">
                    <el-input v-model="form.ftpPort"></el-input>
                </el-form-item>
                <el-form-item label="Ftp 用户">
                    <el-input v-model="form.ftpUser"></el-input>
                </el-form-item>
                <el-form-item prop="password" v-model="form.ftpPwd" label="Ftp 密码">
                    <el-input type="password"></el-input>
                </el-form-item>
                <el-form-item label="上传服务目录">
                    <el-input v-model="form.ftpUpDir"></el-input>
                </el-form-item>
                <el-form-item label="本地存放目录">
                    <el-input v-model="form.ftpUpDir"></el-input>
                </el-form-item>
                <el-form-item label="服务器执行脚本">
                    <el-input v-model="form.ftpSh"></el-input>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary" @click="onSubmit">提交</el-button>
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
                    ftpUrl: '',
                    ftpProt: '',
                    ftpProtocl: '',
                    ftpUser: '',
                    ftpPwd: '',
                    systemcode: ['承保'],
                }
            }
        },
        methods: {
            onSubmit() {
                this.$message.success('提交成功！');
            }
        }
    }
</script>