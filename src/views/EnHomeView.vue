<script setup>

import HeaderTop from "@/components/HeaderTop.vue";
</script>

<template>
  <HeaderTop :param="param" />
  <div class="Item">
    重要！使用前先点击下方按钮进行数据库单词数据的导入，否则无法使用！
    <div>数据导入</div>
    测试按钮
    <div>重置User表</div> 用户数据表
    <div>重置UserWord表</div> 存储用户学习进度表
    <div>重置en表</div> 存储英文单词表
    <div>重置所有表</div> 存储英文单词表
  </div>
</template>

<style scoped>
.Item {
  position: relative;
  display: flex;
  flex-direction: column;
  margin: 50px 182px;
}

.Item>div {
  width: 200px;
  border: 1px solid black;
}
</style>

<script>
export default {
  data() {
    return {
      param: 'isHome'
    }
  }
}
</script>