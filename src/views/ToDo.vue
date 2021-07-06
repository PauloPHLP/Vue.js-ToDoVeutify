<template>
  <div class="home">
    <v-text-field
      v-model="newTaskTitle"
      @click:append="addTask"
      @keyup.enter="addTask"
      class="pa-3"
      outlined
      label="Add a new task"
      append-icon="mdi-plus"
      hide-details
      clearable
    ></v-text-field>
    <v-list
      class="pt-0"
      flat
    >
      <div v-for="task in tasks" :key="task.id">
        <v-list-item @click="task.id" :class="{ 'blue lighten-5': task.done }">
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox
                :input-value="task.done"
                color="primary"
              ></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                :class="{ 'text-decoration-line-through': task.done}"
              >
                {{ task.title }}
              </v-list-item-title>
            </v-list-item-content>

              <v-list-item-action>
                <v-btn
                  icon
                  @click.stop="deleteTask(task.id)"
                >
                  <v-icon color="red lighten-1">mdi-delete</v-icon>
                </v-btn>
              </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-list>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      tasks: [],
      newTaskTitle: '',
    };
  },
  methods: {
    doneTask(id) {
      const task = this.tasks.filter((selectedTask) => selectedTask.id === id)[0];
      task.done = !task.done;
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
    addTask() {
      this.tasks.push({
        id: this.tasks.length,
        title: this.newTaskTitle,
        done: false,
      });
      this.newTaskTitle = '';
    },
  },
};
</script>
