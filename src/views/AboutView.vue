<template>
  <div class="container">
    <div class="about__user">
      <div class="user__image">
        <img src="https://cdn.dribbble.com/users/60166/screenshots/15050243/media/97842f9002c3fefdf33d66c47d8dad70.jpg?compress=1&resize=300x300" alt="image">
      </div>
      <div class="user__info">
        <h4>Информация о пользователе [id # {{ $route.params.id }}]</h4>
        <div class="info__block">
          <h5>Имя</h5>
          <input type="text" value="Abraam Lincoln">
        </div>
        <div class="info__block">
          <h5>Возраст</h5>
          <input type="text" value="12 лет">
        </div>
        <div class="info__block">
          <button  class="info__button" @click="save">Сохранить данные</button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
}
.user__image > img {
  width: 300px;
  height: 300px;
}
.about__user {
  display: flex;
  padding: 50px 50px;
  background-color: #f8f8f8;
}
.user__info {
  margin-left: 30px;
}
.info__block {
  margin-top: 30px;
}
.info__block:last-child {
  margin-top: 75px;
}
.info__button {
  background-color: black;
  color: white;
  padding: 10px 10px;
  font-size: 16px;
}
</style>

<script>
import axios from "axios";

export default {
  name: "AboutView",

  data: () => ({
    users: [],
  }),
  methods: {
    save() {

    }
  },
  mounted() {
    axios
        .patch(`https://localhost:3000/users/${this.$route.params.id}`, {
          "name": this.users.name,
          "age": this.users.age,
          "imagesUrl": this.users.imagesUrl,
        })
        .then(response => (this.users = response));
  }
}
</script>