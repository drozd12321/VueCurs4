<template>
  <div class="cont" v-if="people.length > 0">
    <div class="inf cnt" v-for="pipl in people" :key="pipl.id">
      <span>{{ pipl.firstname }}</span>
      <button class="btn danger" @click="$emit('delete', pipl.id)">Удалить</button>
    </div>
  </div>
  <div class="cont" v-else>
    <div class="inf">
      <h3>Нет данных</h3>
      <button class="btn" @click="$emit('load')">Загрузить данные</button>
    </div>
  </div>
</template>
<script>
export default {
  emits: ['load', 'delete'],
  props: ['people'],
}
</script>
<style>
.cont {
  display: flex;
  flex-direction: column;
  gap: 10px;
  width: 70%;
  height: auto;
}
.inf {
  background-color: rgb(255, 255, 255);
  width: 100%;
  height: 100%;
  border-radius: 10px;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.4);
  text-align: center;
  padding: 7px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.btn {
  background-color: black;
  color: white;
  padding: 6px;
  margin-top: 7px;
  border-radius: 6px;
  font-size: 20px;
  border: none;
}
.danger {
  background-color: rgb(235, 31, 31);
  margin-bottom: 6px;
}
span {
  font-size: 20px;
}
.cnt {
  display: flex;
  justify-content: space-around;
  align-self: center;
}
</style>
