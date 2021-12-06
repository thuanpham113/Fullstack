<template>
  <div class="components" @mouseover="mouse = true" @mouseleave="mouse = false">
    <img
      :src="`http://localhost:1337${datas.image.url}`"
      alt=""
      class="user_img"
      :class="{ user_img1: mouse === true }"
    />
    <div class="user_div">
      <a href="" style="width: 300px">
        <v-icon class="icons" :class="{ icon1: mouse === true }"
          >mdi-facebook</v-icon
        >
      </a>
      <v-icon class="icons" :class="{ icon1: mouse === true }"
        >mdi-instagram</v-icon
      >
      <v-icon class="icons" :class="{ icon1: mouse === true }"
        >mdi-twitter</v-icon
      >
    </div>
  </div>
</template>
<script>
import gql from "graphql-tag";
export default {
  props: ["id"],
  data() {
    return {
      mouse: false,
      datas: [],
    };
  },
  methods: {
    thismouse() {
      this.mouse = true;
    },
    outmouse() {
      this.mouse = false;
    },
  },
  apollo: {
    datas: {
      query: gql`
        query clients($id: ID!) {
          client: userId(id: $id) {
            id
            image{
              url
            }
            Facebook
          }
        }
      `,
      variables() {
        return {
          id: this.id,
        };
      },
      update: (datas) => datas.client,
    },
  },
};
</script>
<style lang="scss" scoped>
.components {
  width: 250px;
  height: 400px;
  border-radius: 0.5rem;
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.8);
  padding: 0.5rem;
  display: grid;
  overflow: hidden;
  margin: 100px;
  grid-template-columns: 17.6rem 19rem 20.4rem;
  grid-template-rows: repeat(autofit, min-content);
  grid-column-gap: 5rem;
  grid-row-gap: 2.5rem;
  align-items: flex-start;
  justify-items: start;
  position: relative;
  background-color: black;
}
.user_img {
  height: 100%;
  position: absolute;
  --uservalue: 0;
  transition: height 1s ease-in-out, transform 1s ease-in-out;
}
.user_img1 {
  height: 200%;
  transform: translatex(-50px);
  transition: height 1s ease-in-out, transform 1s ease-in-out;
  --uservalue: 100;
}
.user_div {
  display: flex;
  flex-direction: column;
  height: 100%;
  width: 100%;
  overflow: hidden;
  align-items: flex-start;
  justify-content: flex-end;
}
.v-icon {
  margin: 5px;
  width: 10%;
  display: none;
  overflow: hidden;
  transform: translatex(0);
  transition: transform 0.5s;
  transition: display 0.5s;
}
.icon1 {
  display: block;
  transition: display 2s;
}
.theme--dark.v-icon:hover {
  color: red;
  transform: translatex(10px);
  transition: transform 0.5s;
}
</style>

<style scoped>
.theme--dark.v-icon {
  color: white;
}
</style>