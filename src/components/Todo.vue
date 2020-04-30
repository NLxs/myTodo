<template>
    <li class="d-flex align-items-center list-group-item">
    <!-- todo 内容 -->
    <button
      class="btn border-0 flex-grow-1 text-left shadow-none"
      :class="{ completed }"
      @click="$emit('on-toggle')"
      v-if="!isEditing"
      >
      <span>{{ description }}</span>
    </button>
    <!-- 编辑内容 -->
    <form v-else class="flex-grow-1" @submit.prevent="finishEditing()">
      <!-- @blur="finishEditing()" 失去鼠标焦点, 执行finishEditing() -->
      <input 
        type="text"
        class="form-control"
        v-model="newTodoDescription"
        @blur="finishEditing()"
        ref="newTodo"
      />
    </form>
    <!-- 编辑 -->
    <button 
      @click="startEditing()"
      class="btn btn-outline-primary border-0 ml-2"
    >
      <span class="fa fa-edit"></span>
    </button>
    <!-- 删除 -->
    <button 
      @click="$emit('on-delete')"
      class="btn btn-outline-danger border-0"
    >
      <span class="fa fa-trash"></span>
    </button>
  </li>
</template>

<script>
  export default {
    name: 'Todo',
    props: {
      description: String,
      completed: Boolean
    },
    data() {
      return {
        isEditing: false,
        newTodoDescription: ""
      };
    },
    methods: {
      startEditing() {
        if(this.isEditing) {
          this.finishEditing();
        } else {
          this.newTodoDescription = this.description;
          this.isEditing = true;
          this.$nextTick(() => this.$refs.newTodo.focus());
        }
      },
      finishEditing() {
        this.isEditing = false;
        this.$emit("on-edit", this.newTodoDescription);
      }
    }
  };
</script>

<style lang="scss" scoped>
/* 标记todo为已完成 */
.completed {
  text-decoration: line-through;
}
</style>