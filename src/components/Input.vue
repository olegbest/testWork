<template>
  <div class="input">
    <input type="text" :placeholder="placeholder" :value="value" @input="$emit('input', $event.target.value)">
  </div>
</template>

<script>

export default {
  props: ['placeholder', 'value']
}

</script>
