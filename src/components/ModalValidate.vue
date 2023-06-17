<template>
  <TheModal @close="$emit('close')" title="modal with form">
    title="Modal with form + Validate" @close="$emit('close')">

    <div slot="body">
      <form @submit.prevent="onSubmit">
        <div class="form-item" :class="{ errorInput: $v.name.$error }">
          <label>Name:</label>
          <p class="errorText" v-if="!$v.name.required">Filed is required!</p>
          <p class="errorText" v-if="!$v.name.minLength"></p>
          <p v-if="password !== repeatPassword">Passwords are note match</p>

          <input
            v-model="name"
            :class="{ error: $v.name.$error }"
            @change="$v.name.$touch()"
          />
        </div>

        <div class="form-item" :class="{ errorInput: $v.email.$error }">
          <label>Email:</label>
          <p class="errorText" v-if="!$v.email.required">Filed is required!</p>
          <p class="errorText" v-if="!$v.email.email">Email is not correct!</p>
          <input
            v-model="email"
            :class="{ error: $v.email.$error }"
            @change="$v.email.$touch()"
          />
          <label>password</label>
          <input
            :class="{ error: $v.email.$error }"
            v-model="password"
            type="password"
          />
          <label>repeat password</label>
          <input
            :class="{ error: $v.email.$error }"
            v-model="repeatPassword"
            type="password"
          />
        </div>

        <button class="btn btnPrimary">Submit!</button>
      </form>
    </div>
  </TheModal>
</template>

<script>
import { required, minLength, email } from "vuelidate/lib/validators";

import TheModal from "./TheModal.vue";
export default {
  components: { TheModal },
  data() {
    return {
      name: "",
      email: "",
      password: "",
      repeatPassword: "",
    };
  },
  validations: {
    name: {
      required,
      minLength: minLength(4),
    },
    email: {
      required,
      email,
    },
  },
  methods: {
    onSubmit() {
      this.$v.$touch();
      if (!this.$v.$invalid && this.password === this.repeatPassword) {
        const user = {
          name: this.name,
          email: this.email,
        };
        console.log(user);

        this.name = "";
        this.email = "";
        this.$v.$reset();
        this.$emit("close");
      }
    },
  },
};
</script>
<style lang="scss">
.form-item .errorText {
  display: none;
  margin-bottom: 8px;
  font-size: 13.4px;
  color: #de4040;
}
.form-item {
  &.errorInput .errorText {
    display: block;
  }
}
input.error {
  border-color: #de4040;
}
</style>
