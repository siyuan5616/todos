<template>
  <header class="header">
    <h1>todos</h1>
    <input
      class="new-todo"
      placeholder="请输入任务名称"
      v-model.trim="text"
      @keydown.enter="add"
      autofocus
    />
  </header>
</template>

<script>
export default {
  data() {
    return {
        text: "",
    };
  },
  methods: {
    add() {
        if(this.text==='')return alert('请输入完整内容')
        this.$emit('add',this.text)
        this.text=''
    },
  },
};
</script>

<style>
</style>