<template>
    <div>
      <div class="form-field">
        <input type="text" placeholder="search" v-model="searchTerm" @change="postsData"/>
        <font-awesome-icon icon="search" class="icon-search"/>
      </div>
      <div v-for="post in computedPost" :key="post.id" class="post-post">
         <CardPost :post="post" />
      </div>
      <div class="paginate">
        <ul class="pagination">
            <li class="page-item">
              <button @click="prev" class="page-link">
                prev
              </button>
            </li>
              <div v-for="page in totalPages" :key="page">
                <li class="page-item">
                  <div v-if="page === currentPage">
                    <button @click="pageClick(page)" class="page-link-active">
                      {{ page }}
                    </button>
                  </div>
                  <div v-else>
                    <button @click="pageClick(page)" class="page-link">
                      {{ page }}
                    </button>
                  </div>
                </li>
              </div>
            <li class="page-item">
              <button @click="next" class="page-link">
                next
              </button>
          </li>
        </ul>
      </div>
    </div>
</template>

<script>
import CardPost from '@/components/CardPost.vue'
import axios from 'axios'

export default {
  name: 'PostView',
  components: {
    CardPost
  },
  data () {
    return {
      posts: [],
      computedPost: [],
      searchTerm: '',
      currentPage: 1,
      totalPages: 0,
      totalPosts: 1,
      postsPerPage: 10
    }
  },
  mounted () {
    this.getPosts()
  },
  methods: {
    getPosts () {
      axios.get('https://jsonplaceholder.typicode.com/posts')
        .then((response) => {
          this.posts = response.data
          this.postsData()
        })
        .catch((error) => {
          console.log(error)
        })
    },
    postsData () {
      this.totalPages = 0
      this.computedPost = this.posts
      if (this.searchTerm) {
        this.computedPost = this.computedPost.filter(posts => {
          return posts.title.toLowerCase().includes(this.searchTerm.toLowerCase())
        })
      }

      this.totalPosts = this.computedPost.length
      for (let i = 1; i <= Math.ceil(this.totalPosts / this.postsPerPage); i++) {
        this.totalPages += 1
      }

      this.computedPost = this.computedPost.slice((this.currentPage - 1) * this.postsPerPage, (this.currentPage - 1) * this.postsPerPage + this.postsPerPage)
    },
    next () {
      this.currentPage = this.currentPage + 1
      this.postsData()
    },
    prev () {
      this.currentPage = this.currentPage - 1
      this.postsData()
    },
    pageClick (page) {
      this.currentPage = page
      this.postsData()
    }
  }
}
</script>

<style>
  .form-field {
    display: grid;
    grid-template-columns: 90% 10%;
    margin: auto;
    width: 400px;
    border-radius: 25px;
    background-color: #eff3f4;
    border: none;
  }
.icon-search {
  padding-top: 12px;
}
.form-field input {
    display: block;
    border: none;
    outline: none;
    background: none;
    font-size: 1rem;
    width: 100%;
    height: 40px;
    padding: 0px 0px 0px 10px;
    text-align: center;
    color: #c9d0d6;
    font-weight: 600;
}
.paginate {
  margin: auto;
  width: 60%;
}

.pagination {
  border: none;
  color:#949192;
}

.page-link {
  display: inline-block;
  cursor: pointer;
  border: none;
  font-size: 16px;
  margin: 4px 2px;
  padding: 9px 10px;
  background-color: white;
}

.page-link-active{
  display: inline-block;
  cursor: pointer;
  border: none;
  font-size: 16px;
  margin: 4px 2px;
  padding: 9px 10px;
  background-color: white;
  text-decoration:underline;
}
</style>
