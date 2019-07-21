<template>
  <div class="header">
    <h1 class="home-header">todos</h1>
    <div>
      <button class="home-itemalldone"
      @click="BtnClick"
      ref="itemalldone"
      >
      ></button>
    <input type="text" 
    placeholder="What needs to be done?" 
    autofocus="autofocus"
    autocomplete="off"
    v-model="newitem"
    @keydown.13="pushNewItem"
    >
    <ul>
      <li
      v-for="(item, index) of list"
      :key="index"
      @mouseenter="showDstryBtn(index)"
      @mouseleave="notShowDstryBtn(index)"
      >
        <input 
        type="checkbox"
        ref="todolist"
        @click="checkedChange(index)"
        >
        <label 
        @dblclick="todoitemChange(index)"
        >{{item.content}}</label>
        <input
        v-show="item.ifchange"
        v-model="item.content"
        @keydown.13="todoitemChange(index)"
        @mouseleave="listernClick(index)"
        >
        <button
        v-show="item.ifDestroyBtn"
        @click="dstryItem(index)"
        >x</button>
      </li>
    </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  props: {
    list: {
      type: Array,
      default () {
        return {
          list: []
        }
      }
    }
  },
  computed: {
    
  },
  data () {
    return {
      newitem: ''
    }
  },
  methods: {
    pushNewItem () {
      const newitem = this.newitem
      this.list.push({
        ifchange: false,
        ifDestroyBtn: false,
        ifdone: false,
        content: newitem
      })
      this.newitem = ''
    },
    BtnClick () {
      let checkeditem = 0
      this.$refs.todolist.forEach((value) => {
        if (value.checked === true) {
          checkeditem += 1
        }
      })
      if( checkeditem === this.list.length) {
        this.$refs.todolist.forEach((value,index) => {
          value.checked = false
          this.list[index].ifdone = false
      })
      }else {
        this.$refs.todolist.forEach((value,index) => {
          value.checked = true
          this.list[index].ifdone = true
      })
      }
    },
    todoitemChange (index) {
      this.list[index].ifchange = !this.list[index].ifchange
      console.log(this.list[index].ifchange)
    },
    showDstryBtn (index) {
      this.list[index].ifDestroyBtn = true
    },
    notShowDstryBtn (index) {
      this.list[index].ifDestroyBtn = false
    },
    dstryItem (index) {
      this.list.splice(index,1)
    },
    checkedChange (index) {
      this.list[index].ifdone = !this.list[index].ifdone
    },
    listernClick (index) {
      window.addEventListener('click',this.todoitemChange(index))
    }
  }
}
</script>

<style lang="stylus" >
  .home-header
    text-align: center
  .home-itemalldone
    transform:rotate(90deg)
</style>

