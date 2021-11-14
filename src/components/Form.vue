<template>
  <FormulateForm v-model="formData" class="form">
    <h2>Личные данные</h2>
    <div class="double-wide">
      <FormulateInput
        type="text"
        name="surname"
        label="Фамилия"
        validation="required"
      />

      <FormulateInput
        type="text"
        name="name"
        label="Имя"
        validation="required"
      />

      <FormulateInput
        type="text"
        name="patronymic"
        label="Отчество"
        validation="required"
      />
    </div>

    <FormulateInput
      type="date"
      name="birthDate"
      label="Дата рождения"
      validation="required"
    />
    <div class="wide">
      <FormulateInput
        type="email"
        name="email"
        label="E-mail"
        validation="required"
      />
    </div>

    <FormulateInput
      type="radio"
      name="gender"
      label="Пол"
      validation="required"
      :options="{ male: 'Мужской', female: 'Женский' }"
    />

    <h2>Паспортные данные</h2>

    <FormulateInput
      type="select"
      label="Гражданство"
      name="citizen"
      :options="selectSitizenshipValues"
    />

    <div
      v-if="formData.citizen == '0e10e8fe-cb2f-42d0-b86a-e38cb4e01f40'"
      class="double-wide"
    >
      <FormulateInput
        type="number"
        name="pasportSeries"
        label="Серия паспорта"
        validation="required"
      />
      <FormulateInput
        type="number"
        name="pasportNumber"
        label="Номер паспорта"
        validation="required"
      />
      <FormulateInput
        type="date"
        name="pasportDate"
        label="Дата выдачи"
        validation="required"
      />
    </div>
    <div v-else>
      <div class="double-wide">
        <FormulateInput
          type="text"
          name="latinSurname"
          label="Фамилия на латинице"
          validation="required"
        />
        <FormulateInput
          type="text"
          name="latinName"
          label="Имя на латинице"
          validation="required"
        />
      </div>
      <div class="double-wide">
        <FormulateInput
          type="number"
          name="pasportNumber"
          label="Номер паспорта"
          validation="required"
        />
        <FormulateInput
          type="select"
          name="pasportCountry"
          label="Страна выдачи"
          validation="required"
          :options="selectSitizenshipValues"
        />
        <FormulateInput
          type="select"
          name="pasportType"
          label="Тип паспорта"
          validation="required"
          :options="selectPassportType"
        />
      </div>
    </div>
    <FormulateInput
      type="radio"
      name="isNameChanged"
      label="Меняли ли фамилию или имя?"
      validation="required"
      :options="{ yes: 'Да', no: 'Нет' }"
    />

    <div v-if="formData.isNameChanged == 'yes'" class="double-wide">
      <FormulateInput
        type="text"
        name="oldSurname"
        label="Фамилия"
        validation="required"
      />

      <FormulateInput
        type="text"
        name="oldName"
        label="Имя"
        validation="required"
      />
    </div>

    <FormulateInput type="button" label="Отправить" @click="submitForm" />
  </FormulateForm>
</template>

<script>
import ClickOutside from "vue-click-outside";
import citizenships from "../assets/data/citizenships.json";
import pasportTypes from "../assets/data/passport-types.json";

export default {
  directives: {
    ClickOutside,
  },
  mounted() {
    citizenships.forEach((item) => {
      this.selectSitizenshipValues[item.uid] = item.nationality;
    });
    pasportTypes.forEach((item) => {
      this.selectPassportType[item.id] = item.type;
    });
  },
  data() {
    return {
      formData: {
        email: "",
        birthDate: "",
        name: "",
        surname: "",
        patronymic: "",
        citizen: "0e10e8fe-cb2f-42d0-b86a-e38cb4e01f40",
        gender: "male",
        pasportSeries: "",
        pasportNumber: "",
        pasportDate: "",
        latinSurname: "",
        latinName: "",
        pasportCountry: "",
        pasportType: "",
        oldSurname: "",
        oldName: "",
        isNameChanged: false,
      },
      isDropdownOpen: false,
      citizenships: citizenships,
      selectSitizenshipValues: {},
      selectPassportType: {},
    };
  },
  methods: {
    hideDropdown() {
      this.isDropdownOpen = false;
    },
    onSitizenshipSelect(selected) {
      this.formData.sitizen = selected;
      this.hideDropdown();
    },
    submitForm() {
      console.log(this.formData);
    },
  },
};
</script>

<style scoped>
h2 {
  padding-bottom: 15px;
}
.form {
  max-width: 600px;
  margin: 0 auto;
  overflow: auto;
  padding: 40px;
  align-content: center;
  border: 1px solid #91b7dd9d;
  /* padding: 20px; */
  border-radius: 6px;
}
input {
  display: block;
  overflow: visible;
  border: solid 0.5px #91b7dd9d;
  border-radius: 5px;
  padding: 10px;
  margin-top: 10px;
  margin-bottom: 10px;
}
@media (min-width: 420px) {
  .double-wide {
    display: flex;
  }
  .double-wide .formulate-input {
    flex-grow: 1;
    width: calc(50% - 0.5em);
  }
  .double-wide .formulate-input:first-child {
    margin-right: 0.5em;
  }
  .double-wide .formulate-input:last-child {
    margin-left: 0.5em;
  }
}
</style>
