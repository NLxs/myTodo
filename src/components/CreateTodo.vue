<template>
  <form class="col-12 col-sm-10 col-md-8 cl-lg-6" @submit.prevent="addTodo()">
    <input 
      type="text" 
      v-model="newTodo"
      class="form-control"
      placeholder="今日任务"
    />
  </form>
</template>

<script>
  export default {
    name: 'CreateTodo',
    data() {
      return {
        newTodo: ""
      };
    },
    methods: {
      addTodo() {
        if(this.newTodo.length > 0) {
          this.$emit("on-new-todo", this.newTodo);
        }
        this.newTodo = ""
      }
    }
  }
</script>

<style lang="" scoped>
  
</style>