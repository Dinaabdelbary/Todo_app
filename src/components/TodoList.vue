<template>
  <div class="container">
    <h1 class="text-center mt-5">{{ text }}</h1>

    <div class="d-flex">
      <input
        v-model="task"
        type="text"
        placeholder="Enter task"
        class="form-control"
      />
      <button @click="addTask()" class="btn btn-outline-info rounded-0">
        Submit
      </button>
    </div>

    <h4 class="text-center mt-3">
      You've got ({{ totalNumber - NumberOfCompletedTasks }}) tasks left
    </h4>
    <table class="table text-center mt-3 table-hover table-bordered">
      <thead>
        <tr>
          <th scope="col">Total: {{ totalNumber }}</th>
          <th scope="col">Task name</th>
          <th scope="col">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in tasks" :key="index">
          <td><input v-model="item.completed" type="checkbox" /></td>
          <td>{{ item.name }}</td>
          <td>
            <button @click="deleteTask(index)" class="btn btn-outline-danger">
            x
            </button>
          </td>
        </tr>
      </tbody>
    </table>
    <div class="notasks" v-if="tasks.length === 0">No tasks here, please create new one</div>
  </div>
</template>

<script>
export default {
  name: "TodoApp",
  props: {
    text: String,
  },
  computed: {
    totalNumber() {
      return this.tasks.length;
    },
    NumberOfCompletedTasks() {
      return this.tasks.filter((task) => task.completed).length;
    },
  },
  data() {
    return {
      task: "",
      tasks: [
        {
          name: "Task 1",
        },
        {
          name: "Task 2",
        },
        {
          name: "Task 3",
        },
      ],
    };
  },
  methods: {
    addTask() {
      if (this.task.length === 0) {
        alert("Please add a task.");
        return;
      }
      console.log(this.task);

      this.tasks.push({
        name: this.task,
        // completed: false,
      });
      this.task = "";
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
  },
};
</script>

<style scoped>
h1, h4, th{
  color: gray;
  font-family: sans-serif;
}



.notasks{
  color: red;
}

template{
  background-color: red ;
}
</style>
