<template>
  <b-list-group>
    <b-list-group-item
      button
      v-for="post in postList"
      :key="post.id"
      class="post-item"
    >
      <div
        class="post-item__image"
        :class="{ 'post-item__image--not': !post.photo }"
      >
        <img v-if="post.photo" :src="post.photo" alt="" />
      </div>
      <div class="post-item__info">
        <span class="post-item__title">
          {{ post.title }}
        </span>
        <div class="post_item__descirption">
          {{ post.body }}
        </div>
      </div>
      <div class="post-item__buttons">
        <b-button variant="danger" size="sm" @click="removePost(post.id)"
          >Delete</b-button
        >
      </div>
    </b-list-group-item>
  </b-list-group>
</template>

<script>
export default {
  name: 'postList',
  props: {
    postList: Array,
  },
  methods: {
    removePost(id) {
      this.$emit('removePost', id)
    },
  },
}
</script>

<style lang="scss" scoped>
.post-item {
  display: flex;
  align-items: center;
  &__image {
    margin-right: 15px;
    width: 30px;
    height: 30px;
    border-radius: 50%;
    overflow: hidden;
    &--not {
      background: #cdcdcd;
    }
  }
  &__info {
    flex: 1;
    padding-right: 30px;
  }
  &__title {
    font-size: 20px;
    font-weight: 700;
  }
  &__description {
    font-size: 14px;
    margin-top: 10px;
  }
  &__buttons {
    margin-left: auto;
  }
}
</style>
