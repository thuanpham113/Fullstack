<template>
  <body>
    <div class="container">
      <div class="card" v-for="user in Users" :key="user.id">
        <div class="face face1 design">
          <div class="content">
            <img :src="`http://localhost:1337${user.IMG.url}`" />
            <h3>{{ user.Title }}</h3>
          </div>
        </div>
        <div class="face face2">
          <div class="content">
            <p>
              Lorem ipsum dolor sit amet consectetur adipisicing elit. Quas cum
              cumque minus iste veritatis provident at.
            </p>
            <a :href="`/${user.Title}`">Read More</a>
          </div>
        </div>
      </div>
    </div>
  </body>
</template>
<script>
import gql from "graphql-tag";
export default {
  data() {
    return {
      Users: [],
    };
  },
  apollo: {
    Users: {
      query: gql`
        query Title {
          client: titlePapers {
            id
            Title
            IMG {
              url
            }
          }
        }
      `,
      update: (Users) => Users.client,
    },
  },
};
</script>
<style scoped>
body {
  margin: 0;
  padding: 0;
  min-height: 100vh;
  width: 100vw;
  color: #000;
  background: #333;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: consolas;
}
@media (max-width: 740px) {
  body {
    height: auto;
  }
  .container {
    flex-direction: column;
  }
}
.container {
  width: 1250px;
  position: relative;
  display: flex;
  justify-content: space-around;
  align-items: center;
  flex-wrap: wrap;
}

.container .card {
  position: relative;
  cursor: pointer;
}

.container .card .face {
  width: 350px;
  height: 250px;
  transition: 0.5s;
}

.container .card .face.face1 {
  position: relative;
  background: #333;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1;
  transform: translateY(125px);
}

.container .card:hover .face.face1 {
  background: #ff0057;
  transform: translateY(0);
}
.container .card:hover .face.face1.design {
  background: #389393;
  transform: translateY(0);
}
.container .card:hover .face.face1.code {
  background: #185adb;
  transform: translateY(0);
}
.container .card:hover .face.face1.launch {
  background: #ffc107;
  transform: translateY(0);
}
.container .card .face.face1 .content {
  opacity: 0.2;
  transition: 0.5s;
}

.container .card:hover .face.face1 .content {
  opacity: 1;
}

.container .card .face.face1 .content img {
  max-width: 100px;
}

.container .card .face.face1 .content h3 {
  margin: 10px 0 0;
  padding: 0;
  color: #fff;
  text-align: center;
  font-size: 1.5em;
}

.container .card .face.face2 {
  position: relative;
  background: #fff;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
  box-sizing: border-box;
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.8);
  transform: translateY(-125px);
}

.container .card:hover .face.face2 {
  transform: translateY(0);
}

.container .card .face.face2 .content p {
  margin: 0;
  padding: 0;
}

.container .card .face.face2 .content a {
  margin: 15px 0 0;
  display: inline-block;
  text-decoration: none;
  font-weight: 900;
  color: #333;
  padding: 5px;
  border: 1px solid #333;
}

.container .card .face.face2 .content a:hover {
  background: #333;
  color: #fff;
}
</style>