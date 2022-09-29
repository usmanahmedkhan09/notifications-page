<template>
  <div class="card">
    <div class="card--header">
      <div class="heading">
        <p class="text">Notifications</p>
        <div class="count">3</div>
      </div>
      <div class="status">Mark all as read</div>
    </div>
    <div class="card--body">
      <div
        class="notifications"
        v-for="(item, index) in notifications"
        :key="index"
      >
        <figure>
          <img :src="`${getImage(item.pic)}.webp`" alt="" />
        </figure>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  setup() {
    let notifications = ref([
      {
        name: "Mark Webber",
        pic: "avatar-mark-webber",
      },
      {
        name: "Angela Gray",
        pic: "avatar-angela-gray",
      },
      {
        name: "Jacob Thompson",
        pic: "avatar-jacob-thompson",
      },
      {
        name: "Rizky Hasanuddin",
        pic: "avatar-rizky-hasanuddin",
      },
      {
        name: "kimberly Smith",
        pic: "avatar-kimberly-smith",
      },
      {
        name: "Nathan Peterson",
        pic: "avatar-nathan-peterson",
      },
      {
        name: "Anna Kim",
        pic: "avatar-anna-kim",
      },
    ]);

    const getImage = (url: any) => {
      return new URL(`./assets/images/${url}`, import.meta.url).href;
    };
    return { notifications, getImage };
  },
});
</script>
