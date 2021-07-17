<template>
  <div class="cards">
    <template v-if="srcImages.length > 0">
        <div
          v-for="srcImage in srcImages"
          :key="srcImage.name"
          class="card"
        >
          <img
            class="card__image"
            :alt="srcImage.name"
            :src="srcImage.link"
            @mousedown="togglePopup"
          >
          <button
            class="button button_type_close"
            type="button"
            @mousedown="cardRemove"
          />
        </div>
    </template>
    <template v-else>
        <span class="cards__title">Здесь будут отображаться ваши загруженные файлы</span>
    </template>
    <div
      v-show="popupStatus"
      class="popup popup_opened"
      @mousedown="togglePopup"
    >
      <img
        class="popup__pic"
        :src="src"
        alt="title"
      >
    </div>
  </div>
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
