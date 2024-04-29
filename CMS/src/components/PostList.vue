<template>
  <div class="min-h-screen py-11 container mx-auto">
    <div v-if="posts">
      <h2 class="text-2xl mb-8">Post List</h2>
      <div
        class="bg-white w-[300px] rounded-xl overflow-hidden text-black shadow-lg"
        v-for="post in posts"
        :key="post.id"
      >
        <router-link :to="{ name: 'Post', params: { id: post.id } }">
          <img
            :src="`http://localhost:1337${post.attributes.Image.data.attributes.url}`"
            alt="Image"
            class="bg-cover rounded-xl bg-center"
          />
          <div class="px-2 py-3">
            <h1 class="font-bold text-lg">{{ post.attributes.Title }}</h1>
            <p class="text-zinc-500">
              {{ shortenText(post.attributes.Description) }}
            </p>
            <hr class="my-2" />
            <div class="inline-flex items-center gap-x-2">
              <img
                :src="`http://localhost:1337${post.attributes.Avatar.data.attributes.url}`"
                alt="Avatar"
                class="rounded-full h-8"
              />
              <h3>{{ post.attributes.Author }}</h3>
            </div>
          </div>
        </router-link>
      </div>
    </div>
    <div v-else>
      <h1 class="text-5xl flex justify-center items-center">Loading...</h1>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
const posts = ref(null);

onMounted(async () => {
  try {
    const response = await axios.get(
      "http://localhost:1337/api/blogs?populate=*"
    );
    posts.value = response.data.data;
  } catch (error) {
    console.error(error);
  }
});

const shortenText = (text) => {
  if (text.length <= 65) {
    return text;
  } else {
    return text.substring(0, 65) + "...";
  }
};
</script>
