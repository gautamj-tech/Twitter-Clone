<template>
  <div class="w-full">
    <div class="w-2/5 bg-gray-200 h-auto mx-auto">
      <div class="flex border-b border-gray-300 align-middle py-2 px-2">
        <h1 class="font-bold text-xl mr-2">Followings</h1>
      </div>
      <div
        v-for="following in followings"
        :key="following.id"
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
          <img :src="following.imageURL" class="rounded-full w-12 h-12 mr-2" />
          <div>
            <p class="font-bold text-left leading-tight">
              {{ following.name }}
            </p>
            <p class="text-left leading-tight text-dark">
              @{{ following.username }}
            </p>
          </div>
        </div>
        <button
          class="
            bg-black
            text-white text-sm
            w-20
            h-8
            hover:bg-dark
            rounded-full
            font-bold
          "
          @click="() => unfollowRequest(following.id)"
        >
          Unfollow
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Followings",
  data() {
    return {
      followings: [],
    };
  },
  methods: {
    async getAllFollowings(){
      const profileData = await JSON.parse(localStorage.getItem('userDetails'));
      const taskToToggle = profileData[0];
       const  tweets= await fetch(`http://localhost:5000/following?from=${taskToToggle.handle}`);
     
     const allTweets=await tweets.json();
    this.followings = allTweets;

    },
    async unfollowRequest(id){
       const res=await fetch(`http://localhost:5000/following/${id}`,
        {method:'DELETE'});
        console.log(res);
        this.getAllFollowings();
    }
   
  },
  created() {
    this.getAllFollowings();
  },
};
</script>

<style>
</style>