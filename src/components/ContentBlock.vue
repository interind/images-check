<template>
  <div class="content">
    <h1 class="content__title">{{ msg }}</h1>
    <form @submit.prevent="onAddImages" class="content__check">
      <input
        @drop="onDragDrop"
        @dragover="onDragOver"
        @change.prevent="isStatusInput"
        type="file"
        :class="classActive"
        id="input-image"
        multiple
        accept="image/*"
      >
      <template v-if="status">
        <span class="content__mark">{{ messageStatus }}</span>
      </template>
      <template v-else>
        <span class="content__mark">{{ messageStatus }}</span>
      </template>
      <div class="content__submit">
        <template v-if="status">
          <button
            class="button button_type_check"
            type="submit"
          >
            Отправить
          </button>
        </template>
        <template v-else>
          <button
            class="button button_type_check"
            type="submit"
            disabled
          >
            Отправить
          </button>
        </template>
      </div>
    </form>
    <Cards :srcImages= "srcImages" />
  </div>
</template>

<script>

import Cards from './Cards.vue';

export default {
  components: { Cards },
  name: 'ContentBlock',
  props: {
    msg: String,
  },
  data: () => ({
    srcImages: JSON.parse(localStorage.getItem('images')) || [],
    status: false,
    classActive: 'content__input',
    messageStatus: 'Перенесите сюда файл',
  }),
  filesNames: [],
  fileLoader: [],
  methods: {
    findItem(arr, name) {
      const item = Array.from(arr).find((i) => i.name === name);
      return item;
    },
    isStatusInput(evt) {
      let arrCorrect = JSON.parse(localStorage.getItem('images')) || [];
      let status = null;
      arrCorrect.forEach((src) => {
        status = this.findItem(evt.target.files, src.name);
      });
      if (!status) {
        arrCorrect = this.srcImages;
        localStorage.setItem('images', JSON.stringify(arrCorrect));
        this.status = true;
        this.messageStatus = 'Файлы получены';
        this.classActive = 'content__input content__input_active';
      } else {
        this.status = false;
        this.messageStatus = 'Файлы уже были добавлены';
        this.classActive = 'content__input content__input_error';
      }
    },
    onAddImages(evt) {
      if (this.status) {
        this.readerImages(evt.target[0].files);
        this.status = false;
        this.messageStatus = 'Перенесите сюда файл';
        this.classActive = 'content__input';
        evt.target.reset();
      }
    },
    readerImages(files) {
      files.forEach((file) => {
        const result = [];
        const reader = new FileReader(file);
        reader.onload = () => {
          this.srcImages.push({ link: reader.result, name: file.name });
          result.push({ code: reader.result, nameFile: file.name, size: file.size });
        };
        reader.readAsDataURL(file);
        console.log(result);
      });
    },
    onDragDrop(evt) {
      this.filesNames = [...Array(this.filesNames || '')];
      const arrayFiles = Array.from(evt.dataTransfer.files).filter((file) => file.type.startsWith('image/'));
      const arrayCorrect = [];
      arrayFiles.forEach((el) => {
        if (this.filesNames.length > 0 && this.filesNames.find((e) => e.includes(el.name))) {
          this.classActive = 'content__input content__input_error';
          this.messageStatus = 'Файлы уже были добавлены';
        } else {
          this.filesNames.push(el.name);
          arrayCorrect.push(el);
        }
      });
      if (arrayCorrect.length > 0) {
        this.fileLoader = arrayCorrect;
      } else {
        evt.preventDefault();
      }
    },
    onDragOver(evt) {
      evt.preventDefault();
    },
  },
};

</script>
