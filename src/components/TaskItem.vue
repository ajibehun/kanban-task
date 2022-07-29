<template>
  <v-card outlined class="cards" @click="show = !show"
    ><v-card-title>{{ list.name }}</v-card-title>
    <taskDetailPg v-if="show" :listItem="list" />
  </v-card>
</template>

<script>
  import taskDetailPg from './TaskDetails';
  export default {
    components: {
      taskDetailPg,
    },
    props: {
      list: Object,
      onGoing: {
        type: Boolean,
        required: false,
      },
      done: {
        type: Boolean,
        required: false,
      },
      task: {
        type: Boolean,
        required: false,
      },
    },
    data: () => ({
      show: false,
    }),
    methods: {
      taskDetails() {
        this.show = true;
      },
    },
  };
</script>
