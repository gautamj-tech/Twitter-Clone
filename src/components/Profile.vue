<template>
  <div>
    <div class="px-2 py-2 border-b border-lighter flex items-center">
      <router-link to="/">
        <i class="fas fa-arrow-left mr-4 hover:bg-lighter p-3 rounded-full"></i>
      </router-link>
      <div>
        <h1 class="font-bold text-lg">{{ profileData.name }}</h1>
      </div>
    </div>

    <!-- cover picture -->
    <div class="w-full h-48 bg-lighter"></div>

    <!-- Profile Details -->
    <div>
      <div class="flex w-full justify-between">
        <img
          :src="profileData.image"
          alt="pic"
          class="w-32 h-32 rounded-full border-4 -mt-16 border-white ml-2"
        />
        <button
          class="
            border
            h-10
            w-28
            font-semibold
            m-4
            border-lighter
            rounded-full
            hover:bg-lighter
          "
        >
          Edit Profile
        </button>
      </div>
      <div class="px-2">
        <h1 class="font-bold text-xl text-black">{{ profileData.name }}</h1>
        <h1 class="text-sm text-dark">@{{ profileData.handle }}</h1>
        <div class="flex">
          <p class="font-semibold pr-1">{{ noOfFollowing }}</p>
          <span class="text-dark">
            <router-link
              :to="{
                name: 'Followings',
                params: { profileName: `${profileData.name}` },
              }"
            >
              Following
            </router-link>
          </span>
          <p class="font-semibold pr-1">&nbsp;{{ noOfFollowers }}</p>
          <span class="text-dark">
            <router-link
              :to="{
                name: 'Followers',
                params: { profileName: `${profileData.name}` },
              }"
            >
              Followers
            </router-link>
          </span>
        </div>
      </div>
    </div>
    <div
      class="
        flex
        justify-around
        border-b border-lighter
        pt-8
        pb-2
        font-semibold
        text-dark
      "
    >
      <h1 class="border-b-4 -mb-2 border-blue text-black cursor-pointer">
        Tweets
      </h1>
      <h1 class="cursor-pointer">Tweets & replies</h1>
      <h1 class="cursor-pointer">Media</h1>
      <h1 class="cursor-pointer">Likes</h1>
    </div>

    <!-- Tweets -->
    <div
      v-for="tweet in myTweets"
      :key="tweet.id"
      class="w-full p-4 border-b hover:bg-lighter"
    >
      <Tweet :tweet="tweet" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Tweet from "./Tweet.vue";
export default {
  name: "Profile",
  props: ["profileData"],
  components: {
    Tweet,
  },
  data() {
    return {
      tweets: [],
      myTweets: [],
      noOfFollowers: "",
      noOfFollowing: "",
      id:""
    };
  },
  methods: {
    async countFollowers() {
      
      const request = await axios.get(`/userData/userFollowers?id=${this.id}`);
  
      return request;
    },
    async countFollowing() {
      const request = await axios.get(`/userData/userFollowings?id=${this.id}`);
  
      return request;
    },
  },
  async created() {
     const user = await JSON.parse(localStorage.getItem("userDetails"));
    this.id=user[0].id
    const tweets = await axios.get(`/userData/mytweets?id=${this.id}`);
    console.log(tweets, "My tweets");
    this.myTweets = tweets.data;
    const result_1=await this.countFollowing();
    this.noOfFollowing=result_1['data'].length
    const result_2=await this.countFollowers();
    this.noOfFollowers=result_2['data'].length
    console.log('in profile')
    console.log(this.noOfFollowing)
  },
};
</script>

<style></style>
