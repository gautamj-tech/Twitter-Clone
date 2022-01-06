<template>
  <div class="w-full">
    <div class="w-2/5 bg-gray-200 h-auto mx-auto">
      <div class="flex border-b border-gray-300 align-middle py-2 px-2">
        <h1 class="font-bold text-xl mr-2">Followers</h1>
      </div>
      <div
        v-for="follower in followers"
        :key="follower.id"
        class="
          w-full
          flex
          justify-between
          align-middle
          p-4
          border-b border-gray-300
        "
      >
        <div class="w-full flex align-middle">
          <img :src="follower.imageURL" class="rounded-full w-12 h-12 mr-2" />
          <div>
            <p class="font-bold text-left leading-tight">
              {{ follower.name }}
            </p>
            <p class="text-left leading-tight text-dark">
              @{{ follower.username }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Followers",
  data() {
    return {
      followers: [],
    };
  },
  methods: {
    async getAllFollowers() {
      const profileData = await JSON.parse(localStorage.getItem("userDetails"));
      const taskToToggle = profileData[0];
      const tweets = await fetch(
        `http://localhost:5000/follower?from=${taskToToggle.handle}`
      );

      const allTweets = await tweets.json();
      this.followers = allTweets;
    },
  },
  created() {
    this.getAllFollowers();
  },
};
</script>

<style></style>
