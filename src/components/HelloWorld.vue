<template>
  <form @submit.prevent="submit">
    <div class="form__attributes">
      <h2>Атрибуты формы</h2>
      <div class="form-group" :class="{ 'form-group--error': $v.name.$error }">
        <label for="name">Имя*</label>
        <div class="flex">
          <input id="name" v-model="name" />
          <small class="error" v-if="!$v.name.required">Введите имя</small>
        </div>
      </div>

      <div class="form-group" :class="{ 'form-group--error': $v.surname.$error }">
        <label for="surname">Фамилия*</label>
        <div class="flex">
          <input id="surname" v-model="surname" />
          <small class="error" v-if="!$v.surname.required">Введите фамилию</small>
        </div>
      </div>

      <div class="form-group">
        <label for="fathers-name">Отчество</label>
        <input id="fathers-name" />
      </div>

      <div class="form-group" :class="{ 'form-group--error': $v.birthDate.$error }">
        <label for="birth-date">Дата рождения*</label>
        <div class="flex">
          <input id="birth-date" type="number" v-model="birthDate" placeholder="ДД.ММ.ГГГГ" />
          <small class="error" v-if="!$v.birthDate.required">Введите дату рождения</small>
        </div>
      </div>

      <div class="form-group" :class="{ 'form-group--error': $v.phoneNumber.$error }">
        <label for="phone-number">Номер телефона*</label>
        <div class="flex">
          <input id="phone-number" type="number" v-model="phoneNumber" placeholder="7 XXX XXX XXXX" />
          <small
            class="error"
            v-if="!$v.phoneNumber.minLength"
          >Введите не менее {{$v.phoneNumber.$params.minLength.min}} символов.</small>
          <small
            class="error"
            v-if="!$v.phoneNumber.maxLength"
          >Введите не более {{$v.phoneNumber.$params.maxLength.max}} символов.</small>
          <small class="error" v-if="!$v.phoneNumber.required">Введите номер телефона</small>
        </div>
      </div>

      <div class="form-group">
        <label for="sex">Пол</label>
        <select id="sex" v-model="sex">
          <option>Женский</option>
          <option>Мужской</option>
        </select>
      </div>

      <div class="form-group" :class="{ 'form-group--error': $v.clientType.$error }">
        <label for="client-type">Группа клиентов*.</label>
        <div class="flex">
          <select id="client-type" v-model="clientType" multiple>
            <option>VIP</option>
            <option>Проблемные</option>
            <option>ОМС</option>
          </select>
          <small class="error" v-if="!$v.clientType.required">Выберите группу клиентов</small>
        </div>
      </div>

      <div class="form-group">
        <label for="attending-doctor">Лечащий врач.</label>
        <select id="attending-doctor" v-model="attendingDoctor">
          <option disabled value>Выберите один</option>
          <option>Иванов</option>
          <option>Захаров</option>
          <option>Чернышева</option>
        </select>
      </div>

      <div class="form-group">
        <label for="sms">Не отправлять СМС.</label>
        <input id="sms" type="checkbox" v-model="sms" true-value="yes" false-value="no" />
      </div>
    </div>

    <div class="form__address">
      <h2>Адрес</h2>
      <div class="form-group">
        <label for="cityIndex">Индекс</label>
        <input id="cityIndex" v-model="cityIndex" />
      </div>

      <div class="form-group">
        <label for="country">Страна</label>
        <input id="country" v-model="country" />
      </div>

      <div class="form-group">
        <label for="region">Область</label>
        <input id="region" v-model="region" />
      </div>

      <div class="form-group" :class="{ 'form-group--error': $v.city.$error }">
        <label for="city">Город*</label>
        <div class="flex">
          <input id="city" v-model="city" />
          <small class="error" v-if="!$v.city.required">Введите город</small>
        </div>
      </div>

      <div class="form-group">
        <label for="street">Улица</label>
        <input id="street" v-model="street" />
      </div>

      <div class="form-group">
        <label for="house">Дом</label>
        <input id="house" v-model="house" />
      </div>
    </div>

    <div class="form__documents">
      <h2>Паспорт</h2>

      <div class="form-group" :class="{ 'form-group--error': $v.documentType.$error }">
        <label for="document-type">Тип документа*.</label>
        <div class="flex">
          <select id="document-type" v-model="documentType">
            <option disabled value>Выберите один</option>
            <option>Паспорт</option>
            <option>Свидетельство о рождении</option>
            <option>Вод. удостоверение</option>
          </select>
          <small class="error" v-if="!$v.documentType.required">Выберите тип документа</small>
        </div>
      </div>

      <div class="form-group">
        <label for="doc-serial">Серия</label>
        <input id="doc-serial" v-model="docSerial" />
      </div>

      <div class="form-group">
        <label for="doc-number">Номер</label>
        <input id="doc-number" v-model="docNumber" />
      </div>

      <div class="form-group">
        <label for="issued-by">Кем выдан</label>
        <input id="issued-by" v-model="issuedBy" />
      </div>

      <div class="form-group" :class="{ 'form-group--error': $v.issuedDate.$error }">
        <label for="issued-date">Дата выдачи*</label>
        <div class="flex">
          <input id="issued-date" type="number" v-model="issuedDate" placeholder="ДД.ММ.ГГГГ" />
          <small class="error" v-if="!$v.issuedDate.required">Введите дату выдачи</small>
        </div>
      </div>

      <div class="success-block" v-bind:style="{ opacity: opacity, visibility: visibility }">
        <h2>Клиент успешно создан</h2>
      </div>
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
    birthDate: "",
    phoneNumber: "",
    sex: "",
    clientType: [],
    attendingDoctor: "",
    sms: false,
    cityIndex: "",
    country: "",
    region: "",
    city: "",
    street: "",
    house: "",
    documentType: "",
    docSerial: "",
    docNumber: "",
    issuedBy: "",
    issuedDate: "",
    opacity: 0,
    visibility: "hidden",
  }),
  validations: {
    name: {
      required,
    },
    surname: {
      required,
    },
    birthDate: {
      required,
    },
    phoneNumber: {
      required,
      minLength: minLength(11),
      maxLength: maxLength(11),
    },
    clientType: {
      required,
    },
    city: {
      required,
    },
    documentType: {
      required,
    },
    issuedDate: {
      required,
    },
  },
  methods: {
    submit() {
      this.$v.$touch();
      if (this.$v.$invalid) {
        this.submitStatus = "ERROR";
      } else {
        this.submitStatus = "PENDING";
        setTimeout(() => {
          this.submitStatus = "OK";
          this.visibility = "unset";
          this.opacity = 1;
          setTimeout(() => {
            this.opacity = 0;
          }, 2000);
          setTimeout(() => {
            this.visibility = "hidden";
          }, 4000);
        }, 500);
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
  margin: 30px 10px;
  display: flex;
  position: relative;
}

small {
  font-size: 10px;
  /* left: 440px; */
  bottom: -15px;
  position: absolute;
  visibility: hidden;
}

.flex {
  display: flex;
  flex-direction: column;
}

input:focus,
select {
  outline: none;
}

.form-group--error input,
.form-group--error select {
  border-color: red;
}

.form-group--error small {
  visibility: unset;
}

label {
  display: inline-block;
  width: 150px;
  margin: 0 50px 0 0;
}

input:not([type="checkbox"]),
select {
  width: 200px;
  box-sizing: border-box;
}

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* Firefox */
input[type="number"] {
  -moz-appearance: textfield;
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

.success-block {
  width: 500px;
  height: 70px;
  border-radius: 15px;
  background-color: rgba(7, 250, 32, 0.85);
  position: fixed;
  top: 5%;
  left: 50%;
  transform: translateX(-250px);
  -webkit-user-select: none; /* Chrome all / Safari all */
  -moz-user-select: none; /* Firefox all */
  -ms-user-select: none; /* IE 10+ */
  user-select: none; /* Likely future */
  transition: opacity 1s;
}
</style>
