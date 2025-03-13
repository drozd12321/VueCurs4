<script>
import AppAlert from './components/AppAlert.vue'
import AppLoader from './components/AppLoader.vue'
import AppPeople from './components/AppPeople.vue'
import axios from 'axios'
export default {
  data() {
    return {
      name: '',
      people: [],
      err: {
        type: '',
        title: '',
        text: '',
      },
      loader: false,
    }
  },
  components: {
    AppPeople,
    AppAlert,
    AppLoader,
  },
  mounted() {
    this.loadData()
    console.log(this.err)
  },
  methods: {
    async personSubmit() {
      const resp = await fetch(
        'https://vuehttp-6614a-default-rtdb.europe-west1.firebasedatabase.app/people.json',
        {
          method: 'POST',
          headers: {
            'Content-type': 'application/json',
          },
          body: JSON.stringify({
            firstName: this.name,
          }),
        },
      )
      const fireBase = await resp.json()
      this.people.push({
        firstname: this.name,
        id: fireBase.name,
      })
      this.name = ''
    },
    async loadData() {
      try {
        this.loader = true
        const { data } = await axios.get(
          'https://vuehttp-6614a-default-rtdb.europe-west1.firebasedatabase.app/people.json',
        )
        if (!data) {
          throw new Error('Список людей пуст, добавьте пользователей ниже')
        }
        const pipl = Object.keys(data).map((item) => {
          return {
            id: item,
            firstname: data[item].firstName,
          }
        })
        this.people = pipl
        this.loader = false
        this.err = null
      } catch (error) {
        this.loader = false
        this.err = {
          type: 'danger',
          title: 'Ошибка',
          text: error.message,
        }
      }
    },
    async deleteData(i) {
      try {
        const pers = this.people.find((item) => item.id === i).firstname
        const data = await axios.delete(
          `https://vuehttp-6614a-default-rtdb.europe-west1.firebasedatabase.app/people/${i}.json`,
        )
        this.people = this.people.filter((item) => item.id !== i)
        if (this.err === null) {
          this.err = {
            title: '',
            type: '',
            text: '',
          }
        }
        this.err.title = 'Успешно'
        this.err.type = 'primary'
        this.err.text = `Вы успешно удалили пользователя "${pers}"`
      } catch (error) {
        this.err.type = 'danger'
        this.err.title = 'Ошибка'
        this.err.text = error.message
      }
    },
    closeAlert() {
      this.err = null
    },
  },
}
</script>

<template>
  <div class="form" @submit.prevent="personSubmit">
    <AppAlert v-if="err != null" :error="err" @closeAl="closeAlert"></AppAlert>
    <form class="fr">
      <h1>Работа с БД</h1>
      <div class="inp">
        <label for="name">Имя:</label>
        <input type="text" id="name" v-model.trim="name" />
      </div>
      <div class="inp">
        <button class="btn" :disabled="name.length === 0">Отправить</button>
      </div>
    </form>
    <AppLoader v-if="loader"></AppLoader>
    <AppPeople v-else :people="people" @load="loadData" @delete="deleteData"></AppPeople>
  </div>
</template>

<style scoped>
.inp {
  display: flex;
  justify-content: center;
  align-items: center;
}
.form {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}
.fr {
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.4);
  background-color: white;
  width: 60%;
  border-radius: 10px;
  height: auto;
  padding: 10px;
}
.fr h1 {
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
}
input {
  outline: none;
  border-radius: 6px;
  margin-left: 4px;
  background-color: rgb(92, 89, 89);
  border: none;
  color: white;
  font-size: 15px;
  padding: 5px;
}
button:disabled {
  background-color: rgb(92, 89, 89);
}
</style>
