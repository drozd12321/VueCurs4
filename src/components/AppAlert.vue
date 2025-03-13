<template>
  <div class="alert" v-if="error">
    <div :class="{ danger: error.type === 'danger', primary: error.type === 'primary' }"></div>
    <div class="content">
      <div class="cnt1">
        <h2>{{ error.title }}</h2>
        <p>{{ error.text }}</p>
        <button class="btn" @click="closeAl">Закрыть</button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  emits: ['closeAl'],
  props: {
    error: Object,
  },
  methods: {
    closeAl() {
      this.$emit('closeAl')
    },
  },
}
</script>
<style scoped>
.alert {
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.4);
  background-color: white;
  width: 60%;
  border-radius: 10px;
  height: auto;
  display: flex;
}
.primary {
  background-color: rgb(7, 232, 37);
  flex: 0.01;
  height: auto;
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
}
.danger {
  background-color: rgb(242, 59, 59);
  flex: 0.01;
  height: auto;
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
}
.content {
  flex: 0.9;
  display: flex;
  height: 100%;
  text-align: center;
  justify-content: center;
  align-items: center;
}
.cnt1 {
  text-align: center;
}
.btn {
  background-color: black;
  color: white;
  padding: 6px;
  margin-top: 7px;
  border-radius: 6px;
  font-size: 20px;
  border: none;
  margin-bottom: 5px;
}
</style>
