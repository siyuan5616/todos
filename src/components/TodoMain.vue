<template>
  <div>
    <section class="main">
      <input id="toggle-all" class="toggle-all" type="checkbox" v-model="isAll"/>
      <label for="toggle-all">Mark all as complete</label>
      <ul class="todo-list">
        <!-- 当任务已完成，可以给 li 加上 completed 类，会让元素加上删除线 -->
        <li
          :class="{ completed: item.isDone }"
          v-for="item in list"
          :key="item.id"
        >
          <div class="view">
            <input class="toggle" type="checkbox" :checked="item.isDone" @click="changeis(item.id)" />
            <label>{{ item.name }}</label>
            <button class="destroy" @click="del(item.id)"></button>
          </div>
        </li>
        <!-- <li>
          <div class="view">
            <input class="toggle" type="checkbox" />
            <label>行万里路</label>
            <button class="destroy"></button>
          </div>
        </li> -->
      </ul>
    </section>
  </div>
</template>

<script>


export default {
  props: {
    list: {
      type: Array,
      equired: true,
    },
  },
  methods: {
    //删除功能
    del(id) {
      this.$emit("del", id);
    },
    //单个状态修改
    changeis(id){
        this.$emit('changeis',id)
    }
  },
  computed:{
    isAll:{
        get(){
            return this.list.every(item => item.isDone===true)
        },
        set(value){
            this.$emit('isAll',value)
        }
    }
  }
};
</script>

<style>
</style>