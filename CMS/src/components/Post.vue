<template>
  <div class="min-h-screen py-11 container mx-auto px-2">
    <div v-if="post" class="flex justify-center items-center flex-col gap-y-10">
      <h1 class="text-3xl">Post</h1>
      <div
        class="bg-white rounded-xl overflow-hidden text-black shadow-lg max-w-screen-md"
      >
        <div
          class="max-h-[420px] bg-cover rounded-xl bg-center object-cover overflow-hidden"
        >
          <img
            :src="`http://localhost:1337${post.attributes.Image.data.attributes.url}`"
            alt="Image"
            class="w-full"
          />
        </div>

        <div class="px-2 py-3">
          <h1 class="font-bold text-lg">{{ post.attributes.Title }}</h1>
          <p class="text-zinc-500">
            {{ post.attributes.Description }}
          </p>
          <hr class="my-4" />
          <div class="inline-flex items-center gap-x-2">
            <img
              :src="`http://localhost:1337${post.attributes.Avatar.data.attributes.url}`"
              alt="Avatar"
              class="rounded-full h-12"
            />
            <h3 class="text-lg">{{ post.attributes.Author }}</h3>
          </div>
        </div>
      </div>
      <button
        @click="goHome"
        class="rounded-lg bg-white px-6 py-3 text-black hover:bg-[#141414] hover:text-white hover:border-white border transition-colors duration-300"
      >
        Go Back
      </button>
    </div>
    <div v-else>
      <h1 class="text-5xl flex justify-center items-center">Loading...</h1>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { useRoute, useRouter } from "vue-router";
import axios from "axios";

const post = ref(null);
const route = useRoute();
const router = useRouter();
onMounted(async () => {
  try {
    const response = await axios.get(
      `http://localhost:1337/api/blogs/${route.params.id}?populate=*`
    );
    post.value = response.data.data;
  } catch (error) {
    console.error(error);
  }
});

const goHome = () => {
  router.push({ name: "Home" });
};
</script>
