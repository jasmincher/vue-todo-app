<template>
  <li>
    <span class="material-icons" :class="check ? 'checked' : 'unchecked'">done</span>
    <p :class="{done: check } ">
      {{ task }}
    </p>
    <button @click="deleteTask" class="delete-btn">Delete</button>
  </li>
</template>

<script>
export default {
  name: "TodoItem",
  props: {
    task: String,
    check: String,
  },
  methods: {
      //this will allow us to use the deleteTask function in 
      //the parent component
    deleteTask() {
      this.$emit("deleteTask");
    },
  },
};
</script>


<style scoped>
li {
  list-style-type: none;
  border: 1px solid rgb(162, 162, 162);
  display: flex;
  position: relative;
  height: 40px;
  width: 500px;
  margin: 10px;
  align-items: center;
  justify-content: center;
  border-radius: 5px;
}


li,
li button {
  cursor: pointer;
}


.delete-btn {
  position: absolute;
  right: 0;
  background: rgb(210, 99, 99);
  color: white;
  height: 40px;
  padding: 10px;
  border: none;
}

.delete-btn:hover {
  background: rgb(230, 108, 108);
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


.done {
  text-decoration: line-through;
}

.checked {
  color: rgb(124, 189, 124);
  position: absolute;
  left: 10px;
  font-size: 30px;
  font-weight: bolder;
}
</style>