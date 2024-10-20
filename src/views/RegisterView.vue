<script setup lang="ts">
import { ref } from 'vue';
import axios from 'axios';

const name = ref('');
const email = ref('');
const pwd = ref('');

function register() {
    const target_url = 'http://localhost:3000/user/register';

    const data = {
        name: name.value,
        email: email.value,
        password: pwd.value
    };

    axios.post(target_url, data, {
        withCredentials: true,
        headers: {
            'Content-Type': 'application/json'
        }
    }).then(res => {
        if (res.status === 200) {
            alert('Register success, code:' + res.status);
            localStorage.setItem('token', res.data.token);
            window.location.href = '/';
        } else {
            alert('注册失败, Messgae: ' + res.data.message);
        }
    });

}

</script>

<template>
    <div>
        <h1>注册</h1>
        <br>
        <p>邮箱：<input v-model="email" /></p>
        <p>用户名：<input v-model="name" /></p>
        <p>密码：<input v-model="pwd" /></p>
        <a href="/login">登录</a><br>
        <button @click="register">注册</button>
    </div>


</template>

<style lang="less" scoped>
input {
    width: 200px;
    height: 30px;
}

button {
    width: 100px;
    height: 30px;
}

a {
    text-decoration: none;
}
</style>