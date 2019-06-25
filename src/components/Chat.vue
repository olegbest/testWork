<template>
  <div class="chat">
    <Input placeholder="Write a new comment" v-model="chatValue" :class="chatValue ? 'fill' : ''"/>
    <Button text="Send" v-if="chatValue" :click="addComment"></Button>
  </div>
</template>

<script>

export default {
  props: ['value', 'isEdit'],
  components: {
    Input: () => import('./Input.vue'),
    Button: () => import('./Button.vue')
  },
  created () {
    if (this.value) {
      this.chatValue = this.value
    }
  },
  data () {
    return {
      chatValue: ''
    }
  },
  methods: {
    addComment () {
      if (this.isEdit) {
        this.$emit('EditComment', this.chatValue)
      } else {
        this.$emit('addComment', this.chatValue)
        this.chatValue = ''
      }
    }
  }
}

</script>

<style lang="scss">
  @import "../sass";

  .chat {
    @extend %flex;

    .input {
      width: 100%;
      input {
        width: 100%;
        height: 48px;
        border-radius: 4px;
        border: 0.5px solid #707070;
        padding-left: 16px;
        font-size: 16px;
        box-sizing: border-box;
      }

      &.fill {
        input {
          border-color: #2C3BFF;
        }
      }

    }

    .button {
      width: 20%;
    }
    button {
      background: #2C3BFF;
      color: #FFFFFF;
      border: none;
      width: 100%;
      height: 100%;
      border-radius: 0px 4px 4px 0px;
    }
  }
</style>
