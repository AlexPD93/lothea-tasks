<script>
import { ref } from "vue";

export default {
  data() {
    return {
      task: "",
      priority: 1,
      count: 3,
      tasks: [
        {
          name: "Feed cat",
          priority: 2,
          id: 1,
          shown: true,
        },
        {
          name: "Take out rubbish",
          priority: 8,
          id: 2,
          shown: true,
        },
        {
          name: "Buy mum's birthday present",
          priority: 1,
          id: 3,
          shown: true,
        },
      ],
    };
  },

  methods: {
    submitTask() {
      if (this.task.length === 0) return;
      if (this.priority < 1 || this.priority > 10) return;
      this.count++;

      this.tasks.push({
        name: this.task,
        priority: this.priority,
        id: this.count,
        shown: true,
      });
    },
    orderNumerically(e) {
      const sortedArray = this.tasks.sort((a, b) => a.priority - b.priority);

      this.tasks = sortedArray;
    },
    orderWhenAdded() {
      // Revert array back to what is was before
      const sortById = this.tasks.sort((a, b) => a.id - b.id);
      this.tasks = sortById;
    },
    deleteTask(e) {
      const indexOfObject = this.tasks.findIndex((object) => {
        return object.id === Number(e.target.id);
      });
      this.tasks.splice(indexOfObject, 1);
    },
  },
};
</script>

<template>
  <div id="container">
    <h1>My Vue Todo App</h1>
    <div id="button">
      <label for="task">Type a task</label>
      <input v-model="task" id="task" type="text" placeholder="Enter task" />
      <label for="priority">Urgency (1 most urgent, 10 least urgent) </label>
      <input v-model="priority" id="priority" type="number" min="1" max="10" />
      <button @click="submitTask" type="submit">Create task</button>
    </div>
    <button @click="orderNumerically">Sort by priority</button>
    <button @click="orderWhenAdded">Sort by when added</button>
    <ul>
      <li v-for="item of tasks">
        {{ item.name }}
        <button v-bind:id="item.id" @click="deleteTask">X</button>
      </li>
    </ul>
  </div>
</template>

<!--
(Optional) The ability to filter to tasks below a certain
priority (e.g. display only tasks with a priority below 3) You may add
additional features if you have the time. -->
<style scoped></style>
