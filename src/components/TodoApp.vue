<script>
import { ref } from "vue";

export default {
  data() {
    return {
      task: "",
      priority: 1,
      tasks: [
        {
          name: "Feed cat",
          priority: 2,
          id: 1,
        },
        {
          name: "Take out rubbish",
          priority: 8,
          id: 2,
        },
        {
          name: "Buy mum's birthday present",
          priority: 1,
          id: 3,
        },
      ],
    };
  },

  methods: {
    submitTask() {
      if (this.task.length === 0) return;
      if (this.priority < 1 || this.priority > 10) return;

      this.tasks.push({
        name: this.task,
        priority: this.priority,
        id: this.tasks[this.tasks.length - 2].id + 1,
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
      <li v-for="item of tasks">{{ item.name }}</li>
    </ul>
  </div>
</template>

<!--
 The ability to order the tasks by priority or the order they were added to the list - The ability to delete a task - 
(Optional) The ability to filter to tasks below a certain
priority (e.g. display only tasks with a priority below 3) You may add
additional features if you have the time. -->
<style scoped></style>
