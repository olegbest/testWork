<template>
  <div class="image" v-if="pic"><img :src="getImgUrl(pic)" alt=""></div>
</template>

<script>

export default {
  props: ['pic'],
  methods: {
    getImgUrl (pic) {
      return require('../assets/images/' + pic)
    }
  }
}

</script>
