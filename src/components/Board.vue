<template>
  <v-container>
    <v-row>
      <!--add task dialog-->
      <v-btn depressed color="primary" @click="createTask()" class="add-btn"
        >add task</v-btn
      >
      <CreateTask v-if="show"></CreateTask>
      <!--add task dialog-->
    </v-row>
    <v-row>
      <!--pending container-->
      <v-col>
        <v-card
          outlined
          height="800px"
          color="grey lighten-2"
          class="main-card"
        >
          <v-card-title v-if="arrBacklog.length > 0">
            <h3>Pending ({{ arrBacklog.length }})</h3>
          </v-card-title>
          <v-card-title v-else>
            <h3>Pending</h3>
          </v-card-title>
          <v-list-item>
            <v-list-item-content>
              <Draggable :list="arrBacklog" group="task" class="kanban-col">
                <div v-for="element in arrBacklog" :key="element.id">
                  <v-row>
                    <v-col md="11">
                      <TaskItem class="taskTitle" :list="element" :task="true">
                        ></TaskItem
                      ></v-col
                    ><v-col md="1">
                      <v-icon class="deleteIcon" @click="deletePending()"
                        >mdi-delete-forever</v-icon
                      ></v-col
                    ></v-row
                  >
                </div>
              </Draggable>
            </v-list-item-content>
          </v-list-item>
        </v-card>
      </v-col>
      <!--pending container-->
      <!--progress container-->
      <v-col>
        <v-card
          outlined
          height="800px"
          color="blue lighten-2"
          class="main-card"
        >
          <v-card-title v-if="arrProgress.length > 0">
            <h3>In Progress ({{ arrProgress.length }})</h3>
          </v-card-title>
          <v-card-title v-else>
            <h3>In Progress</h3>
          </v-card-title>
          <v-list-item>
            <v-list-item-content>
              <Draggable :list="arrProgress" group="task" class="kanban-col">
                <div v-for="element in arrProgress" :key="element.id">
                  <v-row>
                    <v-col md="11">
                      <TaskItem
                        class="onGoTitle"
                        :list="element"
                        :onGoing="true"
                      >
                        ></TaskItem
                      ></v-col
                    ><v-col md="1">
                      <v-icon class="deleteIcon" @click="deleteProg()"
                        >mdi-delete-forever</v-icon
                      ></v-col
                    ></v-row
                  >
                </div>
              </Draggable>
            </v-list-item-content>
          </v-list-item>
        </v-card>
      </v-col>
      <!--progress container-->
      <!--done container-->
      <v-col>
        <v-card
          outlined
          height="800px"
          color="green lighten-2"
          class="main-card"
        >
          <v-card-title v-if="arrDone.length > 0">
            <h3>Done ({{ arrDone.length }})</h3>
          </v-card-title>
          <v-card-title v-else>
            <h3>Done</h3>
          </v-card-title>
          <v-list-item>
            <v-list-item-content>
              <Draggable :list="arrDone" group="task" class="kanban-col">
                <div v-for="element in arrDone" :key="element.id">
                  <v-row>
                    <v-col md="11">
                      <TaskItem
                        class="completeTitle"
                        :list="element"
                        :done="true"
                      >
                        ></TaskItem
                      ></v-col
                    ><v-col md="1">
                      <v-icon class="deleteIcon" @click="deleteDone()"
                        >mdi-delete-forever</v-icon
                      ></v-col
                    ></v-row
                  >
                </div>
              </Draggable>
            </v-list-item-content>
          </v-list-item>
        </v-card>
      </v-col>
      <!--done container-->
    </v-row>
  </v-container>
</template>

<script>
  import Draggable from 'vuedraggable';
  import TaskItem from './TaskItem';
  import { bus } from '../main';
  import CreateTask from './CreateTask.vue';

  export default {
    components: {
      Draggable,
      TaskItem,
      CreateTask,
    },
    data: () => ({
      show: false,
      arrBacklog: [],
      arrProgress: [],
      arrDone: [],
      count: 3,
    }),
    created() {
      bus.$on('title', (data) => {
        var ids = this.count + 1;
        if (data.titleTxt == '') {
          alert('please create some task');
        } else {
          this.arrBacklog.push({
            name: data.titleTxt,
            descTxt: data.DescTxt,
            time: data.taskTime,
            id: ids,
          });
          this.show = data.close;
          this.count = ids;
        }
      }),
        bus.$on('cancel', (cancel) => {
          this.show = cancel;
        });
    },
    methods: {
      createTask() {
        this.show = true;
      },
      deletePending() {
        this.arrBacklog.pop();
      },
      deleteProg() {
        this.arrProgress.pop();
      },
      deleteDone() {
        this.arrDone.pop();
      },
    },
  };
</script>

<style scoped>
  .kanban-col {
    min-height: 800px;
  }
  .main-card {
    overflow-y: scroll;
  }
  .cards {
    margin-bottom: 10px;
  }
  .task-detail {
    margin-left: 10px;
  }

  .add-btn {
    margin-top: 20px;
  }

  .taskTitle {
    background-color: rgb(156, 151, 151);
    padding: 5px;
    border: 1px solid steelblue;
  }
  .onGoTitle {
    background-color: rgb(255, 204, 127);
    padding: 5px;
    border: 1px solid steelblue;
  }
  .completeTitle {
    background-color: aquamarine;
    padding: 5px;
    border: 1px solid steelblue;
  }
</style>
