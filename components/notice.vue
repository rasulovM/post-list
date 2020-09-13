<template>
  <div class="notice">
    <b-icon
      v-if="err"
      icon="exclamation-circle-fill"
      class="notice__icon"
      variant="danger"
    ></b-icon>
    <b-icon
      v-else
      icon="exclamation-circle-fill"
      class="notice__icon"
      variant="primary"
    ></b-icon>
    <span class="notice__title">{{ notice }}</span>
  </div>
</template>

<script>
import { BIcon } from 'bootstrap-vue'
export default {
  name: 'Notice',
  props: {
    notice: String,
    err: Boolean,
  },
  components: {
    BIcon,
  },
}
</script>

<style lang="scss" scoped>
.notice {
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  margin: 50px auto 0;
  background: #ffffff;
  border-radius: 20px;
  padding: 20px;
  width: fit-content;
  z-index: 999;
  border: 1px solid #8f8f8f;
  &__icon {
    margin-right: 15px;
  }
}
</style>
