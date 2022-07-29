<template>
  <div>
    <v-card>
      <v-card-text>
        <v-card-text class="task-detail">
          <div class="mb-5">Description: {{ listItem.descTxt }}</div>
          <div>
            <v-chip>Time: {{ listItem.time }}</v-chip>
          </div>
        </v-card-text>
      </v-card-text>
    </v-card>
  </div>
</template>
<script>
  export default {
    props: {
      listItem: Object,
    },
  };
</script>

<style></style>
