<template>
  <div id="app" class="app">
    <div class="container">
      <div class="content">
        <ImageComponent pic="NoPath.png"></ImageComponent>
        <div class="middle">
          <div class="title">Beautiful landscape</div>
          <Button text="Donate Author" class="donate-button" :disabled="true" icon="cash.svg"></Button>
        </div>
        <Chat @addComment="addComment"></Chat>
        <div class="comments">
          <Comment :info="c" v-for="(c, i) in comments" :key="i" @deleteComment="deleteComment(i)" @EditComment="EditComment(i, $event)"></Comment>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'app',
  components: {
    ImageComponent: () => import('./components/Image.vue'),
    Button: () => import('./components/Button.vue'),
    Comment: () => import('./components/Comment.vue'),
    Chat: () => import('./components/Chat.vue')
  },
  data () {
    return {
      comments: [
        { author: 'Jason X', text: 'That\'s awesome! What techniques are you used to took it?', image: 'jasonx.png' },
        { author: 'Jason X', text: 'That\'s awesome! What techniques are you used to took it?', image: 'jasonx.png' },
        { author: 'Jason X', text: 'That\'s awesome! What techniques are you used to took it?', image: 'jasonx.png' }
      ],
      activeUser: {
        author: 'Jason X',
        image: 'jasonx2.png'
      }
    }
  },
  methods: {
    addComment (text) {
      let { author, image } = this.activeUser
      this.comments.push({
        author,
        image,
        text
      })
    },
    deleteComment (id) {
      let arr = [...this.comments]
      arr.splice(id, 1)
      this.comments = arr
    },
    EditComment (id, data) {
      this.comments[id].text = data.value
    }
  }
}
</script>

<style lang="scss">

  @import url('https://fonts.googleapis.com/css?family=Montserrat&display=swap');
  @import "sass";

  * {
    margin: 0;
    padding: 0;
    font-family: Montserrat;
  }

  html, body {
    height: 100%;
    background: #F0F0F0;
  }

  button, input {
    outline: none;
  }

  .app {
    @extend %flex;
    @include jc(center);
    @include ai (center);
    height: 100%;

    .container {
      width: 568px;
      background: white;
      border-radius: 8px;
      box-shadow: rgba(0,0,0,0.16) 0 8px 32px;
    }

    .content {
      width: 536px;
      margin: auto;
      padding-top: 16px;
      padding-bottom: 16px;

      .image {
      }

      > .middle {
        @extend %flex;
        @include jc(space-between);
        margin-top: 16px;
        margin-bottom: 16px;
        .title {
          font-size: 20px;
        }

        .donate-button {
          background: linear-gradient(160deg,#BEC2F3,#F7CAEB);
          width: 136px;
          height: 32px;
          border-radius: 4px;
          .icon {
            margin-left: 8px;
            margin-top: 4px;
          }
          button {
            border: none;
            background: transparent;
            font-size: 11px;
            color: #222222;
            font-weight: bold;
          }
        }
      }

      .comments {
      }
    }
  }
</style>
