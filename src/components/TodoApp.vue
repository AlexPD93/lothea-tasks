<script>
export default {
  data() {
    return {
      task: "",
      priority: 1,
      tasks: [
        {
          name: "Feed cat",
          priority: 2,
        },
        {
          name: "Take out rubbish",
          priority: 8,
        },
        {
          name: "Buy mum's birthday present",
          priority: 1,
        },
      ],
    };
  },

  methods: {
    submitTask(e) {
      if (this.task.length === 0) return;
      if (this.priority < 1 || this.priority > 10) return;

      this.tasks.push({
        name: this.task,
        priority: this.priority,
      });
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
    <ul>
      <li v-for="item of tasks">{{ item.name }} {{ item.priority }}</li>
    </ul>
  </div>
</template>

<!-- Expected Behaviours: - The ability to add a new task, with a priority of between
1-10. - The ability to view a list of all the tasks - The ability to order the
tasks by priority or the order they were added to the list - The ability to
delete a task - (Optional) The ability to filter to tasks below a certain
priority (e.g. display only tasks with a priority below 3) You may add
additional features if you have the time. -->
<style scoped></style>
