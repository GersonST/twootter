<template>
  <div class="user-profile-container">
    <div class="user-profile_user-panel">
      <h1 class="user-profile_username">{{ user.username }}</h1>
      <div class="user-profile_admin-badge" v-if="user.isAdmin">Admin</div>
      <div class="user-profile_follower-counts">
        <strong>Followers: </strong> {{ followers }}
      </div>
    </div>
    <div class="user-profile_twoots-wrapper">
      <div
        class="user-profile_twoot"
        v-for="twoot in user.twoots"
        :key="twoot.id"
      >
        {{ twoot.content }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "UserProfile",
  data() {
    return {
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
</style>
