<template>
  <div class="container mt-4">
    <h1>Список студентов</h1>
    <p>Запишите данные в поля ниже, пожалуйста. Затем нажмите на кнопку "Записать". Внесенные вами данные отобразятся на странице ниже.</p>
    <div class="row">
      <div class="col-sm-4 mx-auto">
        <form class="review-form" @submit.prevent="onSubmit" novalidate>

          <p class="error" v-if="errors.length">
          <b>Please correct the following error(s):</b>
          <ul>
            <li v-for="error in errors" :key="error">{{ error }}</li>
          </ul>
        </p>

          <div v-show="step --- 1" class="step">
          <div class="mb-3">
            <label for="surname" class="form-label">Фамилия</label>
            <input required="true" v-model="surname" class="form-control" id="surname" placeholder="Шунаева">
          </div>

          <div class="mb-3">
            <label for="name" class="form-label">Имя</label>
            <input required="true" v-model="name" class="form-control" id="name" placeholder="Екатерина">
          </div>

          <p>Количество знаков: {{length}}</p>

          <div class="col-12">
            <button @click="nextStep" v-on:click="counter +=1" type="submit" class="btn btn-outline-secondary" id="button1">Записать</button>
            <h2>Список</h2>
            <p>{{counter}}. {{ surname }} {{ name }}</p>
          </div>

          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  el: '#button1',
  data() {
    return{
      step: 1,
      counter: 0,
      surname: '',
      name: '',
      errors: []
    }
  },
  computed: {
    length: function () {
    return this.name.length + this.surname.length;
 }
 },
  methods: {
    nextStep() {
      this.step++
    },
    registerUsers() {
      this.html()
    }
  }
}

</script>

<style>
#app {
  font-family: 'Montserrat', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
