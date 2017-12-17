<template>
    <el-form label-width="5em" ref="form" status-icon
             :model="formItem"
             :rules="formRules"
             @keypress.native.enter="onSubmit">
        <el-form-item label="用户名" prop="userName">
            <el-input type="text" v-model="formItem.userName" />
        </el-form-item>
        <el-form-item label="密码" prop="password">
            <el-input type="password" v-model="formItem.password" />
        </el-form-item>
        <el-form-item>
            <el-button type="primary" :loading="submitLoading" @click="onSubmit">提交</el-button>
            <el-button @click="onReset">重置</el-button>
        </el-form-item>
    </el-form>
</template>

<script>
import {LOGIN} from '@/store/action_type.js';

export default {
    data () {
        return {
            submitLoading: false,
            formItem: {
                userName: '',
                password: ''
            },
            formRules: {
                userName: [
                  {required: true, message: '请输入用户名', trigger: 'change'}
                ],
                password: [
                  {required: true, message: '请输入密码', trigger: 'change'}
                ]
            }
        };
    },
    mounted () {
    },
    methods: {
        onSubmit () {
            if (this.submitLoading) return;
            this.$refs.form.validate((valid) => {
                if (valid) {
                    this.submitLoading = true;
                    this.$store.dispatch(LOGIN, Object.assign({}, this.formItem));
                }
            });
        },
        onReset () {
            this.$refs.form.resetFields();
        }
    }

};
</script>
