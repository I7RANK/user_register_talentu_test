<template>
  <div class="user-form flex flex-col items-center px-8">
    <Alert v-if="showAlert" :msg="msgAlert" />
    <h2 class="text-3xl text-center my-5">Agregar nuevo usuario</h2>

    <div class="flex flex-col my-2">
      <label for="email">Email*</label>
      <input id="email" type="email" ref="inEmail" @keydown="(e) => {
        changeBorderColor(e.target, 'var(--input-color)')
      }"/>
    </div>

    <div class="flex flex-col my-2">
      <label for="first-name">Nombre(s)*</label>
      <input id="first-name" type="text" ref="inFirstName" @keydown="(e) => {
        changeBorderColor(e.target, 'var(--input-color)')
      }"/>
    </div>

    <div class="flex flex-col my-2">
      <label for="last-name">Apellido(s)*</label>
      <input id="last-name" type="text" ref="inLastName" @keydown="(e) => {
        changeBorderColor(e.target, 'var(--input-color)')
      }"/>
    </div>

    <div class="flex flex-col my-2">
      <label for="birth-date">Fecha nacimiento*</label>
      <input id="birth-date" type="date" ref="inBirthDate" @click="(e) => {
        changeBorderColor(e.target, 'var(--input-color)')
      }"/>
    </div>

    <div>
      <button @click="this.createUpdateUser()"
        class=" my-5 py-3 flex-grow rounded-full hover:opacity-95
        active:opacity-90">
        Agregar usuario
      </button>
    </div>
  </div>
</template>

<script>
import Alert from './Alert.vue';

const EMAIL_REGEX = /[a-z0-9!#$%&'*+/=?^_`{|}~-]+(?:\.[a-z0-9!#$%&'*+/=?^_`{|}~-]+)*@(?:[a-z0-9](?:[a-z0-9-]*[a-z0-9])?\.)+[a-z0-9](?:[a-z0-9-]*[a-z0-9])?/;
const ALERT_TIME = 3400;

let timeControl;

export default {
  data() {
    return {
      showAlert: false,
      msgAlert: '',
    };
  },
  components: {
    Alert,
  },
  methods: {
    createUpdateUser() {
      const userList = JSON.parse(localStorage.getItem('userList'));
      const newUser = this.checkInput();

      if (!newUser) return;

      userList.push(newUser);

      localStorage.setItem('userList', JSON.stringify(userList));
      this.$emit('userListUpdated');
      this.clearAllInputs();
      this.showFormAlert('Usuario agregado!!');
    },
    checkInput() {
      const emailChecked = this.$refs.inEmail.value.match(EMAIL_REGEX);
      const emptyMsg = 'No se permiten campos vacios';

      if (this.$refs.inEmail.value === '') {
        this.showFormAlert(emptyMsg);
        this.changeBorderColor(this.$refs.inEmail);
        return;
      }

      if (!emailChecked || emailChecked.input !== emailChecked[0]) {
        this.showFormAlert('Tipo de email invalido');
        this.changeBorderColor(this.$refs.inEmail);
        return;
      }

      const firstNameValue = this.$refs.inFirstName.value;
      if (firstNameValue === '') {
        this.showFormAlert(emptyMsg);
        this.changeBorderColor(this.$refs.inFirstName);
        return;
      }

      const lastNameValue = this.$refs.inLastName.value;
      if (lastNameValue === '') {
        this.showFormAlert(emptyMsg);
        this.changeBorderColor(this.$refs.inLastName);
        return;
      }

      const birthDateValue = this.$refs.inBirthDate.value;
      if (birthDateValue === '') {
        this.showFormAlert(emptyMsg);
        this.changeBorderColor(this.$refs.inBirthDate);
        return;
      }
      if (Date.now() < Date.parse(birthDateValue)) {
        this.showFormAlert('No puedes nacer en el futuro');
        this.changeBorderColor(this.$refs.inBirthDate);
        return;
      }

      return {
        id: Date.now(),
        email: emailChecked.input,
        first_name: firstNameValue,
        last_name: lastNameValue,
        birth_date: birthDateValue,
        avatar: 'https://www.kindpng.com/picc/m/24-248253_user-profile-default-image-png-clipart-png-download.png',
      };
    },
    showFormAlert(msg='Hola!') {
      this.msgAlert = msg;
      this.showAlert = true;
      clearInterval(timeControl);
      timeControl = setTimeout(() => {
        this.showAlert = false;
      }, ALERT_TIME);
    },
    changeBorderColor(inputElement, color='#f00') {
      inputElement.style.borderColor = color;
      inputElement.focus();
    },
    clearAllInputs() {
      this.$refs.inEmail.value = '';
      this.$refs.inFirstName.value = '';
      this.$refs.inLastName.value = '';
      this.$refs.inBirthDate.value = '';
    }
  },
};
</script>

<style>
.user-form label {
  font-size: 0.8rem;
  padding: 0 1rem;
}

.user-form input {
  max-width: 212px;
  padding: 0 1rem;
  font-size: 1.2rem;
  outline: none;
  border-radius: 9999px;
  border: var(--input-color) 2px solid;
  transition: border 0.3s;
}

.user-form input:focus {
  border: var(--input-color-2) 2px solid;
}

.user-form button {
  background: var(--bg-talentu);
  min-width: 212px;
  color: var(--background-secondary);
}
</style>