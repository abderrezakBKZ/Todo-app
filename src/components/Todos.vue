<template>
  <v-app>
    <v-container>
      <p class="text-h4 my-5 text-center">Todo App</p>
      <v-text-field
        label="Task"
        placeholder="insert Task here"
        task
        :value="task.title"
        v-model="task.title"
        @insert="task.title"
        class="mb-3"
        @keyup.enter="addTask"
      ></v-text-field>
      <v-btn color="primary" @click="addTask"> add task</v-btn>

      <v-card class="mt-8">
        <v-list dense>
          <v-subheader class="text-body-2 mb-1">List of tasks</v-subheader>
          <v-list-item-group color="primary">
            <v-list-item v-for="(t, index) of tasks" :key="index">
              <v-checkbox name="succes" v-model="t.checked"></v-checkbox>
              <v-list-item-content>
                <v-list-item-title
                  :class="[
                    !t.checked
                      ? 'text-body-1 font-weight-regular'
                      : 'font-weight-regular text-body-1 text-decoration-line-through',
                  ]"
                >
                  {{ t.title }}
                </v-list-item-title>
              </v-list-item-content>
              <v-list-item-icon>
                <v-icon large color="error" @click="deleteTask(index)">{{
                  icons.mdiDelete
                }}</v-icon>
              </v-list-item-icon>
            </v-list-item>
          </v-list-item-group>
        </v-list>
      </v-card>

      <div class="text-center mt-5">
        <v-btn color="primary" class="mx-3" @click="checkAllTask()"
          >Check all tasks</v-btn
        >
        <v-btn color="error" class="mx-3" @click="deleteAllTasks()"
          >Remove all tasks</v-btn
        >
      </div>
    </v-container>
  </v-app>
</template>

<script>
import { mdiDelete } from "@mdi/js";
export default {
  name: "Todos",

  data: () => {
    return {
      task: {
        title: "",
        checked: false,
      },
      tasks: [],
      icons: {
        mdiDelete,
      },
    };
  },
  methods: {
    addTask() {
      if (!this.task.title) return;
      this.tasks.push(this.task);
      this.task = {
        title: "",
        checked: false,
      };
    },

    deleteTask(index) {
      return this.tasks.splice(index, 1);
    },
    deleteAllTasks() {
      return (this.tasks = []);
    },
    checkTask(index) {
      return this.tasks.push(this.tasks.splice(index, 1)[0]);
    },
    checkAllTask() {
      return this.tasks.map((t) => {
        return (t.checked = true);
      });
    },
  },
};
</script>
