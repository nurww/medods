<template>
  <form @submit.prevent="submit">
    <div class="form__attributes">
      <h2>Атрибуты формы</h2>
      <div class="form-group" :class="{ 'form-group--error': $v.name.$error }">
        <label for="name">Имя*</label>
        <div class="form-group__input-wrapper">
          <input id="name" v-model="name" />
          <small class="error" v-if="!$v.name.required">Введите имя</small>
        </div>
      </div>

      <div class="form-group" :class="{ 'form-group--error': $v.surname.$error }">
        <label for="surname">Фамилия*</label>
        <div class="form-group__input-wrapper">
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
        <div class="form-group__input-wrapper">
          <input id="birth-date" type="number" v-model="birthDate" placeholder="ДД.ММ.ГГГГ" />
          <small class="error" v-if="!$v.birthDate.required">Введите дату рождения</small>
        </div>
      </div>

      <div class="form-group" :class="{ 'form-group--error': $v.phoneNumber.$error }">
        <label for="phone-number">Номер телефона*</label>
        <div class="form-group__input-wrapper">
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
        <div class="form-group__input-wrapper">
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
        <div class="form-group__input-wrapper">
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
        <div class="form-group__input-wrapper">
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
        <div class="form-group__input-wrapper">
          <input id="issued-date" type="number" v-model="issuedDate" placeholder="ДД.ММ.ГГГГ" />
          <small class="error" v-if="!$v.issuedDate.required">Введите дату выдачи</small>
        </div>
      </div>

      <div class="success-block" v-bind:style="{ opacity: opacity, visibility: visibility }">
        <h2>Клиент успешно создан</h2>
      </div>
    </div>

    <button id="submit" type="submit">Submit</button>
  </form>
</template>

<script>
import { required, minLength, maxLength } from "vuelidate/lib/validators";
export default {
  data: () => ({
    // v-model для класса .form__attributes
    name: "",
    surname: "",
    birthDate: "",
    phoneNumber: "",
    sex: "",
    clientType: [],
    attendingDoctor: "",
    sms: false,
    // v-model для класса .form__address
    cityIndex: "",
    country: "",
    region: "",
    city: "",
    street: "",
    house: "",
    // v-model для класса .form__documents
    documentType: "",
    docSerial: "",
    docNumber: "",
    issuedBy: "",
    issuedDate: "",
    // v-model стили для .success-block
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
          // делаем .success-block видимым
          this.visibility = "unset";
          this.opacity = 1;
          setTimeout(() => {
            // устанавливаем 2 секунды для скрытия .success-block при помощи свойства transiton css
            this.opacity = 0;
          }, 2000);
          setTimeout(() => {
            // окончательно скрываем .success-block
            this.visibility = "hidden";
          }, 4000);
        }, 500);
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="sass">
$form-BGcolor: rgba(205, 225, 247, 1)

form
  background-color: $form-BGcolor
  border-radius: 25px
  box-sizing: border-box
  margin: 0 auto
  max-width: 500px
  padding: 15px 30px
  @media screen and (max-width: 500px)
    max-width: 300px

.form-group
  display: flex
  margin: 30px 0
  justify-content: space-between
  position: relative
  max-width: 500px;

  small
    bottom: -15px
    font-size: 10px
    position: absolute
    visibility: hidden

  &--error input,
  &--error select
    border-color: red

  &--error small
    visibility: unset
  
  @media screen and (max-width: 500px)
    flex-direction: column
    align-items: center

.form-group__input-wrapper
  display: flex
  flex-direction: column

label
  display: block
  @media screen and (max-width: 500px)
    align-self: baseline

input
  background: white
  border: 1px solid silver
  border-radius: 4px
  padding: 5px 10px
  &:not([type="checkbox"])
    box-sizing: border-box
    width: 200px
  &:focus
    outline: none
  &::-webkit-outer-spin-button,
  &::-webkit-inner-spin-button
    margin: 0
    -webkit-appearance: none
  &[type="number"]
    -moz-appearance: textfield

select
  box-sizing: border-box
  width: 200px
  outline: none
  background: white
  border: 1px solid silver
  border-radius: 4px
  padding: 5px 10px

.error
  color: red
  &:focus
    outline-color: #f99

.success-block
  background-color: rgba(255, 250, 208, 1)
  border-radius: 15px
  left: 50%
  position: fixed
  text-align: center
  transform: translateX(-50%)
  transition: opacity 1s
  top: 5%
  -webkit-user-select: none
  -moz-user-select: none
  -ms-user-select: none
  user-select: none
  width: 50%

#submit
  background-color: #fff
  border: none
  border-radius: 15px
  display: block
  font-size: 20px
  margin: 0 auto
  outline: none
  padding: 15px 20px
  &:active
    background-color: rgba(253, 115, 154, 1)
  @media screen and (max-width: 500px)
    margin: 0

.success-block h2
  @media screen and (max-width: 500px)
    font-size: 15px
    padding: 0 10px
    box-sizing: border-box
</style>