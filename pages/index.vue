<template>
  <div class="wrapper main-page">
    <div class="main-page__form">
      <h1 class="main-page__form-title">Добавить</h1>
      <Form @addNewPost="addNewPost" />
      <div class="main-page__post-list">
        <h2 class="main-page__post-list-title">Список</h2>
        <postList :postList="postList" @removePost="removePost" />
      </div>
    </div>
  </div>
</template>

<script>
import PostList from '@/components/PostList.vue'
import Form from '@/components/Form.vue'
export default {
  name: 'MainPage',
  components: {
    PostList,
    Form,
  },
  data() {
    return {
      postList: [],
    }
  },
  methods: {
    addNewPost(data) {
      if (this.disabled) {
        return console.log('disabled')
      }
      this.$axios.post('/posts', data)
      this.postList = [...this.postList, data]
    },
    async getPostList() {
      const posts = await this.$axios
        .get('/posts?_limit=4')
        .then((res) => res.data)
      const photoList = await this.$axios
        .get('/photos?_limit=4')
        .then((res) => res.data)
      this.postList = posts.map((i, indx) => ({
        ...i,
        photo: photoList[indx].thumbnailUrl,
      }))
    },
    removePost(id) {
      this.postList = this.postList.filter((i) => i.id != id)
      this.$axios.delete(`/posts/:${id}`)
    },
  },
  mounted() {
    this.getPostList()
  },
}
</script>

<style lang="scss">
.wrapper {
  padding: 20px 0 0 0;
}

.main-page {
  &__form-title {
    text-align: center;
    margin-bottom: 20px;
  }
  &__post-list {
    margin-top: 20px;
    &-title {
      text-align: center;
      margin-bottom: 20px;
    }
  }
}
</style>
