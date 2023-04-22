<template>
  <div class="w-full shadow-md rounded-lg p-5">

    <h1 v-if="$fetchState.pending">Fetching mountains...</h1>
    <h1 v-else-if="$fetchState.error">An error occurred :(</h1>

    <div v-else>
      <h1 class="text-3xl text-red-500 font-bold"> Novels </h1>

      <div class="py-3">
        <ul class="grid grid-cols-3">
          <li class="p-3 py-5" v-for="(data, index) of result" :key="index">
            <img 
              class="w-full object-cover rounded-xl"
              :src="data?.thumbnail" 
              :alt="data?.title">
            <h1 class="font-bold text-xl">{{ data?.title }}</h1>

            <div class="flex flex-row flex-wrap gap-2 items-center" >
              <div v-for="(path, i) of data?.path" :key="i">
                <a target="_blank" rel="unfollow" :href="data?.thumbnail + path?.endpoint" class="px-1.5 py-0.5 text-xs rounded-full bg-red-500 text-white">{{ path?.part }}</a>
              </div>
            </div>

            <p>{{ data?.auth }}</p>
            <p>{{ data?.description }}</p>
            
          </li>
        </ul>
      </div>

      <button class="px-3 py-1 rounded-full bg-red-500 text-white" @click="$fetch">Refresh</button>
      
    </div>

  </div>
</template>


<script>
  export default {
    name: "HelloWorld",
    data() {
      return {
        result: []
      }
    },
    async fetch() {
      this.result = await fetch(
        'https://api.npoint.io/fd95ed8784305496350b/result'
      )
      .then(res => res.json())

      // console.log(this.result);
    }
  }
</script>