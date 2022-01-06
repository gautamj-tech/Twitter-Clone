<template>
  <div>
    <div class="px-5 py-3 border-b border-lighter flex items-center">
      <h1 class="text-lg font-bold">Home</h1>
    </div>
    <div class="px-5 py-3 border-b border-lighter flex">
      <div>
        <img
          :src="profileData.image"
          alt="profile"
          class="w-12 h-12 rounded-full border border-lighter object-cover"
        />
      </div>
      <form v-on:submit.prevent="addNewTweet" class="w-full px-4 relative">
        <textarea
          v-model="myTweet"
          required
          placeholder="What's happening?"
          class="w-full focus:outline-none mt-3"
        ></textarea>
        <div class="flex items-center">
          <i class="text-lg text-blue mr-4 fas fa-image"></i>
          <i class="text-lg text-blue mr-4 fas fa-chart-line"></i>
          <i class="text-lg text-blue mr-4 fas fa-chart-bar"></i>
          <i class="text-lg text-blue mr-4 fas fa-smile"></i>
          <i class="text-lg text-blue mr-4 fas fa-tasks"></i>
        </div>
        <button
          class="
            h-10
            px-4
            text-white
            font-semibold
            bg-blue
            hover:bg-darkblue
            focus:outline-none
            rounded-full
            absolute
            bottom-0
            right-0
          "
        >
          Tweet
        </button>
      </form>
    </div>
    <div
      v-for="tweet in tweets"
      :key="tweet.id"
      class="w-full p-4 border-b hover:bg-lighter"
    >
      <Tweet :tweet="tweet" />
    </div>
  </div>
</template>

<script>
import Tweet from "./Tweet.vue";
export default {
  name: "Main",
  props: ["profileData"],
  components: {
    Tweet,
  },
  data() {
    return {
      tweets: [],
      myTweet: "",
    };
  },
  methods: {
    async addNewTweet() {
      if (this.myTweet == "") {
        return;
      }
      const profileData = await JSON.parse(localStorage.getItem("userDetails"));
      const taskToToggle = profileData[0];
      //all tweets starts
      const data = {
        src: taskToToggle.image,
        name: taskToToggle.name,
        handle: taskToToggle.handle,
        tweet: this.myTweet,
      };
      const response = await fetch("http://localhost:5000/tweets", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },

        body: JSON.stringify(data),
      });
      const js = await response.json();
      console.log(js);
      this.getTweets();
      //end

      // sending the tweet to database
      this.myTweet = "";
    },
    async getTweets() {
      // const details = await JSON.parse(localStorage.getItem('userDetails'));
      //     const email=details[0].email
      //     const password=res[0].password
      const request2 = await fetch(
        `http://localhost:5000/following?from=${this.profileData.handle}`
      );
      const allRequest2 = await request2.json();
      console.log(allRequest2);
      const result = await fetch("http://localhost:5000/tweets");

      const allTweets = await result.json();
      console.log(allTweets, "My tweets");
      const allRequest1 = allTweets.reverse();
      const res = allRequest1.filter((o1) =>
        allRequest2.some(
          (o2) =>
            o1.handle === o2.username || o1.handle === this.profileData.handle
        )
      );
      this.tweets = res;
    },
  },
  async created() {
    this.getTweets();
    console.log(this.profileData);
  },
};
</script>

<style></style>
