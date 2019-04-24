<template>
  <div
    v-draggable
    class="postit"
    :style="{
      display: post.visible ? 'block' : 'none',
      background: post.color,
      top: `${post.pos.y}px`,
      left: `${post.pos.x}px`
    }"
  >
    <input
      v-model="post.title"
      :disabled="!editMode"
      @click="editMode = true"
      @blur="editMode = false"
    />
    <p>{{ post.desc }}</p>
    <div class="colors">
      <ul v-for="color in colors" :key="color">
        <li @click="changeColor(color)">{{ color }}</li>
      </ul>
      <button @click="remove()">remove</button>
    </div>
  </div>
</template>
<script>
import { Draggable } from 'draggable-vue-directive'

export default {
  directives: {
    Draggable
  },
  props: {
    colors: {
      default: 'yellow'
    },
    postit: {
      type: Object,
      default: () => {
        return {
          id: 0,
          title: '',
          desc: '',
          pos: {
            x: 0,
            y: 0
          },
          color: 'azure',
          visible: true
        }
      }
    }
  },
  data() {
    return {
      editMode: true
    }
  },
  computed: {
    post() {
      return this.postit
    }
  },
  methods: {
    changeColor(color) {
      this.post.color = color
    },
    remove() {
      this.post.visible = false
    }
  }
}
</script>
<style lang="scss" scoped>
.postit {
  min-height: 300px;
  width: 200px;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 20;
}
</style>
