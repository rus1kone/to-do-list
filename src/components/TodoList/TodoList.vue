<template>
  <div class="todo-list">
    <h1>Список задач</h1>
    <input
      type="text"
      placeholder="Поиск..."
      v-model="searchText"
      class="search-input"
    />

    <div class="task-list-container">
      <ul class="task-list">
        <li v-for="task in filteredTasks" :key="task.id" class="task-item">
          <label :class="{ completed: task.completed }">
            <input type="checkbox" v-model="task.completed" />
            {{ task.title }}
          </label>
          <button class="delete-button" @click="deleteTask(task.id)">
            Удалить
          </button>
        </li>
      </ul>
    </div>

    <form class="add-task-form" @submit.prevent="addTask">
      <input
        type="text"
        placeholder="Добавить задачу..."
        v-model="newTaskText"
      />
      <button type="submit">Добавить</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [
        { id: 1, title: "Купить продукты", completed: false },
        { id: 2, title: "Выгулять собаку", completed: false },
        { id: 3, title: "Закончить проект", completed: false },
      ],
      searchText: "",
      newTaskText: "",
    };
  },
  computed: {
    filteredTasks() {
      const searchQuery = this.searchText.toLowerCase();
      return this.tasks.filter((task) =>
        task.title.toLowerCase().includes(searchQuery)
      );
    },
  },
  methods: {
    addTask() {
      if (this.newTaskText.trim() !== "") {
        const newTask = {
          id: Date.now(),
          title: this.newTaskText.trim(),
          completed: false,
        };
        this.tasks.push(newTask);
        this.newTaskText = "";
      }
    },
    deleteTask(taskId) {
      this.tasks = this.tasks.filter((task) => task.id !== taskId);
    },
  },
};
</script>

<style scoped>
.todo-list {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  font-family: "Arial", sans-serif;
}

.todo-list h1 {
  text-align: center;
  font-size: 28px;
  color: #333;
}

.search-input {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.task-list-container {
  max-height: 200px;
  overflow-y: auto;
  background-color: #f9f9f9;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.task-list {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.task-item {
  display: flex;
  align-items: center;
  padding: 10px;
  border-bottom: 1px solid #eee;
  transition: background-color 0.3s;
}

.task-item:last-child {
  border-bottom: none;
}

.task-item:hover {
  background-color: #f5f5f5;
}

.task-item label {
  flex-grow: 1;
  display: flex;
  align-items: center;
  font-size: 16px;
  cursor: pointer;
}

.task-item label input {
  margin-right: 10px;
}

.completed label {
  text-decoration: line-through;
  color: #999;
}

.delete-button {
  background-color: #ff6b6b;
  border: none;
  color: #fff;
  padding: 5px 10px;
  margin-left: 10px;
  font-size: 14px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.delete-button:hover {
  background-color: #ff5252;
}

.add-task-form {
  display: flex;
  margin-top: 10px;
}

.add-task-form input[type="text"] {
  flex-grow: 1;
  padding: 10px;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.add-task-form button {
  background-color: #4caf50;
  border: none;
  color: #fff;
  padding: 10px 20px;
  margin-left: 10px;
  font-size: 16px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.add-task-form button:hover {
  background-color: #45a049;
}

.completed {
  background-color: #f1f1f1;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: background-color 0.3s;
}

.completed:hover {
  background-color: #eee;
}
</style>
