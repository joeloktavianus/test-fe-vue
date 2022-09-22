<template>
    <div class="card">
        <div class="grid-container-post">
            <div class="name-post">
            {{ nama.name }}
            </div>
            <div class="post-post">
            {{ post.title }}
            <p class="comment-post">
                <router-link :to="{path:'/postDetail/' +  post.id + '/' +  nama.name}" className="comment-button"><font-awesome-icon icon="comment" class="icon-comment"/>{{ totalComment }}   Detail</router-link>
            </p>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'CardPost',
  props: {
    post: []
  },
  data () {
    return {
      nama: [],
      totalComment: 0
    }
  },
  async created () {
    this.getName()
    this.getTotalComment()
  },
  methods: {
    getName () {
      axios.get('https://jsonplaceholder.typicode.com/users/' + this.post.userId)
        .then((response) => {
          this.nama = response.data
        })
        .catch((error) => {
          console.log(error)
        })
    },
    getTotalComment () {
      axios.get('https://jsonplaceholder.typicode.com/posts/' + this.post.id + '/comments')
        .then((response) => {
          this.totalComment = response.data.length
        })
        .catch((error) => {
          console.log(error)
        })
    }
  }
}
</script>

<style>
 .grid-container-post {
    display: grid;
    grid-template-columns: 50px 300px;
    gap: 40px;
    padding-top: 20px;
    width: 350px;
  margin: auto;
}

.name-post {
  padding: 10px 0px 0px;
  font-size: 15px;
    font-weight: 5SS00;
    color: black;
  white-space: break-spaces;
  text-align: right;
}

.post-post {
    color:#949192;
  white-space: break-spaces;
  text-align: left;
}

.comment-post {
    color: #6092e1;
    font-size: 15px;
    padding-top: 8px;
    white-space: break-spaces;
    text-align: left;
    text-decoration: none;
}
</style>
