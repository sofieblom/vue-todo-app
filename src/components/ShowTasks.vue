<template>
  <li>
    <span @click="completeTask">{{ todo.title }}</span>
    <span @click="removeTask">&times;</span>
  </li>
</template>

<script lang="ts">
import { Todo } from "@/models/Todo";
import { Vue } from "vue-class-component";
import { Prop } from "vue-property-decorator";

export default class ShowTasks extends Vue {
  @Prop() todo!: Todo;
  @Prop() index!: number;

  completeTask() {
    this.todo.completed = !this.todo.completed;
    if (this.todo.completed) {
      this.$emit("completed", this.todo, this.index);
    } else {
      this.$emit("unfinished", this.todo, this.index);
    }
    console.log(this.todo.completed);
  }
  removeTask() {
    this.$emit("remove", this.index);
  }
}
</script>

<style lang="scss"></style>
