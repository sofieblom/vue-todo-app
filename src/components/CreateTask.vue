<template>
  <div class="add_container">
    <input
      type="text"
      v-model="newTodo"
      placeholder="Add new task"
      @keypress.enter="handleClick"
    />
    <button class="add_btn" v-on:click="handleClick">
      {{ buttonContent }}
    </button>
    <p class="empty_paragraph">{{ emtypInput }}</p>
  </div>
</template>

<script lang="ts">
import { Todo } from "@/models/Todo";
import { Vue } from "vue-class-component";
import { Prop } from "vue-property-decorator";

export default class CreateTask extends Vue {
  buttonContent = "Add";
  emtypInput = "";
  newTodo = "";
  newId = 0;

  @Prop() todolist!: Todo[];

  handleClick() {
    if (this.newTodo.length > 0) {
      this.newId = this.todolist.length + 1;
      this.$emit("addTodo", new Todo(this.newId, this.newTodo, false));
      this.newTodo = "";
    } else {
      this.emtypInput = "You have to write something";
    }
  }
}
</script>

<style lang="scss"></style>
