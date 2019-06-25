<template>
  <div :class="isActiveActions ? 'comment active' : 'comment'" ref="comment">
    <div v-show="!isDeleteComment && !isEditComment" class="cont" @click="toggleButtons('isActiveActions')" >
      <div class="action-buttons" v-if="isActiveActions">
        <Button text="Edit" class="edit-button" icon="edit.svg" :click="toggleEditComment"></Button>
        <Button text="Delete" class="delete-button" icon="delete.svg" :click="toggleDeletComment"></Button>
      </div>
      <ImageComponent :pic="info.image"></ImageComponent>
      <div class="info">
        <div class="author">{{info.author}}</div>
        <div class="text">{{info.text}}</div>
      </div>
    </div>
    <div v-if="isDeleteComment" class="delete-comment">
      <div class="text">Delete comment?</div>
      <div class="buttons">
        <Button text="No" class="action-delete-button no" :click="toggleDeletComment"></Button>
        <Button text="Yes" class="action-delete-button yes" :click="deleteComment"></Button>
      </div>
    </div>
    <div class="edit-comment" v-if="isEditComment">
      <Chat :isEdit="true" :value="info.text" @EditComment="EditComment"></Chat>
    </div>
  </div>
</template>

<script>

export default {
  props: ['info'],
  components: {
    ImageComponent: () => import('./Image.vue'),
    Button: () => import('./Button.vue'),
    Chat: () => import('./Chat.vue')
  },
  created () {
  },
  data () {
    return {
      isActiveActions: false,
      isDeleteComment: false,
      isEditComment: false
    }
  },
  methods: {
    toggleButtons (prop) {
      if (!this[prop]) {
        document.addEventListener('click', listener, false)
      }
      const that = this
      function listener (event) {
        let target = event.target
        while (target !== document) {
          if (target === that.$refs.comment) {
            return
          }
          target = target.parentNode
        }
        that[prop] = false
        document.removeEventListener('click', listener, false)
      }
      this.$set(this, prop, true)
    },
    toggleDeletComment () {
      this.toggleButtons('isDeleteComment')
      // this.isDeleteComment = !this.isDeleteComment
    },
    toggleEditComment () {
      this.toggleButtons('isEditComment')
      // this.isEditComment = !this.isEditComment
    },
    deleteComment () {
      this.$emit('deleteComment')
      this.isDeleteComment = false
      this.isActiveActions = false
    },
    EditComment (value) {
      this.$emit('EditComment', { value })
      this.isEditComment = false
    }
  }
}

</script>

<style lang="scss">

  @import "../sass";

  .comment {
    padding-left: 8px;
    margin-top: 16px;
    cursor: pointer;
    height: 48px;

    .cont {
      @extend %flex;
      @include ai(center);
    }

    &.active {
      background: #F4F5FF;
    }

    .info {
      margin-left: 16px;
      overflow: hidden;

      .author {
        font-size: 11px;
      }

      .text {
        font-size: 16px;
        white-space: pre;
      }
    }

    .action-buttons {
      @extend %flex;
      @include jc(space-around);
      width: 40%;

      button {
        background: transparent;
        border: none;
        font-size: 11px;
        font-weight: bold;
      }

      .edit-button button{
        color: #2C3BFF;
      }

      .delete-button button{
        color: #FF0000;
      }
    }
  }

  .delete-comment {
    @extend %flex;
    @include jc(space-between);
    @include ai(center);
    height: 100%;

    .buttons {
      width: 50%;
      text-align: right;
      @extend %flex;
      @include jc(flex-end);
      .action-delete-button {
        button {
          height: 48px;
          width: 50px;
          border: none;
          color: white;
          font-size: 11px;
        }
        &.no button{
          background: #2C3BFF;
        }

        &.yes button{
          background: #FF0000;
        }
      }
    }
  }

</style>
