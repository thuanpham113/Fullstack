<template>
  <div class="container">
    <UserContent v-for="data in datas" :key="data.id" :id="data.id" />
  </div>
</template>

<script>
import gql from "graphql-tag";
export default {
  data() {
    return {
      datas: [],
    };
  },
  apollo: {
    datas: {
      query() {
        return gql`
          query clients {
            client: userIds(where: { Jobs: { Title: "Code" } }) {
              id
              Name
              Jobs {
                id
              }
            }
          }
        `;
      },
      update: (datas) => datas.client,
    },
  },
};
</script>
<style lang='scss' scoped>
.v-btn__content,
.theme--dark.v-icon,
.theme--dark.v-input {
  color: black;
}
.container {
  min-height: 100vh;
  min-width: 100vw;
  display: flex;
  position: initial;
  justify-content: center;
  align-items: center;
  font-family: "Poppins", sans-serif;
  background: #333;
  flex-wrap: wrap;
}
@media (max-width: 800px) {
  .container {
    min-height: auto;
  }
}
:root {
  --primary-light: #8abdff;
  --primary: #6d5dfc;
  --primary-dark: #5b0eeb;
  --white: #ffffff;
  --greyLight-1: #e4ebf5;
  --greyLight-2: #c8d0e7;
  --greyLight-3: #bec8e4;
  --greyDark: #9baacf;
}
</style>
<style  scoped lang="scss">
$shadow: 0 20px 50px rgba(0, 0, 0, 0.8);
$inner-shadow: 0 20px 50px rgba(0, 0, 0, 0.8);

*,
*::before,
*::after {
  margin: auto;
  padding: auto;
  box-sizing: inherit;
}
</style>
