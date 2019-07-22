<template>
  <div>
   <strong>{{this.activeCount}} items left</strong>
   <br>
   <router-link to="/All">All</router-link>
   <router-link to="/Active">Active</router-link>
   <router-link to="/Complete">Complete</router-link>
   <button @click="cleanCompletedItem"> clean completed</button>
  </div>
</template>

<script>
export default {
  name: 'HomeOthers',
  props: {
    list: {
      type: Array
    }
  },
  computed: {
    activeCount: function () {
      let count = 0
      this.list.forEach((value) => {
        if (!value.ifdone) {
          count += 1
        }
      })
      return count
  }
  },
  methods: {
    cleanCompletedItem () {
      const length = this.list.length
      for (let i = length-1; i > -1; i -= 1){
        if (this.list[i].ifdone) {
          this.list.splice(i, 1)
        }
      }
    }
  },
  watch: {
    $route () {
      console.log(this.$route.params)
      console.log(this.$route.params.itemlist)
      if(this.$route.params.itemlist === 'Complete'){
        this.list.forEach((value) => {
          if (!value.ifdone) {
            value.ifshow = false
          }else {
            value.ifshow = true
          }
        })
      }
      if(this.$route.params.itemlist === 'Active'){
        this.list.forEach((value) => {
          if (value.ifdone) {
            value.ifshow = false
          }else{
            value.ifshow = true
          }
        })
      }
      if(this.$route.params.itemlist === 'All'){
        this.list.forEach((value) => {
          value.ifshow = true
        })
      }
    }
  }
}
</script>
