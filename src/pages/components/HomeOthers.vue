<template>
  <div>
   <strong>{{this.activeCount}} items left</strong>
   <br>
   <router-link to="/All">All</router-link>
   <router-link to="/Active">Active</router-link>
   <router-link to="/complete">complete</router-link>
   <button @click="cleanCompletedItem">completed</button>
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
      this.list.forEach((value,index) => {
        if(value.ifdone) {
          this.list.splice(index,1)
        }
      })
    }
  }
}
</script>
