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
      followings: [{id:1,
          imageURL:"https://source.unsplash.com/random/900×700/?ironman",
          name: "Iron man",
          username: "RD jr",
        },
        {
          "id":2,
          imageURL:"https://source.unsplash.com/random/900×700/?marvel",
          name: "Marvel cinamatics",
          username: "MCU",
        },],
    };
  },
  methods: {
   
  },
  created() {
    this.getAllFollowings();
  },
};
</script>

<style>
</style>