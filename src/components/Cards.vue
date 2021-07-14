<template>
  <template v-if="srcImages.length > 0">
    <div class="cards">
      <div class="card" v-for="srcImage in srcImages" :key="srcImage.name">
        <img
          class="card__image"
          :alt="srcImage.name"
          :src="srcImage.link"
          @mousedown="togglePopup"
        >
        <button @mousedown="cardRemove" class="button button_type_close" type="button"></button>
      </div>
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
    message: '',
  }),
  methods: {
    togglePopup(evt) {
      this.popupStatus = !this.popupStatus;
      this.src = evt.target.src;
      this.title = evt.target.alt;
    },
    cardRemove(evt) {
      evt.target.parentNode.remove();
    },
  },
};
</script>
