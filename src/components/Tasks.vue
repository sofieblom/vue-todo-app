<template>
  <h1>{{ heading }}</h1>
  <div class="wrapper">
    <CreateTask :todolist="unfinishedTasks" @addTodo="handleAddTodo($event)" />

    <div class="todos_container">
      <ul>
        <ShowTasks
          v-for="(todo, i) in unfinishedTasks"
          :index="i"
          :todo="todo"
          :key="todo.id"
          :completedTasks="completedTasks"
          @completed="removeUnfinishedTodo($event, i)"
        ></ShowTasks>
      </ul>

      <br />
      <h2>Completed tasks</h2>
      <ul>
        <ShowTasks
          :class="'active'"
          v-for="c in completedTasks"
          :todo="c"
          :key="c.id"
          :completedTasks="completedTasks"
        ></ShowTasks>
      </ul>
    </div>
  </div>
</template>
<script lang="ts">
import { Todo } from "@/models/Todo";
import { Options, Vue } from "vue-class-component";
import CreateTask from "./CreateTask.vue";
import ShowTasks from "./ShowTasks.vue";

@Options({
  components: {
    ShowTasks,
    CreateTask,
  },
})
export default class Tasks extends Vue {
  heading = "What's left to do ?";
  completed = true;

  completedTasks: Todo[] = [];
  unfinishedTasks: Todo[] = [
    new Todo(0, "handla", false),
    new Todo(1, "springa", false),
    new Todo(2, "dricka kaffe", false),
  ];

  handleAddTodo(newTodo: Todo) {
    this.unfinishedTasks.push(newTodo);
  }

  removeUnfinishedTodo(completedTask: Todo, i: number) {
    console.log("fubka rå");
    this.unfinishedTasks.splice(i, 1);
  }
}
</script>
<style lang="scss"></style>
