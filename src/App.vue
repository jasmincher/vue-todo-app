<template>
  <div>
    <TodoInput @keyup.enter="add" />
    <button @click="add" id="add-item-btn">Submit</button>

    <ul>
      <TodoItem
        v-for="item in tasks"
        v-bind:key="item.id"
        :task="item.name"
        v-model="newTask"
        @deleteTask="deleteTask(item)"
        @click="toggleDone(item)"
        :strikethrough="{ done: item.isDone }"
        :check="[item.isDone ? 'checked' : 'unchecked']"
      />
    </ul>
  </div>
</template>

<script>
import TodoInput from "./components/TodoInput.vue";
import TodoItem from "./components/TodoItem.vue";

export default {
  name: "App",
  components: {
    TodoInput,
    TodoItem,
  },

  data() {
    return {
      tasks: [],
      newTask: String,
      index: 0,
      isDone: false,
      checked: "unchecked",
    };
  },
  methods: {
    //function that will create a new tasks based on the input the user types in 
    add() {
      let taskValue = document.getElementById("todo-input").value;

      // will only create a task if input is not empty
      if (taskValue != "") {
        this.newTask = taskValue;
        //creating a name, id, and isDone values to unique identify each task
        this.tasks.push({
          name: this.newTask,
          id: this.index++,
          isDone: this.isDone,
        });
      }


      //setting the input to blank after user creates a task
      document.getElementById("todo-input").value = "";
    },

    //function will delete the task that is clicked on
    deleteTask(item) {
      // in order to delete an item, tasks array will now be filtered 
      //without the item that is chosen
      this.tasks = this.tasks.filter((newTask) => newTask.id !== item.id);
    },

    //function will toggle isDone boolean between true and false
    toggleDone(item) {
      item.isDone = !item.isDone;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

#add-item-btn {
}

.done {
  text-decoration: line-through;
}

.unchecked {
  position: absolute;
  left: 10px;
  font-size: 30px;
  color: gray;
  font-weight: bolder;
}

.unchecked:hover {
  color: rgb(124, 189, 124);
}

.checked {
  color: rgb(124, 189, 124);
  position: absolute;
  left: 10px;
  font-size: 30px;
  font-weight: bolder;
}

li,
li button {
  cursor: pointer;
}
</style>
