<template>
  <div class='wrapper-profile'>
    <a href='/posts' class="back-button-profile"><font-awesome-icon icon="arrow-left" /></a>
    <div class="container-profile">
      <p>Username</p>
      <p>:</p>
      <p>{{username}}</p>
      <p>Email</p>
      <p>:</p>
      <p>{{email}}</p>
      <p>Address</p>
      <p>:</p>
      <p>{{address}}</p>
      <p>Phone</p>
      <p>:</p>
      <p>{{phone}}</p>
        <!-- <ul class="paddingUl">
            <li class="title">Username</li>
            <li>:</li>
            <li class="value">{{username}}</li>
        </ul>
        <ul class="paddingUl">
            <li class="title">Email</li>
            <li>:</li>
            <li class="value">{{email}}</li>
        </ul>
        <ul class="paddingUl">
            <li class="title">Address</li>
            <li>:</li>
            <li class="value">{{address}}</li>
        </ul>
        <ul class="paddingUl">
            <li class="title">Phone</li>
            <li>:</li>
            <li class="value">{{phone}}</li>
        </ul> -->
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  Data () {
    return {
      profile: [],
      username: '',
      email: '',
      address: '',
      phone: ''
    }
  },
  props: {
    userId: String
  },
  beforeCreated () {
    this.getProfile()
  },
  methods: {
    getProfile () {
      axios.get('https://jsonplaceholder.typicode.com/users/' + this.userId)
        .then((response) => {
          this.profile = response.data
          this.username = this.profile.username
          this.email = this.profile.Email
          this.address = this.profile.Address
          this.phone = this.profile.Phone
        })
        .catch((error) => {
          console.log(error)
        })
    }
  }
}
</script>

<style>
.wrapper-profile {
  width:400px;
  margin: auto;
}
.container-profile {
  display: grid;
  grid-template-columns: 40% 5% 55%;
}
.container-profile p {
  text-align: left;
}
.back-button-profile {
  float: left;
  padding-right: 300px;
}
.wrapper-profile {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding-top: 40px;
}
.paddingUl {
    padding: 12px 0px 12px 0px;
}
.title {
    width: 100px;
    text-align: left;
}
.value {
    padding-left: 5px;
}
</style>
