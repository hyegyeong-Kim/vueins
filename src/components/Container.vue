<template>
  <div>
    <Post :데이터들="데이터들"/>
</div>
</template>

<script>
import Post from './Post.vue'

export default {
  name: 'Container',
  components: {
    Post,
  },
  props : {
    데이터들 : Array,
  }
}
</script>

<style>

</style>