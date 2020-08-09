<template>
  <form @submit.prevent="submit">
    <div class="form__attributes">
      <h2>Атрибуты формы</h2>
      <div class="form-group" :class="{ 'form-group--error': $v.name.$error }">
        <label class="form__label" for="name">Имя*</label>
        <input class="form__input" v-model="name" id="name" />
        <small class="error" v-if="!$v.name.required && $v.name.$dirty">Введите имя</small>
      </div>

      <div class="form-group" :class="{ 'form-group--error': $v.surname.$error }">
        <label for="surname">Фамилия*</label>
        <input v-model="surname" id="surname" />
        <small class="error" v-if="!$v.surname.required && $v.surname.$dirty">Введите фамилию</small>
      </div>

      <div class="form-group">
        <label class="form__label" for="fathers-name">Отчество</label>
        <input class="form__input" id="fathers-name" />
      </div>

      <div class="form-group" :class="{ 'form-group--error': $v.birthDay.$error }">
        <label for="birth-day">День рождения*</label>
        <select class="number-input" id="birth-day" v-model="birthDay">
          <option v-for="index in 31" :key="index">{{ index }}</option>
        </select>
        <small class="error" v-if="!$v.birthDay.required && $v.birthDay.$dirty">Выберите день</small>
      </div>

      <div class="form-group" :class="{ 'form-group--error': $v.birthMonth.$error }">
        <label for="birth-month">Месяц рождения*</label>
        <select class="number-input" id="birth-month" v-model="birthMonth">
          <option>Январь</option>
          <option>Февраль</option>
          <option>Март</option>
          <option>Апрель</option>
          <option>Май</option>
          <option>Июнь</option>
          <option>Июль</option>
          <option>Август</option>
          <option>Сентябрь</option>
          <option>Октябрь</option>
          <option>Ноябрь</option>
          <option>Декабрь</option>
        </select>
        <small class="error" v-if="!$v.birthMonth.required && $v.birthMonth.$dirty">Выберите месяц</small>
      </div>

      <div class="form-group">
        <label for="birth-year">Год рождения*</label>
        <input class="number-input" id="birth-month" type="number" value="2020" disabled />
      </div>

      <div class="form-group" :class="{ 'form-group--error': $v.birthMonth.$error }">
        <label for="phone-number">Номер телефона*</label>
        <input v-model="phoneNumber" id="phone-number" />
        <small
          class="error"
          v-if="!$v.phoneNumber.minValue"
        >Phone must have at least {{$v.phoneNumber.$params.minValue.min}} numbers.</small>
      </div>

      <div class="form-group">
        <label for="sex">Пол</label>
        <input v-model="sex" id="sex" />
      </div>

      <!-- <div class="form-group">
        <label for="client-type">Группа клиентов*.</label>
        <select id="client-type" v-model="selected" multiple>
          <option>VIP</option>
          <option>Проблемные</option>
          <option>ОМС</option>
        </select>
      </div>

      <div class="form-group">
        <label for="attending-doctor">Лечащий врач.</label>
        <select id="attending-doctor" v-model="selected">
          <option disabled value>Please select one</option>
          <option>Иванов</option>
          <option>Захаров</option>
          <option>Чернышева</option>
        </select>
      </div>

      <div class="form-group">
        <label for="sms">Не отправлять СМС.</label>
        <input id="sms" type="checkbox" v-model="toggle" true-value="yes" false-value="no" />
      </div> -->
    </div>
    <button type="submit">Submit</button>
  </form>
</template>

<script>
import { required, minLength, maxLength } from "vuelidate/lib/validators";
export default {
  data: () => ({
    name: "",
    surname: "",
    birthDay: "",
    birthMonth: "",
    phoneNumber: "",
    sex: ""
  }),
  validations: {
    name: {
      required,
    },
    surname: {
      required,
    },
    birthDay: {
      required,
    },
    birthMonth: {
      required,
    },
    phoneNumber: {
      required,
      minLength: minLength(11),
      maxLength: maxLength(11)
    },
  },
  methods: {
    submit() {
      this.$v.$touch();
      if (this.$v.$invalid) {
        this.submitStatus = "ERROR";
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
body {
  background-color: #ede8f6;
}

form {
  background-color: #fff;
  border-radius: 5px;
  /* width: 500px; */
  padding: 15px 10px;
}

.form-group {
  word-break: break-all;
  margin: 10px;
}

input:focus,
select {
  outline: none;
}

.form-group--error input,
.form-group--error select {
  border-color: red;
}

label {
  display: inline-block;
  width: 150px;
  margin: 0 50px 0 0;
}

input:not([type="checkbox"]),
select {
  width: 200px;
}

.number-input {
  /* width: 50px !important; */
}

.validate {
  border-color: #ef9a9a;
  display: inline-block;
  padding: 10px 20px;
  border-radius: 10px;
  position: absolute;
  top: 20px;
  right: 20px;
  background-color: transparent;
  transition: background-color 2s;
}

.validate-message {
  font-size: 20px;
  color: #fff;
}

input,
select {
  border: 1px solid silver;
  border-radius: 4px;
  background: white;
  padding: 5px 10px;
}

.dirty {
  border-color: #5a5;
  background: #efe;
}

.dirty:focus {
  outline-color: #8e8;
}

.error {
  color: red;
}

.error:focus {
  outline-color: #f99;
}
</style>
