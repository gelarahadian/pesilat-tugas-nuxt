<template>
  <div class="list-task">
    <h1>Todo List</h1>
    <h2 v-if="tasks.length === 0">Belum ada task</h2>
    <div
      v-for="task of tasks"
      :key="task.id"
      class="item-task d-flex align-items-start border-bottom pt-3 pb-4"
    >
      <input
        type="checkbox"
        name="status"
        id="task"
        class="me-2 mt-2"
        :checked="task.isDone"
        @click="editTaskIsDone(task.id)"
      />
      <div class="d-flex flex-column">
        <div
          class="title-task mb-1 text-decoration-line-through"
          :style="task.isDone ? { textDecoration: 'line-through' } : {}"
        >
          {{ task.title }}
        </div>
        <div class="description-task small text-muted">
          {{ task.description }}
        </div>
        <button class="btn btn-danger" @click="deleteTask(task.id)">
          Delete
        </button>
      </div>
    </div>
  </div>
  <div class="action py-2">
    <a href="#" class="add-button" @click="addTaskToggle" v-if="!isCreating"
      >Add Task</a
    >
    <div v-if="isCreating" class="add-card">
      <div class="card mb-2">
        <div class="card-body d-flex flex-column p-0">
          <input
            class="form-control border-0 mb-2"
            placeholder="Title"
            type="text"
            v-model="titleValue"
          />
          <textarea
            class="form-control border-0 small"
            placeholder="Description"
            rows="3"
            v-model="descriptionValue"
          ></textarea>
        </div>
      </div>
      <div class="button-wrapper d-flex">
        <button class="btn btn-primary me-2" @click="addTask">Save</button>
        <button class="btn btn-outline-secondary" @click="addTaskToggle">
          Cancel
        </button>
      </div>
    </div>
  </div>
</template>
<script>
import "bootstrap/dist/css/bootstrap.css";
import "bootstrap-vue/dist/bootstrap-vue.css";
export default {
  data() {
    return {
      tasks: [],
      isCreating: false,
      titleValue: "",
      descriptionValue: "",
    };
  },
  methods: {
    addTaskToggle() {
      this.isCreating = !this.isCreating;
    },
    addTask() {
      console.log(this.titleValue, this.descriptionValue);
      this.tasks.push({
        id: this.tasks.length + 1,
        title: this.titleValue,
        description: this.descriptionValue,
        isDone: true,
      });
      (this.titleValue = ""), (this.descriptionValue = "");
    },
    deleteTask(id) {
      const deleteTask = this.tasks.filter((task) => {
        return task.id !== id;
      });
      this.tasks = deleteTask;
    },
    editTaskIsDone(id) {
      this.tasks.map((task) => {
        if (task.id === id) {
          task.isDone = !task.isDone;
        }
        return task;
      });
    },
  },
};
</script>
