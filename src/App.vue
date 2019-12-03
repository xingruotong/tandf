<template>
  <div id="app">
    <h3>总任务：{{list.length}}<br/></h3>
      <input type="text" v-model="txt" v-on:keydown="add">
      <ul v-for="(item, index) in list" :key="item.id">
        未完成<input type="checkbox" @change="weiFn">
        已完成<input type="checkbox"><br/>
        <span v-if="!item.flag">{{index+1}}：{{item.nm}}</span>
        <input type="text" v-else v-model="item.nm" @blur="editF(item.id)">
        <div class="Btn">
          
          <span @click="wei(item.id)" v-if="!item.already" :class="!item.already ? 'Already' : 'red'">未完成</span>
          <span v-else @click="yi(item.id)">已完成</span>
          <button @click="edit(item.id)">编辑</button>
          <button @click="delFn(item.id)">删除</button>
        </div>
      </ul>
    <router-view/>
  </div>
</template>
<script>
export default {
  data() {
    return {
      txt: '',
      list: [{
        nm: '向往的生活',
        flag: false,
        already: false,
        id: 0
      },],
      
    }
  },
  methods: {
    add(e) {
      if(e.keyCode === 13) {
          let obj ={
          nm: this.txt,
          flag: false,
          already: false,
          id: new Date()*1
        }
        this.list.push(obj)
        console.log(this.txt)
        this.txt = ''
      }
    },
    //编辑
    edit(id) {
      this.list.find(v => v.id == id).flag = true

    },
    //编辑
    editF(id) {
      this.list.find(v => v.id == id).flag = false
    },
    //删除
    delFn(id) {
      let index = this.list.findIndex(v => v.id == id)
      this.list.splice(index, 1)
    },
    //点击变状态
    wei(id) {
      this.list.find(v => v.id == id).already = true
    },
    //点击变状态
    yi(id) {
      this.list.find(v => v.id == id).already=false
    },
    //点击input
    weiFn() {
      let newList = this.list.filter(v => v.already == false)
      this.list = newList
    }
  }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  list-style: none;
}
.Btn {
  margin: 0 0 10px;
  span {
    display: inline-block;
    width: 70px;
    height: 30px;
    text-align: center;
    line-height: 30px;
    margin: 0 15px;
  }
  button {
    width: 70px;
    height: 30px;
  }
}
.Already {
  background: lime;
}
.red {
  background: red;
}
</style>
