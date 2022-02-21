<template>
  <div class="user-profile-container">
    <div class="user-profile_user-panel">
      <h1 class="user-profile_username">{{ user.username }}</h1>
      <div class="user-profile_follower-counts">
        <strong>Followers: </strong> {{ followers }}
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

<style lang="scss" scoped></style>
