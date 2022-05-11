<template>
  <h1>{{ heading }}</h1>
  <div class="wrapper">
    <CreateTask :todolist="unfinishedTasks" @addTodo="handleAddTodo($event)" />

    <div class="todos_container">
      <h2>Unfinished tasks</h2>

      <ul>
        <ShowTasks
          v-for="(todo, i) in unfinishedTasks"
          :index="i"
          :todo="todo"
          :key="todo.id"
          @completed="moveToCompletedTask($event, i)"
          @remove="removeUnfinishedTask($event)"
        ></ShowTasks>
      </ul>
    </div>
    <div class="todos_container">
      <br />
      <h2>Completed tasks</h2>
      <ul>
        <ShowTasks
          v-for="(c, i) in completedTasks"
          :todo="c"
          :index="i"
          :key="c.id"
          @unfinished="moveToUnfinished($event, i)"
          @remove="removeCompletedTask($event)"
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
    new Todo(3, "städa badrummet", false),
    new Todo(4, "baka en god kaka", false),
  ];

  handleAddTodo(newTodo: Todo) {
    this.unfinishedTasks.push(newTodo);
  }

  moveToCompletedTask(todo: Todo, i: number) {
    this.completedTasks.push(todo);
    this.unfinishedTasks.splice(i, 1);
  }

  moveToUnfinished(todo: Todo, i: number) {
    this.unfinishedTasks.push(todo);
    this.completedTasks.splice(i, 1);
  }

  removeCompletedTask(i: number) {
    if (this.completed) {
      this.completedTasks.splice(i, 1);
    }
  }

  removeUnfinishedTask(i: number) {
    if (this.completed) {
      this.unfinishedTasks.splice(i, 1);
    }
  }
}
</script>
<style lang="scss"></style>
