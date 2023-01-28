<template>
  <div class="create-task-container">
    <input
      class="task-input"
      placeholder="Agrega una tarea nueva"
      :value="task"
      @input="input"
      @keyup.enter="submitTask"
    />
    <button class="submit-task" type="button" @click="submitTask">
      {{ buttonLabel }}
    </button>
  </div>
</template>

<script>
export default {
  name: "task-creator",
  props: { task: String, isEditing: Boolean },
  methods: {
    input(e) {
      this.$emit("update:task", e.target.value);
    },
    submitTask() {
      this.$emit("submitTask");
    },
  },
  computed: {
    //change button label based on isEditing variable
    buttonLabel() {
      return this.isEditing ? "Actualizar" : "Crear";
    },
  },
};
</script>

<style scoped>
.create-task-container {
  margin-top: 50px;
  display: flex;
}
.task-input {
  width: 100%;
  outline: none;
  border: none;
  border-bottom: 1px solid var(--primary-color);
  background-color: transparent;
  margin-right: 10px;
}
.submit-task {
  height: 32px;
  padding: 0 10px;
  border-radius: 8px;
  cursor: pointer;
  background-color: var(--primary-color);
  border: none;
  color: white;
}
.submit-task:hover {
  background-color: var(--secondary-color);
}

@media (min-width: 640px) {
  .submit-task {
    min-width: 100px;
  }
}
</style>
