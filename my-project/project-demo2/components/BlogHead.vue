<template>
  <div>
    <v-col>
      <v-card-text>APP RELEASE</v-card-text>
      <v-card-title primary-title> {{this.title}} </v-card-title>
      <v-row>
        <v-avatar size="55">
          <img :src="this.img" alt="alt" />
        </v-avatar>
        <strong>{{ this.name }}</strong>
        <p>{{ new Date(this.date).toLocaleDateString() }}</p>
        <v-row>
          <v-icon>
            mdi-comment-outline
          </v-icon>
          <p>Comments {{ this.comment.length }}</p>
        </v-row>
      </v-row>
    </v-col>
  </div>
</template>

<script>
export default {
  props: ["title","img", "name", "date", "comment"],
};
</script>