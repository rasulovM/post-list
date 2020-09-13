<template>
  <form class="form" @submit.prevent="addNewPost">
    <b-input
      class="mb-2 mr-sm-2 mb-sm-0 form__input"
      placeholder="Название"
      v-model="post.name"
    ></b-input>
    <b-input
      class="mb-2 mr-sm-2 mb-sm-0 form__input"
      placeholder="Описание"
      v-model="post.description"
    ></b-input>
    <b-button
      type="submit"
      :variant="disabled ? 'secondary' : 'primary'"
      class="form__button"
      >Save</b-button
    >
  </form>
</template>

<script>
export default {
  name: 'Form',
  props: {},
  data() {
    return {
      post: {},
      disabled: true,
    }
  },
  watch: {
    post: {
      handler(value) {
        value.name && value.description
          ? (this.disabled = false)
          : (this.disabled = true)
      },
      deep: true,
    },
  },
  methods: {
    addNewPost() {
      if (this.disabled) {
        return null
      }

      const data = {
        userId: Math.floor(Math.random() * 9999) + 1,
        id: Math.floor(Math.random() * 9999) + 1,
        title: this.post.name,
        body: this.post.description,
      }
      this.post = {}
      this.$emit('addNewPost', data)
    },
  },
}
</script>
<style lang="scss" scoped>
.form {
  width: 100%;
  position: relative;
  display: flex;
  &__wrapper {
    display: flex;
    flex-direction: column;
    flex: 1;
  }
  &__input {
    &:last-child {
      margin-top: 15px;
    }
  }
  &__button {
    margin-left: 40px;
  }
}
</style>
