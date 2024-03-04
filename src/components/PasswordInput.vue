<script setup>
import {computed, ref, watch} from "vue";

const props = defineProps({
  id: {type: String, required: true},
  label: {type: String, required: true},
  placeholder: {type: String, required: true},
  tabindex: {type: Number, required: true},
});

const password = ref('');
let passwordSecurityLevel = ref('');

watch(
    password,
    (actualPassword) => {
      getPasswordSecurityLevel(actualPassword);
    },
)

function getPasswordSecurityLevel(passwordToValidate) {
  const lightPassword = /^(\S)(?=.*\d)(?=.*[a-z])[a-z0-9]{6,10}$/
  const middlePassword = /^(\S)(?=.*\d)(?=.*[A-Z])(?=.*[a-z])[a-zA-Z0-9]{8,16}$/;
  const strongPassword = /^(\S)(?=.*\d)(?=.*[A-Z])(?=.*[a-z])(?=.*[~`!@#$%^&*()--+={}\[\]|\\:;"'<>,.?/_₹])[a-zA-Z0-9~`!@#$%^&*()--+={}\[\]|\\:;"'<>,.?/_₹]{10,32}$/;

  if (passwordToValidate === '') {
    passwordSecurityLevel = '';
  }
  else if (strongPassword.test(passwordToValidate)) {
    passwordSecurityLevel = '<div class="securityIndicator strongSecurity">strong</div>';
  }
  else if (middlePassword.test(passwordToValidate)) {
    passwordSecurityLevel = '<div class="securityIndicator middleSecurity">middle</div>';
  }
  else if (lightPassword.test(passwordToValidate)) {
    passwordSecurityLevel = '<div class="securityIndicator lightSecurity">light</div>';
  }

  document.getElementById('password').setCustomValidity('');
}

</script>

<template>
  <div class="col-md-2">
    <label class="form-label required" for="password">{{ label }}</label>
  </div>
  <div class="col-md-8">
    <input :id="id" class="form-control" :placeholder="placeholder" required :tabindex="tabindex" type="password" v-model="password" minlength="6">
    <div class="invalid-feedback">
      password min 6 with chars and numbers
    </div>
  </div>
  <div class="col-md-2">
    <div v-html="passwordSecurityLevel" style="display: block"></div>
  </div>
</template>

<style>
.securityIndicator {
  text-align: center;
  border-radius: 5px;
}

.lightSecurity {
  background-color: red;
  color: white;
}

.middleSecurity {
  background-color: yellow;
  color: black;
}

.strongSecurity {
  background-color: green;
  color: white;
}
</style>