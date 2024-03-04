<script setup>
import PasswordInput from "@/components/PasswordInput.vue";
import {onMounted, ref} from "vue";

const input = ref(null);
onMounted(() => {
  input.value.focus();
})

function validateForm(event)  {
  const form = document.getElementById('signupForm');
  if ( !checkPasswordValidity() && !form.checkValidity()) {
    event.preventDefault();
    event.stopPropagation();
  }
  form.classList.add('was-validated');
}

function checkPasswordValidity() {
  const password = document.getElementById("password");
  const minPassword = /^(?=.*[a-z])(?=.*\d)[a-z\d]{6,}$/i

  if (!minPassword.test(password.value)) {
    password.setCustomValidity("password wrong");
    return false;
  } else {
    return true;
  }
}
</script>

<template>
  <div class="bd-example m-0 border-0">
  <fieldset>
    <legend>Signup form</legend>
    <form id="signupForm" class="row g-3" novalidate @submit="validateForm($event)">
      <div class="col-md-2">
        <label for="name" class="form-label required">Name</label>
      </div>
      <div class="col-md-10">
        <input required tabindex="1" type="text" class="form-control" id="name" placeholder="Max Mustermann" ref="input">
        <div class="invalid-feedback">
          Please enter a username.
        </div>
      </div>
      <div class="col-md-2">
        <label for="street" class="form-label required">Straße</label>
      </div>
      <div class="col-md-10">
        <input required tabindex="2" type="text" class="form-control" id="street" placeholder="Musterstr. 13">
        <div class="invalid-feedback">
          Please enter a street.
        </div>
      </div>
      <div class="col-md-2">
        <label for="postcode" class="form-label required">PLZ</label>
      </div>
      <div class="col-md-2">
        <input required tabindex="3" type="number" class="form-control" id="postcode" placeholder="12345" minlength="5">
        <div class="invalid-feedback">
          Please enter a post code.
        </div>
      </div>
      <div class="col-md-2">
        <label for="city" class="form-label required">Ort</label>
      </div>
      <div class="col-md-6">
        <input required tabindex="4" type="text" class="form-control" id="city" placeholder="Musterstadt">
        <div class="invalid-feedback">
          Please enter a city.
        </div>
      </div>
      <div class="col-md-2">
        <label class="form-label required" for="password">Email</label>
      </div>
      <div class="col-md-10">
        <input id="email" class="form-control" placeholder="name@example.com" required tabindex="5" type="email">
        <div class="invalid-feedback">
          Please enter a valid email address.
        </div>
      </div>
      <PasswordInput id="password" label="Password" placeholder="password min 6 with chars and numbers" :tabindex="6" />
      <div class="col-12 small">
        <div class="feedback">
          <span class="required"></span> required input field.
        </div>
      </div>
      <div class="col-12 text-center">
        <button tabindex="7" type="submit" id="submit" class="btn btn-primary">Submit</button>
      </div>
    </form>
  </fieldset>
  </div>
</template>

<style scoped>
fieldset {
  border: 2px solid #000;
  border-radius: 5px;
  padding: 10px;
}

legend {
  font-size: 24px;
  margin-top: -32px;
  background-color: var(--bs-body-bg);
  width: auto;
  margin-left: 10px;
  padding: 0 7px 0 5px;
}
</style>

<style>
.form-control:hover {
  border-color: #86b7fe;
  outline: 0;
  box-shadow: 0 0 0 0.25rem rgba(13, 110, 253, 0.25);
}

.form-control {
  width: 100%;
  margin-top: -5px;
}

.required:after {
  content:" *";
  color: red;
}
</style>