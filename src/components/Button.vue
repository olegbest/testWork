<template>
  <div class="button" @click="clickButton">
    <ImageComponent v-if="icon" :pic="icon" class="icon"></ImageComponent>
    <button :disabled="disabled">{{text}}</button>
  </div>
</template>

<script>
export default {
  props: ['text', 'disabled', 'click', 'icon'],
  components: {
    ImageComponent: () => import('./Image.vue')
  },
  methods: {
    clickButton () {
      if (this.click) {
        this.click()
      }
    }
  }
}
</script>

<style lang="scss" scoped>

  @import "../sass";

  .button {
    @extend %flex;
    @include ai(center);
    .icon {
      margin-right: 8px;
    }
    button {
      cursor: pointer;

    }
  }

</style>
