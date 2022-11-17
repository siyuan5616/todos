<template>
  <section class="todoapp">
    <!-- 头部部分 -->
    <TodoHeader @add="add"></TodoHeader>

    <!-- 主体部分 -->
    <TodoMain :list="show" @del="del" @changeis="changeis" @isAll="isAll"></TodoMain>

    <!-- 底部部分 -->
    <TodoFooter :list="list" @clear="clear" :type="falg" @filter="filter"></TodoFooter>
  </section>
</template>

<script>
import TodoMain from "./components/TodoMain.vue";
import TodoHeader from "./components/TodoHeader.vue";
import TodoFooter from "./components/TodoFooter.vue";
export default {
  components: { TodoHeader, TodoMain, TodoFooter },
  data() {
    return {
      list: JSON.parse(localStorage.getItem('todos')) || [
        { id: 1, name: "吃饭", isDone: true },
        { id: 2, name: "睡觉", isDone: false },
        { id: 3, name: "打豆豆", isDone: true },
      ],
      falg: "all",
    };
  },
  methods: {
    //删除
    del(id) {
      this.list.splice(this.list.id === id, 1);
    },
    //单个状态修改
    changeis(id) {
      const i = this.list.find((item) => item.id === id);
      i.isDone = !i.isDone;
    },
    //添加功能
    add(text) {
      this.list.push({ id: this.list.length, name: text, isDone: false });
    },
    //清楚已完成
    clear(){
      this.list = this.list.filter(item => item.isDone===false)
    },
    //底部过滤
    filter(type){
      this.falg=type
    },
    //全选
    isAll(value){
      this.list.forEach((item) => (item.isDone = value))
    }
  },

  computed:{
    show(){
      if(this.falg==='no'){
        return this.list.filter(item => item.isDone===false)
      }else if(this.falg==='yes'){
        return this.list.filter(item => item.isDone===true)
      }else{
        return this.list
      }
    }
  },

  watch:{
    list:{
      deep:true,
      handler(newValue){
        localStorage.setItem('todos',JSON.stringify(newValue))
      }
    }
  }
};
</script>

<style></style>
