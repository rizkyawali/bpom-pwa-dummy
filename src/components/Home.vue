<template>
  <div class="konten">
    

    <input type="text" name="username" v-model="username" />
    <br>

    <button @click="getUserData" > Cari </button>

    <div v-if=" user != null" class="profile">
      <img v-bind:src="user.avatar_url" width="200" height="200" alt="">
      <br>

      <label for=""> Username : {{ user.login }} </label><br>
      <label for=""> Profil Name : {{ user.name }} </label><br>
      <label for=""> Bio User : {{ user.bio }} </label><br>

    </div>

  </div>
</template>

<script>
import GithubApi from '@/services/GithubApi'
export default {
  name: 'konten',
  data () {
    return {
      msg: '',
      username: '',
      user: null
    }
  },

  methods: {
    async getUserData () {
      this.user = null

      const result = await GithubApi.searchUser({
        username: this.username
      }).then (response => {
        this.user = response.data
      }).catch(error => {
        console.log(this.user)
      })
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #35495E;
}

 h1, h2 {
    font-weight: normal;
  }
  input {
    width: 40%;
    padding: 12px 20px;
    margin: 8px 0;
    display: inline-block;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
  }
  button {
    background-color: #4CAF50;
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
  }
  .profile {
    padding: 16px;
  }
  label {
    font-size: 20px;
  }
  
</style>
