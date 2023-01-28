<template>
  <div class="task">
    <!-- task details -->
    <label class="task-details">
      <input
        type="checkbox"
        :checked="task.isCompleted"
        @click="completeTask"
      />
      <span> {{ task.description }} </span>
    </label>
    <!-- actions available for the task -->
    <div class="task-actions">
      <icon-button class="edit-task" @click="editTask">
        <PencilSquareIcon class="h-6 w-6" />
      </icon-button>
      <icon-button @click="deleteTask">
        <TrashIcon class="h-6 w-6" />
      </icon-button>
    </div>
  </div>
</template>

<script>
import { PencilSquareIcon, TrashIcon } from "@heroicons/vue/24/solid";
import iconButton from "./global/iconButton.vue";

export default {
  name: "task-item",
  components: { iconButton, PencilSquareIcon, TrashIcon },
  props: {
    task: { description: String, isCompleted: Boolean },
    index: Number,
  },
  methods: {
    completeTask() {
      this.$emit("completeTask");
    },
    editTask() {
      this.$emit("editTask");
    },
    deleteTask() {
      this.$emit("deleteTask");
    },
  },
};
</script>

<style scoped>
.task {
  min-height: 54px;
  display: flex;
  align-items: center;
  background-color: rgba(255, 255, 255, 0.6);
  border-radius: 8px;
  padding: 6px;
  margin-bottom: 12px;
}
.task:hover {
  background-color: rgba(255, 255, 255, 1);
}
.task-details {
  width: 100%;
  display: flex;
  align-items: center;
}
.task-details input {
  height: 15px;
  min-width: 15px;
  margin-right: 8px;
  appearance: none;
  border: 2px solid var(--primary-color);
  border-radius: 2px;
  cursor: pointer;
}
.task-details input:checked {
  background-color: var(--primary-color);
  background-image: url("../assets/checkIcon.svg");
  background-repeat: no-repeat;
  background-position: center;
}
.task-details input:checked + span {
  text-decoration: line-through;
  color: #696f75;
  opacity: 80%;
}
.task-actions {
  min-width: fit-content;
}

@media (min-width: 640px) {
  .edit-task {
    margin-right: 12px;
  }
}
</style>
