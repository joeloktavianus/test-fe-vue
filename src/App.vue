<template>
        <ul>
            <li class="logo">Cinta Coding</li>
            <li class="post"><router-link v-if="authenticated" to="/posts" >Post</router-link></li>
            <li v-if="!authenticated" class="button-login" style="float:right">
              <router-link  class="font-login" to="/login">
                Login
              </router-link>
            </li>
            <li v-if="authenticated" class="dropdown" style="float:right">
              <button class="dropbtn">Welcome, {{ name }}</button>
              <div class="dropdown-content">
                <router-link class="link-profile" :to="{path:'/profile/' +  userId }">
                      Detail Profile
                    </router-link>
              </div>
              <!-- <ul class="dropdown" :class="{ isOpen }">
                  <li>
                    <router-link :to="{path:'/profile/' +  userId }">
                      Detail Profile
                    </router-link>
                  </li>
              </ul> -->
            </li>
        </ul>
  <router-view @authenticated="setAuthenticated" />
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      authenticated: false,
      name: '',
      userId: ''
    }
  },
  mounted () {
    if (!this.authenticated) {
      this.$router.replace({ name: 'home' })
    }
  },
  methods: {
    setAuthenticated ({ authenticated, id, name }) {
      this.name = name
      this.userId = id
      this.authenticated = authenticated
      console.log(this.authenticated)
    },
    logout () {
      this.authenticated = false
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
    white-space: nowrap;
}

.button-login {
  font-weight: bold;
  align-items: center;
  background-color: #3EB2FD;
  border-radius: 100px;
}

.font-login {
  color: white;
  padding: 10px 30px 10px 30px
}

.logo {
  font-weight: bold;
  font-size: 20px;
  padding-top: 10px;
}

.post {
  margin: 0 0 0 30%;
  text-decoration: underline;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}

ul {
  list-style-type: none;
  /* margin: 0; */
  padding: 0;
  overflow: hidden;
  background-color: white;
    width: 70%;
    margin: auto;
}

li {
  float: left;
}

li a {
  display: block;
  color: black;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
}

.dropbtn {
  background-color: white;
  color: black;
  padding: 16px;
  font-size: 16px;
  border: none;
  cursor: pointer;
}

.dropdown {
  position: relative;
  display: inline-block;
}

.dropdown-content {
  display: none;
  position: absolute;
  right: 0;
  background-color: #f9f9f9;
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
  z-index: 1;
  border-radius: 10px;
  border: #3EB2FD;
}

.dropdown-content .link-profile {
  float: none;
  color: black;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
}

.dropdown-content .link-profile:hover {background-color: #f1f1f1;}
.dropdown:hover .dropdown-content {display: inline;}
.dropdown:hover .dropbtn {background-color: white}
</style>
