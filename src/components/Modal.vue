<script setup>
const types = [
  "Начинается через",
  "Заканчивается сегодня",
  "Заканчивается завтра",
  "Заканчивается через",
  "Закончилось",
];
</script>
<template>
  <div class="sortingType" >
    <p v-for="(type, index) in types" :key="index">{{ type }}</p>
  </div>
</template>

<style lang="scss" scoped>
.sortingType {
  position: absolute;
  top: 87px;
  right: 37px;
  background: #080d6b;
  color: white;
  width: 200px;
  height: 200px;
  padding: 20px;
  text-align: left;
  p {
    cursor: pointer;
  }
  p:hover {
    font-weight:700;
  }
}
</style>
