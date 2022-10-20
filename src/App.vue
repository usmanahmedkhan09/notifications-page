<template>
  <div class="card">
    <div class="card--header">
      <div class="heading">
        <p class="text">Notifications</p>
        <div class="count" v-if="unreadCount > 0">{{ unreadCount }}</div>
      </div>
      <div class="status" @click="markedAllRead">Mark all as read</div>
    </div>
    <div class="card--body">
      <div
        class="notifications"
        :class="!item.read ? 'read' : 'unread'"
        v-for="(item, index) in notifications"
        :key="index"
      >
        <div class="image_wrapper">
          <img :src="getImage(`${item.pic}.jpg`)" alt="user" />
        </div>
        <div class="body">
          <p>
            <span class="name">{{ item.name }}</span>
            <span class="message-body">{{ item.body }}</span>
            <strong v-if="item.reacted">{{ item.reacted }}</strong>
          </p>
          <p class="time">{{ item.time }}</p>
          <div v-if="item.privateMessage" class="private-message">
            {{ item.privateMessage }}
          </div>
        </div>
        <figure v-if="item.commentedPicture" class="comment-figure">
          <img :src="getImage(`${item.commentedPicture}.jpg`)" alt="user" />
        </figure>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { computed, defineComponent, ref } from "vue";

export default defineComponent({
  setup() {
    let notifications = ref([
      {
        name: "Mark Webber",
        pic: "avatar-mark-webber",
        time: "1m ago",
        body: "reacted to your recent post",
        reacted: "My first tournament today!",
        read: false,
      },
      {
        name: "Angela Gray",
        pic: "avatar-angela-gray",
        time: "5m ago",
        body: "followed you",
        read: false,
      },
      {
        name: "Jacob Thompson",
        pic: "avatar-jacob-thompson",
        time: "1 day ago",
        body: "has joined your group",
        reacted: "Chess Club",
        read: false,
      },
      {
        name: "Rizky Hasanuddin",
        pic: "avatar-rizky-hasanuddin",
        time: "5 days ago",
        body: "sent you a private message",
        privateMessage:
          "Hello, thanks for setting up the Chess Club, I've been member for a few weeks now and I'm already having alots of fun and improving my game.",
        read: true,
      },
      {
        name: "kimberly Smith",
        pic: "avatar-kimberly-smith",
        time: "1 week ago",
        body: "commented on your profile",
        commentedPicture: "image-chess",
        read: true,
      },
      {
        name: "Nathan Peterson",
        pic: "avatar-nathan-peterson",
        time: "2 weeks ago",
        body: "reacted to your recent post",
        reacted: "5 end-game strategies to increase your win rate",
        read: true,
      },
      {
        name: "Anna Kim",
        pic: "avatar-anna-kim",
        time: "2 weeks ago",
        body: "left the group",
        reacted: "Chess Club",
        read: true,
      },
    ]);

    let unreadCount = computed(() => {
      return notifications.value.filter((item: any) => !item.read).length;
    });

    const markedAllRead = () => {
      notifications.value.filter((item: any) => (item.read = true));
    };

    const getImage = (url: any) => {
      return new URL(`./assets/images/${url}`, import.meta.url).href;
    };
    return { notifications, getImage, unreadCount, markedAllRead };
  },
});
</script>
