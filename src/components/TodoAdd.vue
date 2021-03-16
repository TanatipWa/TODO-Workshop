<template>
  <v-container>
    <!-- Todo Add -->
    <v-row>
      <v-col cols="10">
        <v-text-field
          name="name"
          label="Task"
          id="id"
          @keyup.enter="addTask"
          v-model="taskTextField"
        ></v-text-field>
      </v-col>

      <v-col cols="2">
        <v-btn block color="success" @click="addTask">ADD</v-btn>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import { v4 as uuidv4 } from 'uuid';
export default {
  name: "TodoAdd",
  methods: {
    addTask() {
      let task = {
          id: uuidv4(),
          title: this.taskTextField,
          completed: false
      }

      this.$emit("onSubmit", task);
      this.taskTextField = "";
    },
  },
  data() {
    return {
      taskTextField: "",
    };
  },
};
</script>

<style></style>
