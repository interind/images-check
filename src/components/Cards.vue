<template>
  <div class="cards">
    <template v-if="((srcImages.length > 0) && `${status}`)">
        <div
          v-for="(srcImage, index) in (srcImages.filter((s) => s.name !== `${image}`))"
          :key="srcImage.name"
          class="card"
        >
          <img
            @load="getStore"
            :id="index"
            class="card__image"
            :alt="srcImage.name"
            :src="srcImage.link"
            @mousedown="togglePopup"
          >
          <button
            class="button button_type_close"
            type="button"
            :id="srcImage.name"
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
    image: '',
    status: false,
  }),
  methods: {
    getStore(evt) {
      if ((this.srcImages.length - 1) === Number(evt.target.id)) {
        localStorage.setItem('images', JSON.stringify(this.srcImages));
        const arr = this.srcImages.map((s) => ({ name: s.name, link: s.link }));
        console.log(...arr);
      }
    },
    togglePopup(evt) {
      this.popupStatus = !this.popupStatus;
      this.src = evt.target.src;
      this.title = evt.target.alt;
    },
    cardRemove(evt) {
      this.image = evt.target.id;
      const arr = JSON.parse(localStorage.getItem('images')).filter((s) => s.name !== evt.target.id);
      if (arr.length > 0) {
        this.status = true;
        localStorage.setItem('images', JSON.stringify(arr));
      } else {
        this.status = false;
        localStorage.setItem('images', JSON.stringify([]));
      }
    },
  },
};
</script>
