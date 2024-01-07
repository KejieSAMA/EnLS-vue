<script setup>
</script>

<template>
    <div class="user-item">
        <form action="" class="login-view">
            <div>
                UserName:
                <br>
                <input type="text" v-model="user_name" name="usename" placeholder="请输入账号名" class="input-item">
            </div>
            <div>
                password:
                <br>
                <input type="text" v-model="user_pwd" name="pwd" placeholder="请输入密码" class="input-item">
            </div>
            <button @click="UserLogin" class="login-button" type='button'>确定登录</button>
        </form>
        <a href="" @click="goRegisterView">没账号?!点击注册</a>
    </div>
</template>
<style scoped>
.user-item>a {
    padding: 10px;
}

.login-button {
    margin-top: 20px;
    width: 220px;
    height: 36px;
    background-color: #df2d2d;
    color: white;
    border-radius: 14px;
    border: none;
}

.input-item {
    width: 200px;
    padding: 5px;
    border: none;
    border-bottom: 1.5px solid rgb(164, 163, 163, 70%);
}

.input-item:focus {
    outline: none;
}

.login-view {
    margin: 50px;
}

.login-view>div {
    line-height: 28px;
    margin: 10px 0px;
    text-align: left;
}

.user-item {
    margin: 130px auto;
    border: 1px solid black;
    height: 340px;
}
</style>
<script>

import axios from 'axios'

export default {
    data() {
        return {
            /* username: "xiaojie99",
            user_pwd: "123456", */
            user_name: "",
            user_pwd: ""
        }
    },

    created() {
        this.userState()
    },
    methods: {
        userState() {
            // eslint-disable-next-line no-constant-condition
            if (localStorage.getItem('userToken')) {
                alert('您已登录')
                this.$router.push('/')
                setTimeout(function () {
                    window.location.reload();
                }, 100);
            }
        },
        goRegisterView(){
            this.$router.push('/pc/register')
        },
        async UserLogin() {
            await axios({
                method: 'post',
                url: 'http://localhost:8000/users/login',
                data: {
                    user_name: this.user_name,
                    password: this.user_pwd
                }
            }).then((res) => {
                if (res.code == 400) return;

                if (res.data.message == "用户登录成功") {
                    alert('恭喜登录成功!')
                    localStorage.setItem('userToken', res.data.result.token)
                    this.$router.push('/')
                    setTimeout(function () {
                        window.location.reload();
                    }, 100);
                } else {
                    alert(res.data.message)
                    localStorage.setItem('userToken', '')
                    window.location.reload();
                }
            })
        }
    }
}
</script>