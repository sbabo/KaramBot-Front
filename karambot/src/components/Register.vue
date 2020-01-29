<template>
  <div class="middle">
    <b-form @submit="Register" @reset="onReset" @cancel="onCancel" v-if="show">
      <b-form-group
        id="input-group-1"
        label="Username :"
        label-for="input-1"
      >
        <b-form-input
          id="input-1"
          v-model="form.username"
          type="text"
          required
          placeholder="Choose an username..."
        ></b-form-input>
      </b-form-group>

      <b-form-group
        id="input-group-2"
        label="Email address:"
        label-for="input-2"
        description="We'll never share your email with anyone else."
      >
        <b-form-input
          id="input-2"
          v-model="form.email"
          type="email"
          required
          placeholder="Choose an email..."
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-3" label="Password:" label-for="input-3">
        <b-form-input
          id="input-3"
          v-model="form.password"
          type="password"
          required
          placeholder="Choose a password..."
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
      <b-button type="cancel" v-on:click="onCancel" variant="">Cancel</b-button>
    </b-form>
  </div>
</template>

<style>
.middle {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
}
</style>
<script>
import axios from 'axios'
  export default {
    data() {
      return {
        form: {
          username: '',
          email: '',
          password: '',
          food: null,
          checked: []
        },
        show: true
      }
    },
    methods: {
      onSubmit(evt) {
        evt.preventDefault()
        alert(JSON.stringify(this.form))
      },
      onReset(evt) {
        evt.preventDefault()
        // Reset our form values
        this.form.email = ''
        this.form.password = ''
        this.form.username = ''
        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      },
      Register(evt) {
        axios.post('http://127.0.0.1:8000/player/register', {
          user_name: this.form.username,
          email: this.form.email,
          password: this.form.password
        })
        .then(response => (console.log(this.info = response.data)))
        this.$router.push({name: "login"});
      },
      onCancel(evt) {
        this.$router.push({name: "login"});
      }
    }
  }
</script>