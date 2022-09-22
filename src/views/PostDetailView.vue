<template>
    <div class="wrapper-post-detail">
        <a href='/posts' class="back-button"><font-awesome-icon icon="arrow-left" /></a>
          <div class="grid-container-post-detail">
            <div class="name-detail-post">
              {{ name }}
            </div>
            <div class="post-detail-post">
              {{ post.title }}
            </div>
            <div class="body-detail-post">
              {{ post.body }}
            </div>
            <div v-if="isShown" class="comment-detail-post">
              <p><b>All Comment</b></p>
              <div v-for="comment in comments" :key="comment.id">
                <div class="grid-container-comment">
                  <div class="name-comment">
                    {{ comment.name }}
                  </div>
                  <div class="post-comment">
                    {{ comment.body }}
                  </div>
                </div>
              </div>
            </div>
            <div v-else-if="!isShown" class="comment-detail-post">
              <p>
                <a href='#' @click="showComment" style="text-decoration: none" class="comment-button"><font-awesome-icon icon="comment" class="icon-comment"/>5</a>
              </p>
            </div>
          </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
  props: {
    postId: String,
    name: String
  },
  data () {
    return {
      isShown: false,
      post: [],
      comments: []
    }
  },
  async created () {
    this.getPost()
  },
  methods: {
    showComment () {
      this.getComments()
      this.isShown = !this.isShown
    },
    getPost () {
      axios.get('https://jsonplaceholder.typicode.com/posts/' + this.postId)
        .then((response) => {
          this.post = response.data
        })
        .catch((error) => {
          console.log(error)
        })
    },
    getComments () {
      axios.get('https://jsonplaceholder.typicode.com/posts/' + this.postId + '/comments')
        .then((response) => {
          this.comments = response.data
        })
        .catch((error) => {
          console.log(error)
        })
    }
  }
}
</script>

<style>
.back-button {
  float: left;
}
.wrapper-post-detail {
  margin: auto;
  width: 60%;
  flex-direction: column;
  align-items: center;
}

.grid-container-post-detail {
  display: grid;
  grid-template-columns: 20% 80%;
  gap: 30px;
  padding: 10px;
}

.name-detail-post {
  width: 100px;
  text-align: right;
  color: black;
  padding-top: 40px;
  grid-row-start: 1;
  grid-row-end: 4;
  white-space: break-spaces;
}

.post-detail-post {
  display: flex;
  text-align: left;
    padding-top: 20px;
  color:#b3afb0;
  white-space: break-spaces;
}

.body-detail-post {
  width: 100%;
  text-align: left;
    padding: 0px 0px 0px 0px;
    color: #d2d2d2;
    white-space: break-spaces;
}

.comment-detail-post {
    text-align: left;
    color: #acacac;
    font-size: 15px;
    padding-top: 8px;
}

.grid-container-comment {
  display: grid;
  grid-template-columns: 20% 80%;
  gap: 50px;
  padding: 10px;
}

.post-comment {
    color: #d2d2d2;
  white-space: break-spaces;
}

.name-comment{
    font-weight: 700;
    align-content: flex-start;
    color: black;
    font-size: 14px;
  white-space: break-spaces;
}
</style>
