<template>
  <template v-if="srcImages.length > 0">
    <div class="cards">
      <img
        v-for="srcImage in srcImages"
        class="card"
        :alt="srcImage.name"
        :src="srcImage.link"
        :key="srcImage.name"
        @mousedown="togglePopup"
      >
    </div>
  </template>
  <template v-else>
    <div class="cards">
      <span class="cards__title">Здесь будут отображаться ваши загруженные файлы</span>
    </div>
  </template>
  <template v-if="popupStatus">
    <div class="popup popup_opened" @mousedown="togglePopup">
      <img class="popup__pic" :src="src" alt="title">
    </div>
  </template>
</template>

<script>
export default {
  name: 'Cards',
  props: {
    srcImages: Array,
  },
  data: () => ({
    popupStatus: false,
    src: '',
    title: '',
  }),
  methods: {
    togglePopup(evt) {
      this.popupStatus = !this.popupStatus;
      this.src = evt.target.src;
      this.title = evt.target.alt;
    },
  },
};
</script>
