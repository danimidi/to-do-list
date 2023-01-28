<template>
  <div class="container">
    <h1 class="title">Mi App de Tareas</h1>
    <!-- Task creation and update section -->
    <task-creator
      v-model:task="task"
      :isEditing="isEditing"
      @submitTask="submitTask"
    />
    <!-- available task list -->
    <div class="taskList" v-if="!!taskList.length">
      <task-item
        v-for="(task, index) in taskList"
        :key="index"
        :task="task"
        :index="index"
        @completeTask="completeTask(task, index)"
        @editTask="editTask(task, index)"
        @deleteTask="deleteTask(index)"
      />
    </div>
    <!-- if there is no task show this message -->
    <p class="no-tasks" v-else>Sin tareas</p>
  </div>
</template>

<script>
import taskItem from "./components/taskItem.vue";
import taskCreator from "./components/taskCreator.vue";

export default {
  name: "App",
  components: { taskItem, taskCreator },
  data() {
    return {
      //Defines the task description
      task: "",
      //Indicates if a task is being edited
      isEditing: false,
      //Defines the index of a specific task
      selectedIndex: null,
      //Defines the task list
      taskList: [],
    };
  },
  mounted() {
    //assigns the information in localStorage to the taskList variable
    const tasks = JSON.parse(localStorage.getItem("taskList"));
    if (Array.isArray(tasks)) {
      this.taskList = tasks;
    }
  },
  methods: {
    //clear primary variable values
    clear() {
      this.isEditing = false;
      this.selectedIndex = null;
      this.task = "";
    },
    //save task list in localStorage
    save() {
      localStorage.setItem("taskList", JSON.stringify(this.taskList));
    },
    //create a new Task or update an existing task
    submitTask() {
      if (!this.task) return;
      if (this.isEditing) {
        this.taskList[this.selectedIndex].description = this.task;
      } else {
        this.taskList.push({ description: this.task, isCompleted: false });
      }
      this.clear();
      this.save();
    },
    //enable editing of a task
    editTask(task, index) {
      this.isEditing = true;
      this.selectedIndex = index;
      this.task = task.description;
    },
    //remove a task from taskList
    deleteTask(index) {
      this.taskList.splice(index, 1);
      this.clear();
      this.save();
    },
    //change the isCompleted attribute of the task
    completeTask(task, index) {
      this.taskList[index].isCompleted = !task.isCompleted;
      this.save();
    },
  },
};
</script>

<style>
:root {
  --primary-color: #28847e;
  --secondary-color: #3cbbb2;
  --light-green: #d4f2ef;
}
html {
  margin: 0px;
  padding: 0px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  background-color: var(--light-green);
}
.container {
  padding: 0 14px;
  max-width: 1320px;
  margin: 0 auto;
}
.title {
  margin-top: 60px;
  text-align: center;
}
.taskList {
  width: 100%;
  margin-top: 40px;
}
.no-tasks {
  margin-top: 80px;
  text-align: center;
  opacity: 80%;
}

@media (min-width: 640px) {
  .container {
    padding: 0 32px;
  }
  .title {
    text-align: left;
  }
}
</style>
