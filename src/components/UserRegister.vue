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
                <input type="password" v-model="user_pwd" name="pwd" placeholder="请输入密码" ref="r_pwd1" class="input-item">
            </div>
            <div>
                password:
                <br>
                <input type="text" v-model="user_pwdaG" name="pwd" placeholder="请再次输入相同的密码" ref="r_pwd2" class="input-item">
            </div>
            <button @click="UserRegister" class="login-button" type='button'>确定注册</button>
        </form>
        <a href="" @click="goLogin">已有账号?点击登录!</a>
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
    height: 400px;
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
            user_pwd: "",
            user_pwdaG: ""
        }
    },
    methods: {
        goLogin() {
            this.$router.push('/pc/login')
        },
        async UserRegister() {

            if (this.user_pwd != this.user_pwdaG || !this.user_pwd) {
                alert('俩次密码不相同或存在空,请再次确认密码')
                this.$refs.r_pwd1.style.borderBottom = '1.5px solid rgba(249, 69, 69, 0.7)'
                this.$refs.r_pwd2.style.borderBottom = '1.5px solid rgba(249, 69, 69, 0.7)'
                return false
            }

            this.$refs.r_pwd1.style.borderBottom = '1.5px solid rgb(164, 163, 163, 70%)'
            this.$refs.r_pwd2.style.borderBottom = '1.5px solid rgb(164, 163, 163, 70%)'
            await axios({
                method: 'post',
                url: 'http://localhost:8000/users/register',
                data: {
                    user_name: this.user_name,
                    password: this.user_pwd
                }
            }).then((res) => {
                if (res.data.message == '用户注册成功') {
                    alert(`恭喜${res.data.result.user_name}注册成功,快去登录吧!`)
                    this.$router.push('/pc/login')
                } else {
                    alert(res.data.message)
                }
            })
        }
    },
}
</script>