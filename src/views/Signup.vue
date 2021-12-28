      <template>
  <div class="h-screen w-full flex flex-col items-center">
   
     <h1 class="text-3xl font-bold my-4"> <button
      class="h-16 w-16 hover:bg-lightblue text-3xl rounded-full text-blue"
    >
      <i class="fab fa-twitter"></i>
    </button> <i>SignUp</i></h1>
    <form @submit.prevent="submitHandler" class="w-1/3 px-4">
     
      <div class="flex flex-col">
        <!-- name -->
        <input
          class="border border-gray-400 my-2 p-3 text-grey-darkest rounded"
          type="text"
          required
          placeholder="Full name"
          v-model="name"
        />
        <!-- email -->
        <input
          class="border border-gray-400 my-2 p-3 text-grey-darkest rounded"
          type="email"
          required
          placeholder="Email"
          v-model="email"
        />
        <!-- username -->
        <input
          class="border border-gray-400 my-2 p-3 text-grey-darkest rounded"
          type="text"
          required
          placeholder="Username"
          v-model="handle"
        />
        <!-- image url -->
        
        <!-- Password -->
        <input
          class="border border-gray-400 my-2 p-3 text-grey-darkest rounded"
          type="password"
          required
          placeholder="Password"
          v-model="password"
        />
        <input
          class="border border-gray-400 my-2 p-3 text-grey-darkest rounded"
          type="text"
          placeholder="Image url"
          required
          v-model="image"
        />
      </div>
      <button
        class="
          bg-blue
          w-full
          h-14
          my-2
          rounded-2xl
          text-xl text-white
          font-bold
        "
        type="submit"
      >
        SignUp
      </button>
    </form>
    <div class="w-1/3 px-4">
      <router-link to="/login">
        <button class="bg-blue w-full h-14 rounded-2xl text-white text-xl font-bold">
          Login
        </button>
      </router-link>
    </div>
  </div>
</template>

<script>
export default {
  name: "Login",
  data() {
    return {
      name: "",
      email: "",
      handle: "",
      image: "",
      password: "",
    };
  },
  methods: {
    async submitHandler() {
      const d = {
        name: this.name,
        email: this.email,
        handle: this.handle,
        tweets:[],
        image: this.image,
        password: this.password,
      };
    console.log(d);

      try {
        const response = await fetch('http://localhost:5000/data', {
    method: 'POST', // *GET, POST, PUT, DELETE, etc.
    headers: {
      'Content-Type': 'application/json'
    },
   
    body: JSON.stringify(d) // body data type must match "Content-Type" header
  });
   const re=await response.json()
   console.log(re);
        this.$router.push("/login");
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>

<style>
</style>