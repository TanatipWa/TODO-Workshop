<template>
  <div class="home">
    <v-container>
      <TodoAdd @onSubmit="addTask" />
      <TodoList @onRemove="removeTask" :todos="todos | reverse" />

      <V-row class="d-flex flex-row justify-content-center align-center">
        <v-img
          class="mt-10"
          contain
          maxHeight="200"
          src="https://todolist.london/wp-content/uploads/2020/01/To-Do-List-Logo-for-Facebook.jpg"
        />
      </V-row>
    </v-container>
  </div>
</template>

<script>
// @ is an alias to /src
import TodoList from "@/components/TodoList.vue";
import TodoAdd from "@/components/TodoAdd.vue";
import axios from "axios";

export default {
  name: "Home",
  computed: {
    reversedTodo() {
      return this.todos.slice().reverse();
    },
  },
  filters: {
    reverse(value) {
      return value.slice().reverse();
    },
  },
  components: {
    TodoList,
    TodoAdd,
  },
  async mounted() {
    let result = await axios.get("https://jsonplaceholder.typicode.com/todos");
    this.todos = result.data;
  },
  methods: {
    async addTask(task) {
      let result = await axios.post(
        "https://jsonplaceholder.typicode.com/todos",
        task
      );
      //alert(JSON.stringify(result.data))
      this.todos.push(result.data);
    },
    removeTask(id) {
      axios
        .delete("https://jsonplaceholder.typicode.com/todos/" + id)
        .then((result) => {
          console.log(JSON.stringify(result.data))
          this.todos = this.todos.filter((item) => item.id !== id);
        })
        .catch(error => {
          console.log(error)
        });
    },
  },
  data() {
    return {
      todos: [],
      todos_mockup: [
        { id: 1, title: "Task 1", completed: false },
        { id: 2, title: "Task 2", completed: true },
        { id: 3, title: "Task 3", completed: false },
      ],
    };
  },
};
</script>
