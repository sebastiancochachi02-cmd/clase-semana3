<script setup>
import {ref} from "vue";

const firstName = ref('');
const lastName = ref('');
const errorMessage = ref('')

const emit = defineEmits(['developer-registered', 'registration-defered']);

function clearFields() {
  firstName.value = '';
  lastName.value = '';
  errorMessage.value = '';
}

function submitRegistrationRequest() {
  let submittedFirstName = firstName.value.toString().trim();
  let submittedLastName = lastName.value.toString().trim();
  if (submittedFirstName||submittedLastName) {
    console.log('Registering developer');
    emit ('developer-registered',{
    firstName: submittedFirstName,
        lastName: submittedLastName});
    clearFields();
    errorMessage.value = '';
  }else {
    console.log('Cannot register: both fields are required');
    errorMessage.value = 'Please provide at least firts name or last name.';
  }
}

function  deferRegistration(){
  console.log('Deferred registered');
  emit('developer-registered',{firstName: '', lastName: ''})
  clearFields();
  errorMessage.value = '';
}

</script>

<template>
<div>
  <h2>New Developer</h2>
  <div>
    <form v-on:submit.prevent="submitRegistrationRequest">
      <div class="field">
        <label for="first-name">First Name:</label><input id="first-name" v-model="firstName" type="text"/>
        <div class="field">
          <label for="last-name">Last Name:</label><input id="last-name" v-model="lastName" type="text"/>
    </form>
  </div>
</div>
</template>

<style scoped>
button{
  margin: 10px;
  padding: 8px 16px;
  cursor: pointer;
}
.error{
  color: #d32f2f;
  margin-top: 10px;
  font-size: 14px;
}
.field {
  margin-bottom: 10px;
}
.actions{
  margin-top: 10px;
}
label{
  margin-right: 5px;
}
</style>