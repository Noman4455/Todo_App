<template>
  <q-page class="bg-grey-3 column">
    <div class="rwo q-pa-sm bg-primary">
      <q-input
        v-model="newTask"
        @keyup.enter="addTask"
        class="col"
        square
        filled
        placeholder="New Task"
        bg-color="white"
        dense
      >
        <template v-slot:append>
          <q-btn @click="addTask" round dense flat icon="send" />
        </template>
      </q-input>
    </div>

    <div class="row">
      <div class="col">
        <div
          class="checkbox"
          v-for="(task, index) in tasks"
          :key="index"
          :class="!task.completed ? 'bg-white' : 'bg-blue-2'"
        >
          <q-toolbar>
            <q-toggle
              side
              top
              class="text-h6"
              :label="task.name"
              v-model="task.completed"
              color="rgb(24, 103, 156)"
            />
            <q-space />

            <q-btn
              @click="deleteTask(index)"
              flat
              dense
              icon="delete"
              size="15px"
              class="q-mt-sm q-ml-md text-grey-6"
            />
          </q-toolbar>
        </div>
      </div>
    </div>
    <div v-if="!tasks.length" class="no-task absolute-center">
      <q-icon name="check" size="100px" color="primary" />
      <div class="text-h5 text-primary">No Task</div>
    </div>
  </q-page>
</template>

<script>
import { ref } from "vue";
export default {
  name: "Todo",
  setup() {
    return {};
  },
  data() {
    return {
      newTask: '',
      tasks: [
        {
        name: 'Get Apples',
        completed: false
        },
      ],
    };
  },

  methods: {
    deleteTask: function (index) {
      this.$q
        .dialog({
          title: "Confirm",
          message: "Are You Sure You Want to Delete?",
          cancel: true,
          persistent: true,
        })
        .onOk(() => {
          this.tasks.splice(index, 1);
          this.$q.notify({
            message: "Your task is deleted",
            color: "blue-9",
          });
        });
    },
    addTask() {
      this.tasks.push({
        name: this.newTask,
        completed: false
      })
      this.newTask = ''
    }
  }
}
</script>


<style>
.checkbox {
  margin: 20px;
  border: 2px outset rgb(24, 103, 156);
}
.no-task {
  opacity: 0.6;
}
</style>
