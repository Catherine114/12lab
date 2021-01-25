<template>
  <div class="container mt-4">
    <h1>Список студентов</h1>
    <p>Запишите данные в поля ниже, пожалуйста. Затем нажмите на кнопку "Записать". Внесенные вами данные отобразятся на странице ниже.</p>
    <div class="row">
      <div class="col-sm-4 mx-auto">
        <form class="review-form" novalidate>

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
            <button v-on:click="counter +=1" v-on:click.prevent="addItem" v-bind:disabled="Button" type="submit" class="btn btn-outline-secondary" id="button1">Записать</button>
            <h2>Список</h2>
            <p v-if="!surname.length + !name.length">Список пуст</p>
            <div v-else>
              <p>{{counter}}. {{ surname }} {{ name }}</p>
              <ol>
                <li v-for="item in items" :key="item">{{item}}</li>
              </ol><br>
            </div>
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
      errors: [],
      items: [],
      Button: true
    }
  },
  computed: {
    length: function () {
    return this.name.length + this.surname.length;
 }
 },
  methods: {
    addItem(e) {
      this.errors = []
      if (this.surname !== '' && this.name !== '') {
        let item = {
          name: this.name,
          surname: this.surname
        };
        this.$emit('add-Item', item)
        this.name = null
        this.surname = null

        } else {
          e.preventDefault()
          }
        
        this.items.push(`${this.surname} ${this.name} `);
        this.surname = '';
        this.name = '';
      
    }
  },
  watch: {
    surname(value) {
                        if (value.length > 0 && this.name.length > 0) {
                            this.Button = false;
                        } else {
                            this.Button = true;
                        }
                    },
    name(value) {
                        if (value.length > 0 && this.surname.length > 0) {
                            this.Button = false;
                        } else {
                            this.Button = true;
                        }
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
