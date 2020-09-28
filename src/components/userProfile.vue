<template>
  <div class="user-profile">
      <div class="user-profile_user-panel">
          <h1 class="user-profile_user-name">@{{user.username}}</h1>
      </div>
      <div class="user-profile_follower-count">
          <strong>Followers:</strong> {{ followers }}
      </div>
  </div>
</template>

<script>


export default {
  name: 'App',
  data () {
    return {
      followers: 0,
      user: {
        id: 1,
        username: 'Patrick',
        firstname: 'Patrick',
        lastname: 'Campbell',
        email: 'patrick@patrick.com',
        isAdmin: true
      }
    }
  },
  computed: {
    fullName () {
      return `${this.user.firstname} ${this.user.lastname}`
    }
  },
  methods: {
    followUser() {
      this.followers++
    }
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a follower`)
      }
    }
  },
  mounted() {
    this.followUser();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  text-align: center;
}
</style>
