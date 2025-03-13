<template>
  <div class="alert">
    <div class="danger"></div>
    <div class="content">
      <h2>Ошибка</h2>
      <p>message</p>
      <button>Закрыть</button>
    </div>
  </div>
</template>
<script>
export default {}
</script>
<style>
.alert {
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.4);
  background-color: white;
  width: 60%;
  border-radius: 10px;
  height: auto;
  padding: 10px;
}
.danger {
  background-color: rgb(242, 59, 59);
  width: 10px;
  height: 100%;
}
</style>
