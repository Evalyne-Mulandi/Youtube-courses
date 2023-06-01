<template>
    <div class="">
      <div
        class="flex flex-col items-center sm:max-w-lg max-w-full rounded py-5 mx-auto px-2"
      >
        <h1 class="text-2xl font-bold text-gray-700 mb-4">Create Course form</h1>
        <Loading v-if="store.loading" class="" />
        <form class="w-full max-w-lg" @submit.prevent="addCourse">
          <div class="flex flex-wrap mb-6">
            <div class="w-full mb-3">
              <label class="block text-gray-700 font-bold mb-2" for="title"> Video ID </label>
              <input
                v-model="video_id"
                class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                id="video_id"
                type="text"
                placeholder="Enter courses video id"
                required
              />
            </div>
            <div class="w-full mb-3">
              <label class="block text-gray-700 font-bold mb-2" > Video Name </label>
              <input
                v-model="video_name"
                class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                id="video_name"
                type="text"
                placeholder="Enter video name"
                required
              />
            </div>
            <div class="w-full mb-3">
              <label class="block text-gray-700 font-bold mb-2" for="channel_name">
                channel Name
              </label>
              <textarea
                v-model="channel_name"
                class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                id=" channel_name"
                placeholder="Enter  channel_name"
                rows="3"
              ></textarea>
            </div>
          </div>
          <div class="flex justify-end">
            <button
              class="bg-yellow-600 text-white px-4 py-2 rounded-lg cursor-pointer ring-1 ring-white my-2"
            >
              Add Course
              <Icon name="ic:round-bookmark-add" class="h-10 w-10" />
            </button>
          </div>
        </form>
      </div>
    </div>
  </template>
  
  <!-- <script setup>
  import { ref, computed } from "vue";
  import { useCreateBookMarkStore } from "~/composables/useCreateBookMark";
  const store = useCreateBookMarkStore();
  const user = store.$state.user;
  const title = ref("");
  const description = ref("");
  const url = ref("");
  
  const bookmark = computed(() => {
    return {
      video_id: video_id.value,
      video_name: video_name.value,
      channel_name: channel_name.value,
    };
  });
  
  const createBook = async () => {
    console.log(bookmark.value);
    await store.create(bookmark.value);
  };
  </script> -->