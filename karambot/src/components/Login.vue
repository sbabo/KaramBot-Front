<template>
  <div class="middle">
    <b-form @submit="onSend" @reset="onReset" v-if="show">
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
          placeholder="Enter your username"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Password:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.password"
          type="password"
          required
          placeholder="Enter password"
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
      <b-button type="register" v-on:click="goRegister" variant="">Register</b-button>
    </b-form>
      <b-modal ref="my-modal">{{this.info.user}}</b-modal>

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

<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

<script>
import axios from 'axios';

  export default {
    data() {
      return {
        form: {
          username: '',
          password: '',
        },
        show: true,
        info: "",
        infos: []
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
        this.form.username = ''
        this.form.password = ''
        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      },
      onSend(evt) {
        const infos = this
        axios
        .post('http://127.0.0.1:8000/player/login', {
        user_name : this.form.username,
        password : this.form.password
      })
    .then(response => {
      this.infos = response.data,
      console.log(this.infos)
      if(this.infos) {
        this.$router.push({name: "chat", params: this.infos})
      } else {
        this.showModal()
      }
    })
      },
      goRegister(evt) {
        this.$router.push({name: "register"});
      },
      showModal() {
        this.$refs['my-modal'].show()
      }
    }
  }

</script>
