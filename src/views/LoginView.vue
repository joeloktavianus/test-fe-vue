<template>
  <div class="login-wrapper">
    <p class="title-login">Login Page</p>
    <form>
        <input type="text" placeholder="Username" class="form-field-login" v-model="username"/>
        <input type="password" placeholder="Password" class="form-field-login" v-model="password"/>
        <button class="btn mt-3" @click="login">Login</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      users: [],
      userLogin: [],
      passwordLogin: [],
      username: '',
      password: ''
    }
  },
  mounted () {
    this.getUsers()
  },
  methods: {
    getUsers () {
      axios.get('https://jsonplaceholder.typicode.com/users')
        .then((response) => {
          this.users = response.data
        })
        .catch((error) => {
          console.log(error)
        })
    },
    login () {
      if (this.username && this.password) {
        this.userLogin = this.users
        this.userLogin = this.userLogin.filter(users => {
          return users.username.toLowerCase().includes(this.username.toLowerCase())
        })
        this.passwordLogin = this.userLogin
        this.passwordLogin = this.passwordLogin.filter(users => {
          return users.username.toLowerCase().includes(this.password.toLowerCase())
        })
        if (this.userLogin.length === 1 && this.passwordLogin.length === 1) {
          // this.$emit('authenticated', true)
          // const userId = this.userLogin.length[0].id
          // const name = this.userLogin.length[0].name
          this.$emit('authenticated', {
            authenticated: true,
            id: '1',
            name: 'name'
          })
          this.$router.replace({ name: 'posts' })
        } else {
          console.log('user dan password salah')
        }
      } else {
        console.log('belum input')
      }
    }
  }
}
</script>

<style>
    input {
        display: block;
        padding: 10px 15px 10px 10px;
    }

    .title-login {
        font-weight: 700;
        font-size: 1.4rem;
        margin-bottom: 60px;
        color: #000000;
    }

    .login-wrapper {
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .form-field-login {
        padding-left: 100px;
        margin-bottom: 20px;
        border-radius: 25px;
        border: solid #527AF5 2px;
    }

    .btn {
        box-shadow: none;
        width: 100%;
        height: 40px;
        background-color: #527AF5;
        color: #fff;
        border-radius: 25px;
        box-shadow: 3px 3px 3px #b1b1b1,
            -3px -3px 3px #fff;
        letter-spacing: 1.3px;
    }
</style>
