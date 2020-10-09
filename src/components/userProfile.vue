<template>
  <div class="user-profile">
    <div class="user-profile_user-panel">
        <h1 class="user-profile_user-name">@{{user.username}}</h1>
        <div v-if="user.isAdmin" class="user-profile_admin-badge">
            Admin
        </div>
        <div class="user-profile_follower-count">
            <strong>Followers:</strong> {{ followers }}
        </div>
        <form class="user-profile_create-form" @submit.prevent="createNewTwit">
          <label for="newTwit"><strong>New Twits</strong></label>
          <textarea id="newTwit" cols="30" rows="4" v-model="newTwitContent"></textarea>
          
          <div class="user-profile_create-twit-type">
            <label for="newTwitType"><strong>Type: </strong></label>
            <select id="newTwitType" v-model="selectedTwitType">
              <option :value="option.value" v-for="(option, index) in twitTypes" :key="index">
                  {{ option.name }}
              </option>
            </select>
          </div>
          <button>Tweet</button>
        </form>
    </div>
    <div class="user-profile_twit-wrapper">
      <twitItem 
      v-for="twit in user.twits" 
      :key="twit.id" 
      :username="user.username" 
      :twit="twit" 
      @favorite="toggleFavorite"/>
    </div>
  </div>
</template>

<script>
import twitItem from "./twitItem";  

export default {
  name: 'userProfile',
  components: { twitItem },
  data () {
    return {
      newTwitContent: '',
      selectedTwitType: 'instant',
      twitTypes: [
        {value: 'draft', name: 'Draft'},
        {value: 'instant', name: 'Instant Twit'}
      ],
      followers: 0,
      user: {
        id: 1,
        username: 'Patrick',
        firstname: 'Patrick',
        lastname: 'Campbell',
        email: 'patrick@patrick.com',
        isAdmin: true,
        twits: [
        {id: 1, content: "Wooow Vue"},
        {id: 2, content: "Better than react!"}
        ]
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
    },
    toggleFavorite(id){
      console.log(`Favorited Twit #${id}`)
    },
    createNewTwit() {
      if (this.newTwitContent && this.selectedTwitType !== 'draft'){
        this.user.twits.unshift({
          id: this.user.twits.length +1,
          content: this.newTwitContent
        })
        this.newTwitContent = ''
      }
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
.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 100%;
    padding: 50px 5%;
    margin: 0 auto;
}

.user-profile_user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 8px;
    border: 1px solid orangered;
}

h1 {
    margin: 0;
}

.user-profile_admin-badge{
    background-color: pink;
    color: green;
    font-weight: bold;
    padding: 4px;
    border-radius: 4px;
}
</style>
