<script setup>

import HeaderTop from "@/components/HeaderTop.vue";
</script>

<template>
    <HeaderTop :param="param" />
    <div class="Item">
        <div class="item-top">
            <div v-if="to == 'en'" @click="changeTo" class="changeBox">中译英</div>
            <div v-else @click="changeTo" class="changeBox">英译中</div>
            <div @click="fanyi" class="changeBox">立即翻译</div>
        </div>
        <div class="item-bottom">
            <div>
                <textarea type="text" v-model="inputValue" placeholder="请输入要查询的单词(或者进行长句翻译" class="input-box"></textarea>
            </div>
            <div class="getInfo">
                {{ test }}
            </div>
        </div>
    </div>
</template>

<style scoped>
.item-top{
    display: flex;
    flex-direction: row;
}
.item-bottom{
    margin-top: 20px;
    display: flex;
    flex-direction: row;
}
.changeBox {
    margin: 0px 10px;
    width: 100px;
    border-radius: 5px;
    padding: 6px;
    border: 1px solid black;
}
.changeBox:hover {
    background: rgb(188, 188, 188);
}

.Item {
    display: flex;
    margin: 50px 182px;
    flex-direction: column;
}

.getInfo {
    display: flex;
    width: 500px;
    padding: 10px;
    height: 160px;
    border-radius: 0px 10px 10px 0px;
    border: 1px solid rgba(200, 200, 200, 0.6);
    background: rgba(200, 200, 200, 0.6);
    font-size: 20px;
    font-weight: bold;
}

.input-box {
    resize: none;
    display: flex;
    width: 500px;
    height: 160px;
    padding: 10px;
    border: 1px solid rgb(169, 168, 168);
    border-radius: 10px 0px 0px 10px;
    font-size: 20px;
    font-weight: bold;
}

.input-box:focus {
    outline: 1px solid #4395ff;
}


</style>

<script>

import axios from 'axios'

export default {
    data() {
        return {
            param: 'isLearnView',
            userToken: '',
            test: '',
            inputValue: '',
            to: 'en',
        }
    },
    mounted() {
    },
    methods: {
        async fanyi() {
            const res = await axios({
                method: 'post',
                url: 'http://localhost:8000/learn/translate',
                data: {
                    "q": this.inputValue,
                    "to": this.to
                }
            })
            this.test = res.data.trans_result[0].dst
            console.log(res)
        },
        changeTo() {
            if (this.to == 'en') {
                alert('当前英文翻译中文')
                this.to = 'zh'
            } else {
                alert('当前中文翻译英文')
                this.to = 'en'
            }
        }
    }
}
</script>