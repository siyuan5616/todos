<template>
  <div>
    <footer class="footer">
      <span class="todo-count"
        ><strong>{{ leftCount }}</strong
        >剩余</span
      >
      <ul class="filters">
        <li>
          <a
            :class="{ selected: falg }"
            @click.prevent="falg === 'all'"
            href="#/"
            >全部</a
          >
        </li>
        <li>
          <a
            :class="{ selected: falg }"
            @click.prevent="filter('no')"
            href="#/active"
            >进行中</a
          >
        </li>
        <li>
          <a
            :class="{ selected: falg }"
            @click.prevent="filter('yes')"
            href="#/completed"
            >已完成</a
          >
        </li>
      </ul>
      <button class="clear-completed" v-show="isShowClear" @click="clear">
        清除已完成
      </button>
    </footer>
  </div>
</template>

<script>
export default {
  props: {
    list: {
      type: Array,
      equired: true,
    },
    falg:{
        type:String
    }
  },
  methods: {
    clear() {
      //清楚已完成
      this.$emit("clear");
    },
    filter(type){
        //底部过滤
        this.$emit('filter',type)
    }
  },
  computed: {
    leftCount() {
      //剩余任务统计
      return this.list.filter((item) => item.isDone === false).length;
    },
    isShowClear() {
      //清楚已完成显示
      return this.list.some((item) => item.isDone === true);
    },
  },
};
</script>

<style>
</style>