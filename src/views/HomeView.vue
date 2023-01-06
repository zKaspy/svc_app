<template>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat&display=swap" rel="stylesheet">
  <v-card max-width="600" class="mx-auto">
    <v-toolbar color="light-blue" dark>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>
      <v-toolbar-title>Список пользователей</v-toolbar-title>
      <v-spacer></v-spacer>
    </v-toolbar>
    <div class="users__list" v-for="user in users" :key="user.value">
      <div class="users__item">
        <div class="users__logo">
          <img src="https://cdn.dribbble.com/users/1258347/screenshots/14725198/media/f4f50db512a56e0642b97056101eadca.jpg?compress=1&resize=60x60&vertical=top" alt="logo">
        </div>
        <div class="users__info">
          <h4>{{ user.name }}</h4>
          <h5>{{ user.age }} лет</h5>
        </div>
        <div class="users__action">
          <a class="users__button" :href="`/about/${user.id}`">Редактировать</a>
          <a class="users__button remove" @click="removeUser(user.id)">Удалить</a>
        </div>
      </div>
      <v-divider></v-divider>
    </div>
  </v-card>
</template>

<style scoped>
.users__item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-family: 'Montserrat', sans-serif;
}
.users__logo {
  width: 60px;
  height: 60px;
  border-radius: 50%;
}
.users__button {
  padding: 10px 20px;
  margin: 10px;
  background-color: green;
  border-radius: 5px;
  color: white;
  font-size: 14px;
}
.users__info {
  margin-right: 70px;
}
.remove {
  background-color: darkred;
  font-weight: bold;
}
</style>

<script>
import axios from "axios";

export default {
  name: "StartPage",

  data: () => ({
    users: [],
  }),
  methods: {
    removeUser(id) {
      axios
          .delete(`https://localhost:3000/users/${id}`)
          .then(() => (console.log('true')));
    }
  },
  mounted() {
    axios
        .get('https://localhost:3000/users')
        .then(response => (this.users = response));
  }
}
</script>
