<script setup lang="ts">
import { ref } from 'vue';
import { ElForm, ElFormItem, ElInput, ElButton, ElTabPane } from 'element-plus';
import axios from 'axios';

const loginForm = ref({
    email: '',
    password: ''
});

function login() {
    const { email, password } = loginForm.value;
    const target_url = 'http://localhost:3000/user/login';
    const data = {
        email,
        password
    };

    axios.post(target_url, data, { withCredentials: true }).then(res => {
        if (res.status === 200) {
            alert('login success, code:' + res.status);
            localStorage.setItem('token', res.data.token);
            window.location.href = '/';
        } else {
            alert('login failed, code:' + res.status);
        }
    });

}

</script>

<template>
    <div>
        <h1>登录</h1>
        <p>邮箱：<input v-model="loginForm.email" /></p>
        <p>密码：<input v-model="loginForm.password" /></p>
        <a href="/register">注册</a><br>
        <button @click="login">登录</button>
    </div>
</template>

<style lang="less" scoped></style>