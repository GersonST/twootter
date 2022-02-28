<template>
  <div class="user-profile-container">
    <div class="user-profile_user-panel">
      <h1 class="user-profile_username">{{ user.username }}</h1>
      <div class="user-profile_admin-badge" v-if="user.isAdmin">Admin</div>
      <div class="user-profile_follower-counts">
        <strong>Followers: </strong> {{ followers }}
      </div>
      <form class="user-profile_create-twoot">
        <label for="newTwoot"><strong>New Twoot</strong></label>
        <textarea id="newTwoot" rows="4" />

        <div class="user-profile_create-twoot-type">
          <label for="newTwootType"><strong>Type: </strong></label>
          <select id="newTwootType">
            <option
              :value="option.value"
              v-for="(option, index) in twootTypes"
              :key="index"
            />
          </select>
        </div>
      </form>
    </div>
    <div class="user-profile_twoots-wrapper">
      <TwootItem
        v-for="twoot in user.twoots"
        :key="twoot.id"
        :username="user.username"
        :twoot="twoot"
        @favourite="toggleFavourite"
      >
        {{ twoot.content }}
      </TwootItem>
    </div>
  </div>
</template>

<script>
import TwootItem from "./TwootItem";

export default {
  name: "UserProfile",
  components: { TwootItem },
  data() {
    return {
      twootTypes: [
        { value: "draft", name: "Draft" },
        { value: "instant", name: "Instant Twoot" },
      ],
      followers: 0,
      user: {
        id: 1,
        username: "FoxLegion",
        firstName: "Gerson",
        lastName: "Severo",
        email: "gersonsevero90@gmail.com",
        isAdmin: true,
        twoots: [
          { id: 1, content: "Twootter is amazing!!" },
          { id: 2, content: "Hello World!!" },
        ],
      },
    };
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a follower!`);
      }
    },
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavourite(id) {
      console.log(`Favourite Twoot #${id}`);
    },
  },
  mounted() {
    this.followUser();
  },
};
</script>

<style>
.user-profile-container {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
}

.user-profile_user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
}

.user-profile_admin-badge {
  background: purple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
}

h1 {
  margin: 0;
}

.user-profile_twoots-wrapper {
  display: grid;
  grid-gap: 10px;
}

.user-profile_create-twoot {
  padding-top: 20px;
  display: flex;
  flex-direction: column;
}
</style>
