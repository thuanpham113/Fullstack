<template>
  <div>
    <Loading v-if="$fetchState.pending"/>
    <v-row v-else>
      <v-card-text>APP RELEASE</v-card-text>
      <v-card-title primary-title> title </v-card-title>
      <v-col>
        <v-avatar size="avatarSize" color="red">
          <!-- <img
            :src="`http://localhost:1337${this.img}`"
            alt="alt"
          /> -->
        </v-avatar>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  props: ["img"],
};
</script>