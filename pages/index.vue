<template>
  <div>
    <div class="container" @click="addNew($event)"></div>
    <pre>{{ tmp }}</pre>
    <div v-for="postit of postits" :key="postit.id">
      <PostIt :colors="colors" :postit="postit" />
    </div>
  </div>
</template>

<script>
import PostIt from '~/components/PostIt.vue'

export default {
  components: {
    PostIt
  },
  data() {
    return {
      tmp: '',
      postits: [],
      colors: ['yellow', 'red', 'purple', 'azure', 'blue']
    }
  },
  methods: {
    addNew(e) {
      this.postits.push({
        id: e.clientX,
        pos: {
          x: e.clientX,
          y: e.clientY
        },
        color: 'yellow',
        visible: true
      })
    }
  }
}
</script>

<style>
.container {
  position: absolute;
  margin: 0 auto;
  min-height: 100vh;
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  z-index: 10;
  background: #ccc;
}
</style>
