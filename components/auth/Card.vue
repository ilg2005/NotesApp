<template>

  <v-card class="px-12 pb-12 ma-auto w-33">
    <v-card-title class="text-h4 mb-5">{{ authState }}</v-card-title>
    <v-form
        ref="form"
        v-model="valid"
        lazy-validation
    >

      <v-text-field
          v-model="fields.email"
          :rules="rules.email"
          label="E-mail"
          required
      ></v-text-field>

      <v-text-field
          v-model="fields.password"
          :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
          :type="show1 ? 'text' : 'password'"
          @click:append="show1 = !show1"
          :rules="rules.password"
          :counter="8"
          label="Password"
          required
      ></v-text-field>

      <v-btn
          :disabled="!valid"
          color="success"
          class="mr-4"
          @click="validate"
      >
        Submit
      </v-btn>
      <p @click="toggleAuthState"
         class="msg"
      >
        {{ message[authState] }}
      </p>

    </v-form>
  </v-card>

</template>

<script setup>

const authState = ref('login');

const message = {
  login: "Don't have an account? Create one now",
  signup: "Already have an account? Log in now",
};

const toggleAuthState = () => authState.value = authState.value === 'login' ? 'signup' : 'login';

const fields = reactive({
  email: '',
  password: ''
})

const rules = {
  email: [
    v => !!v || 'E-mail is required',
    v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
  ],
  password: [
    v => !!v || 'Password is required',
    v => (v && v.length >= 8) || 'Password must be not less than 8 characters',
  ]
}
const valid = ref(true);
const show1 = ref(false);
const form = ref();
const validate = () => form.value.validate();

</script>

<style scoped>
.msg {
  margin-top: 2rem;
  cursor: pointer;
  color: blue;
}

.text-h4 {
  text-transform: capitalize !important;
}
</style>
