<template>
  <div class="card">
  <h2>{{ title }}</h2>

    <app-button
      @action="open">
      {{isNewsOpen ? 'close' : 'open'}}
    </app-button>

    <app-button
      color="danger"
      v-if="wasRead" @click="$emit('unmark', id)">
      read
    </app-button>

    <div v-if="isNewsOpen">
      <hr>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Harum earum voluptas officia eligendi enim, labore repellat dicta alias facilis voluptatem!</p>
      <app-button
        v-if="!wasRead"
        color="primary"
        @action="mark">
        Read news
      </app-button>

      <app-news-list></app-news-list>
    </div>
  </div>
</template>

<script>
import AppButton from './AppButton'
import AppNewsList from './AppNewsList'
export default {
  //props: ['title'],
  //emits:['open-news'],
  props: {
    wasRead: Boolean,
    title: {
      type: String,
      required: true
    },
    id: {
      type: Number,
      required: true
    },
    isOpen: {
      type: Boolean,
      required: false,
      default: false,
      validator(value) {
        return value === true || value === false
      }
    }
  },
  emits: {
    'open-news': null,
    'read-news'(id) {
      if(id) {
        return true
      }
      console.warn('dont have id parametr for emit read-news')
      return false
    },
    unmark: null
  },
  data() {
    return {
      isNewsOpen: this.isOpen
    }
  },

  methods: {
    open() {
      this.isNewsOpen = !this.isNewsOpen
      if(this.isNewsOpen) {
        this.$emit('open-news')
      }
    },
    mark() {
      this.isNewsOpen = false
      this.$emit('read-news', this.id)
    },
    // unmark() {
    //   this.$emit('unmark', this.id)
    // }
  },
  components: {AppButton, AppNewsList}
}
</script>