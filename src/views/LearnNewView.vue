<script setup>
import HeaderTop from "@/components/HeaderTop.vue";
</script>

<template>
    <HeaderTop :param="param" />
    <div class="Item">
        <div class="box">
            <div v-if="resWord[index]" class="box-item">
                <div class="en">{{ index + 1 }} : {{ resWord[index].En }}</div>
                <div>{{ resWord[index].enClass }}:{{ resWord[index].EnCn }}</div>
            </div>
            <div>
                <button @click="changeReduceIndex" class="learn">上一个</button>
            </div>
            <div>
                <button @click="LearnEn" class="learn">确认学习</button>
            </div>
            <div>
                <button @click="changeAddIndex" class="learn">下一个</button>
            </div>
        </div>
        <div>
            <router-link href="" :class="{ 'navc': true, 'red': param === 'isLearnView' }" :to="{
                path: '/learn'
            }">返回</router-link>
        </div>
    </div>
</template>

<style scoped>
.navc {
    text-decoration: none;
}

.learn {
    width: 100px;
}

.en {
    font-size: 20px;
}

.box>div>div {
    margin: 10px;
}

.box>div {
    margin: 3px
}

.Item {
    display: flex;
    margin: 50px 182px;
    flex-direction: column;
}

.box {
    border-bottom: 1px dashed gray;
    padding: 10px;
    display: flex;
    flex-direction: column;
}
</style>

<script>

import axios from 'axios'

export default {
    data() {
        return {
            param: 'isLearnView',
            userToken: '',
            resWord: [{}],
            index: 0,
            userId: 0
        }
    },
    mounted() {
        this.getWord()
    },
    methods: {
        async getCookie() {
            this.userToken = localStorage.getItem('userToken')
        },
        async getWord() {
            await this.getCookie()
            const res = await axios({
                method: 'post',
                url: 'http://localhost:8000/enData/getWord',
                headers: {
                    authorization: this.userToken
                }
            })
            this.userId = res.data.userId
            this.resWord = res.data.message;
        },
        changeAddIndex() {
            // 检查是否达到数组边界
            if (this.index < this.resWord.length - 1) {
                this.index++;
            } else {
                // 如果已经到达数组末尾，则将索引重置为0
                this.index = 0;
            }
        },
        changeReduceIndex() {
            // 检查是否达到数组边界
            if (this.index != 0) {
                this.index--;
            } else {
                // 如果已经到达数组末尾，则将索引重置为length-1
                this.index = this.resWord.length - 1;
            }
        },
        async LearnEn() {
            if (confirm('您确定记住了该单词了吗?')) {
                // 用户点击了确认按钮
                await axios({
                    method: 'post',
                    url: 'http://localhost:8000/learn/userLean',
                    data: {
                        userId: this.userId,
                        wordId: this.resWord[this.index].id,
                        word: this.resWord[this.index].En
                    }
                })
                this.index++;
            } else {
                // 用户点击了取消按钮
                // 可以选择不执行任何操作或者做一些其他处理
            }
            if (this.index == this.resWord.length) {
                alert('您已完成本次单词的学习，即将跳转到学习页面');
                this.$router.push('/learn');
            }
        }
    }
}
</script>