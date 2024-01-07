<script setup>

import HeaderTop from "@/components/HeaderTop.vue";
</script>

<template>
    <HeaderTop :param="param" />
    <div class="Item">
        <div class="Item-title">英语学习</div>
        <div class="learnEn"> <!--  -->
            <router-link href="" class="learnEn-item" :to="{
                path: '/learnNew'
            }">新词学习
            </router-link>
            <a href="" class="learnEn-item"  @click="test">
                快速自检
            </a>
            <router-link href="" class="learnEn-item" :to="{
                path: '/learn/queryEn'
            }">单词查询
            </router-link>
        </div>
        <div class="Item-title">专项训练</div>
        <div class="learnEn"> <!--  -->
            <a href="" class="learnEn-item" @click="test">
                单词训练
            </a>
            <router-link href="" class="learnEn-item" :to="{
                path: '/learn/wordSpelling'
            }">全拼默写
            </router-link>
            <router-link href="" class="learnEn-item" :to="{
                path: '/learn/wordSpellingIncomplete'
            }">填空拼写
            </router-link>
            <a href="" class="learnEn-item"  @click="test">
                中文选词
            </a>
        </div>
    </div>
</template>

<style scoped>
.Item-title {
    margin: 20px;
    font-size: 20px;
    color: red;
}

.Item {
    display: flex;
    margin: 50px 182px;
    flex-direction: column;
}

.learnEn {
    border-bottom: 1px dashed rgb(178, 177, 177);
    display: flex;

}

.learnEn-item {
    text-decoration: none;
    margin: 10px;
    width: 100px;
    padding: 20px;
    color: black;
    border-radius: 8px;
    background-color: rgba(175, 228, 246, 0.6);
}

.learnEn-item:hover {

    background-color: rgba(167, 214, 230, 0.8);
}

.learnEn-item-admin {
    text-decoration: none;
    margin: 10px;
    width: 100px;
    padding: 20px;
    color: black;
    border-radius: 8px;
    background-color: rgba(65, 187, 227, 0.2);
}

.learnEn-item-admin:hover {

    background-color: rgba(6, 152, 201, 0.5);
}
</style>

<script>

import axios from 'axios'

export default {
    data() {
        return {
            param: 'isLearnView',
            userToken: ''
        }
    },
    mounted() {
        this.getCookie()
    },
    methods: {
        test() {
            alert('未编写该功能')
        },
        getCookie() {
            this.userToken = localStorage.getItem('userToken')
        },
        async getM() {
            const res = await axios({
                method: 'post',
                url: 'http://localhost:8000/enData/getWordMasteredLimit',
                headers: {
                    authorization: this.userToken
                }
            })
            console.log(res)
        }
    }
}
</script>