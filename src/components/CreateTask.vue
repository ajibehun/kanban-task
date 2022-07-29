<template>
  <v-container class="modals">
    <v-card>
      <v-card-title>
        <h2>Create Task</h2>
        <v-icon right @click="onClose()">mdi-close</v-icon>
      </v-card-title>
      <hr />
      <v-card-text class="cards">
        <v-row>
          <v-text-field placeholder="Enter the Title" v-model="title"
        /></v-row>

        <v-row class="inputElement">
          <v-text-field
            name="taskDescrip"
            id=""
            placeholder="Enter a Short description"
            v-model="taskDescription"
          ></v-text-field>
        </v-row>
        <v-row>
          <v-col cols="12" sm="6">
            <v-date-picker v-model="time" range></v-date-picker>
          </v-col>
          <v-col cols="12" sm="6">
            <v-text-field
              v-model="dateRangeText"
              label="Date range"
              prepend-icon="mdi-calendar"
              readonly
            ></v-text-field>
          </v-col>
        </v-row>
      </v-card-text>
      <v-card-actions>
        <v-btn color="success" @click="onEnter()">Add Task</v-btn>
      </v-card-actions>
    </v-card>
  </v-container>
</template>

<script>
  import { bus } from '../main';

  export default {
    data: () => ({
      title: '',
      taskDescription: '',
      time: [],
    }),
    computed: {
      dateRangeText() {
        return this.time.join(' ~ ');
      },
    },
    methods: {
      onEnter() {
        var titleTxt = this.title;
        var DescTxt = this.taskDescription;
        var taskTime = this.dateRangeText;
        var close = false;
        bus.$emit('title', { titleTxt, DescTxt, taskTime, close });
        this.title = '';
      },
      onClose() {
        var close = false;
        bus.$emit('cancel', close);
      },
    },
  };
</script>

<style scoped lang="scss">
  .modals {
    max-width: 800px;
    position: absolute;
    z-index: 9999999;
  }
  .cards {
    padding: 20px 20px;
  }
</style>
