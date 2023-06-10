<template>
  <div class="list-task">
    <h1>Todo List</h1>
    <div class="empty" v-if="taskEmpty">Belum ada task</div>
    <div v-else class="list-card">
      <div
        v-for="(task, index) of tasks"
        :key="index"
        class="list"
      >
        <input
          type="checkbox"
          name="status"
          id="task"
          :checked="task.isDone"
          @change="done(index)"
        />
        <div class="task">
          <div class="title" :class="{ coret: task.isDone }">
            {{ task.title }}
          </div>
          <div
            class="description"
            :class="{ coret: task.isDone }"
          >
            {{ task.description }}
          </div>
          <button @click="deleteTask(index)" class="btn-delete">Delete</button>
        </div>
      </div>
    </div>
    <div class="form">
      <a
        href="#"
        v-if="!isCreating"
        @click="isCreating = !isCreating"
        >Add Task</a
      >
      <div class="card" v-else>
        <input
          v-model="titleValue"
          placeholder="Title"
          type="text"
        />
        <textarea
          v-model="descriptionValue"
          placeholder="Description"
          rows="3"
        ></textarea>
        <div class="button">
          <button @click="addTask">Save</button>
          <button
            @click="isCreating = !isCreating"
          >
            Cancel
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
let taskEmpty = ref(true);
let isCreating = ref(false);
let titleValue = ref("");
let descriptionValue = ref("");
let tasks = reactive([
  {
    title: 'Belajar Javascript',
    description: 'Mantap Sekali Belajar Javascript ini',
    isDone: false
  }
]);

function addTask() {
  if (titleValue.value && descriptionValue.value) {
    tasks.push({
      title: titleValue.value,
      description: descriptionValue.value,
      isDone: false,
    });
    titleValue.value = "";
    descriptionValue.value = "";
    isCreating.value = false;
  }
}

function deleteTask(index) {
  tasks.splice(index, 1);
}

function done(index) {
  tasks[index].isDone = !tasks[index].isDone;
}

onMounted(() => {
  if (tasks.length > 0) {
    taskEmpty.value = false;
  } else {
    taskEmpty.value = true;
  }
})

onUpdated(() => {
  if (tasks.length > 0) {
    taskEmpty.value = false;
  } else {
    taskEmpty.value = true;
  }
});
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@200;300;400;500;600;700;800&display=swap");
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  width: 100%;
  font-family: "Montserrat", sans-serif;
  background-color: #2c3333;
}
.list-task {
  width: 60%;
  margin: auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: #2e4f4f;
  min-height: 400px;
}

.list-task h1 {
  color: #0e8388;
  font-size: 90px;
  font-weight: 700;
}

.empty {
  margin-top: 12px;
  font-size: 30px;
  color: #0e8388;
  font-weight: 300;
}

.form {
  margin-top: 30px;
  width: 80%;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 28px;
}

a {
  text-decoration: none;
  color: #0e8388;
  padding: 12px 18px;
  border-radius: 6px;
  background-color: #cbe4de;
}

.card {
  display: flex;
  flex-direction: column;
  width: 60%;
}

.card input {
  height: 36px;
  font-size: 16px;
  margin-bottom: 8px;
  padding: 3px;
  outline: none;
  color: #0e8388;
}

.card textarea {
  padding: 6px;
  height: 120px;
  font-size: 16px;
  margin-bottom: 8px;
  outline: none;
  color: #0e8388;
}

.button {
  display: flex;
  gap: 8px;
}

.button button {
  color: #0e8388;
  padding: 8px 12px;
  border-radius: 3px;
  border: none;
  background-color: #cbe4de;
}

.list {
  margin-top: 12px;
  display: flex;
  align-items: center;
  gap: 18px;
  padding: 24px;
  max-width: 100%;
  border: 1px solid #0e8388;
}

.list input {
  width: 24px;
  height: 24px;
  min-width: 32px;
}
.coret {
  text-decoration: line-through;
}

.title {
  color: #cbe4de;
  font-size: 24px;
  font-weight: 600;
  margin-bottom: 6px;
}

.description {
  color: #cbe4de;
  margin-bottom: 10px;
}

.btn-delete {
  color: #0e8388;
  padding: 4px 6px;
  border-radius: 2px;
  border: none;
  background-color: #cbe4de;
}

.task {
  margin: 12px 0;
}

.list-card {
  max-width: 80%;
}
</style>