<template>
  <div class="content">
    <h1 class="content__title">{{ msg }}</h1>
    <div :class="classActive">
      <input
        @drop="onDragDrop"
        @dragover="onDragOver"
        @change="isStatusInput"
        @click="onClickInput"
        type="file"
        class="content__input"
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
    </div>
    <template v-if="status">
      <button
        class="button button_type_check"
        @click="onAddImages"
        type="button"
      >
        Отправить
      </button>
    </template>
    <template v-else>
      <button
        class="button button_type_check"
        @click="onAddImages"
        type="button"
        disabled
      >
        Отправить
      </button>
    </template>
    <Cards :srcImages= "srcImages" />
  </div>
</template>

<script>

import Cards from './Cards.vue';

export default {
  components: { Cards },
  name: 'ContentBlock',
  data: () => ({
    srcImages: [],
    status: false,
    classActive: 'content__check',
    messageStatus: 'Перенесите сюда файл',
  }),
  filesNames: [],
  fileLoader: [],
  props: {
    msg: String,
  },
  methods: {
    onClickInput(evt) {
      evt.preventDefault();
    },
    isStatusInput(evt) {
      if (evt.target.value) {
        this.status = true;
        this.messageStatus = 'Файлы получены';
        this.classActive = 'content__check content__check_active';
      } else {
        this.status = false;
        this.classActive = 'content__check';
      }
    },
    onAddImages() {
      if (this.status) {
        this.readerImages(this.fileLoader);
        this.status = false;
        this.messageStatus = 'Перенесите сюда файл';
        this.classActive = 'content__check';
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
          this.classActive = 'content__check content__check_error';
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
