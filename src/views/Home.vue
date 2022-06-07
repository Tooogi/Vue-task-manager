<template>
  <div class="home">
    <h1>{{ title }}</h1>
    <form>
      <input type="text" v-model="task" placeholder="Add new task" />
      <input type="date" @blur="addTask()" v-model="due" />
    </form>
    <div class="row">
      <button class="toggle" @click="toggleCompleted()">
        Hide / Show Completed Tasks
      </button>
      <div class="column">
        Open Tasks: <button class="open">{{ OpenTasks }}</button> Overdue
        Tasks:<button class="close">{{ ClosedTasks }}</button>
      </div>
    </div>
    <ul>
      <li
        v-for="task in tasks"
        :key="task.id"
        :class="{ completed: task.completed }"
        v-show="!task.completed || (showCompleted && task.completed)"
      >
        <input
          type="checkbox"
          @click="changeCompleted(task.id)"
          :checked="task.completed"
        />
        {{ task.name }} - {{ task.due }}
      </li>
    </ul>
  </div>
</template>

<style scoped>
/* background-color: #25ad9d */
.completed {
  text-decoration: line-through;
  color: #25ad9d;
  border: 0;
}
h1 {
  background: #25ad9d;
  color: white;
  padding: 1rem;
  text-align: center;
}
.toggle {
  padding: 0.4rem;
  margin: 0.5rem;
  border: 0.15rem solid #cacaca;
  border-radius: 50px;
  background-color: white;
  cursor: pointer;
}
.toggle:hover {
  background: #25ad9d;
  color: white;
  transition: 0.5s;
}
.column {
  text-align: right;
}
.open,
.close {
  width: 50px;
  margin-left: 5px;
}
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  font-size: 1.5rem;
  color: #000;
}
li {
  margin: 1rem;
  position: relative;
  top: 0.5em;
  border-bottom: 1px solid #25ad9d;
  padding: 10px;
}
li:hover {
  background: #25ad9d;
  color: white;
  transition: 0.5s;
}
form {
  display: flex;
}
input[type="text"] {
  flex-grow: 3;
  font-size: 1.5rem;
  height: 2.5rem;
}
input[type="date"] {
  font-size: 1.5rem;
  height: 2.5rem;
}
</style>

<script>
// @ is an alias to /src

//import axios from "axios";

export default {
  name: "Home",

  data() {
    return {
      title: "Task Manager",
      showCompleted: true,
      due: new Date().toISOString().split("T")[0],
      task: " ",
      tasks: [
        {
          id: 1,
          name: "Test",
          completed: false,
          due: "2022-02-27",
        },
        {
          id: 2,
          name: "Learn C++",
          completed: false,
          due: "2023-01-27",
        },
        {
          id: 3,
          name: "Read The Lord of The Rings part 1",
          completed: true,
          due: "2022-02-10",
        },
        {
          id: 4,
          name: "Learn vue.js",
          completed: true,
          due: "2022-04-20",
        },
        {
          id: 5,
          name: "Learn React",
          completed: false,
          due: "2022-09-05",
        },
        {
          id: 6,
          name: "Setup backend for task manager",
          completed: false,
          due: "2022-07-01",
        },
      ],
    };
  },
  computed: {
    OpenTasks: function () {
      return this.tasks.filter((task) => !task.completed).length;
    },
    ClosedTasks: function () {
      return this.tasks.filter(
        (task) => !task.completed && task.due < new Date().toISOString()
      ).length;
    },
  },
  methods: {
    changeCompleted(id) {
      let task = this.tasks.find((task) => task.id == id);
      task.completed = !task.completed;
    },
    /*addTask() {
      const task = {
        name: this.task,
        due: this.due,
        completed: false,
      };
    },*/
    toggleCompleted() {
      this.showCompleted = !this.showCompleted;
    },
  },
};
</script>
