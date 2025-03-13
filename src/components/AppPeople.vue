<template>
  <div class="cont" v-if="people.length > 0">
    <div class="inf" v-for="pipl in people">
      <span>{{ pipl.id }}:&nbsp;</span>
      <span
        ><strong>{{ pipl.firstname }}</strong></span
      >
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
  emits: ['load'],
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
</style>
