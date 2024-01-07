<template>
    <div class="item">
        <a class="logoBlock">
        </a>
        <!-- class="navc" -->
        <div>
            <router-link href="" :class="{ 'navc': true, 'red': param === 'isHome' }" :to="{
                path: '/'
            }">首页</router-link>
        </div>
        <div>
            <router-link href="" :class="{ 'navc': true, 'red': param === 'isLearnView' }" :to="{
                path: '/learn'
            }">学习</router-link>
        </div>
        <div>
            <router-link href="" :class="{ 'navc': true, 'red': param === 'isCinemaView' }" :to="{
                path: '/'
            }">训练</router-link>
        </div>
        <div>
            <router-link href="" :class="{ 'navc': true, 'red': param === 'isEnList' }" :to="{
                path: '/enList'
            }">词库</router-link>
        </div>
        <div>
            <router-link href="" :class="{ 'navc': true, 'red': param === 'isGewara' }" :to="{
                path: '/'
            }">社区</router-link>
        </div>
        <div>
        </div>
        <div v-if="!userToken">
            <router-link href="" :class="{ 'navc': true, 'red': param === 'isLogin' }" :to="{
               path: '/pc/login'
            }">登录</router-link>
        </div>
        <div v-else>
            <router-link href="" :class="{ 'navc': true, 'red': param === 'isGewara' }" :to="{
                path: '/'
            }">个人</router-link>
        </div>
        
        <button @click="UserOut" class="navcUserOut">注销</button>
        
        <!-- <div v-if="!userToken">
            <router-link href="" class="navcLogin" :to="{
                path: '/pc/login'
            }">Login</router-link>
        </div>
        <div v-else>
            <div class="userItem">
                <div class="userImg"></div>
                <button @click="UserOut" class="navcUserOut">注销</button>
            </div>
        </div> -->
        <!-- <router-link :to="{
            path: '/file/movieInfo',
            query: {
                testInfo: 123456
            }
        }">Home</router-link> -->
    </div>
</template>

<style scoped>
.logoBlock {
    margin-left: 300px;
}

.item {
    display: flex;
    width: 100%;
    height: 80px;
    border-bottom: 1px solid #d8d8d8
}

.logo {
    height: 95%;
}

.city {
    display: inline-block;
    text-align: center;
    margin: 0px 8px;
    height: 100%;
    font-size: 16px;
    margin-top: 28px;
}

.navc {
    text-decoration: none;
    text-align: center;
    display: inline-block;
    height: 80px;
    line-height: 80px;
    font-size: 18px;
    width: 70px;
    color: #333;
}


.navcLogin {
    text-decoration: none;
    text-align: center;
    display: inline-block;
    height: 80px;
    line-height: 80px;
    font-size: 18px;
    margin-left: 550px;
    width: 64px;
    color: #333;
}

.navcUserOut {
    margin-top: 25px;
    text-decoration: none;
    text-align: center;
    display: inline-block;
    height: 30px;
    font-size: 18px;
    width: 64px;
    color: red;
    border-radius: 20px;
    border: 0.5px solid black;
}

.userItem {
    display: flex;
    margin-left: 500px;
}

.userImg {
    margin: 0px 20px;
    margin-top: 20px;
    border-left: 1px solid hsl(0, 0%, 0%, 50%);
    border-right: 1px solid hsl(0, 0%, 0%, 50%);
    width: 80px;
    height: 60px;
}

.navc:hover {
    color: red;
}

.red {
    background-color: #ef4238;
    color: white;
}

.red:hover {
    color: white;
}
</style>

<script>
export default {
    props: ['param'],
    data() {
        return {
            userToken: '',
        }
    },
    mounted() {
        this.getCookie()

    },
    methods: {
        getCookie() {
            this.userToken = localStorage.getItem('userToken')
        },
        UserOut() {
            localStorage.setItem('userToken', '')
            alert('成功注销账号')
            this.$router.push('/')
            setTimeout(function () {
                window.location.reload();
            }, 100);
        }
    }
}
</script>