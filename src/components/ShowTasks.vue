<template>
  <li @click="completeTask">
    {{ todo.title }}
  </li>
</template>

<script lang="ts">
import { Todo } from "@/models/Todo";
import { Vue } from "vue-class-component";
import { Prop } from "vue-property-decorator";

export default class ShowTasks extends Vue {
  @Prop() todo!: Todo;
  @Prop() completedTasks!: Todo[];
  @Prop() index!: number;

  completeTask() {
    this.todo.completed = !this.todo.completed;
    if (this.todo.completed) {
      this.completedTasks.push(this.todo);
      this.$emit("completed", this.todo, this.index);
    }
    console.log(this.todo.completed);
  }
}
</script>

<style lang="scss"></style>
