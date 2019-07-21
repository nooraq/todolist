<template>
  <div>
    <keep-alive>
    <home-pages :list="todolist"></home-pages>
    </keep-alive>
    <home-others :list="todolist"></home-others>
  </div>
</template>

<script>
import HomePages from './components/HomePages'
import HomeOthers from './components/HomeOthers'
export default {
  name: 'Home',
  data () {
    return {
      todolist: []
    }
  },
  components: {
    HomePages,
    HomeOthers
  }
}
</script>
