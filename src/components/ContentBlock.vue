<template>
  <div class="content">
    <h1 class="content__title">{{ msg }}</h1>
    <div class="content__check"><span class="content__mark">Перенесите файл сюда</span></div>
    <button class="button button_type_check" type="button">Отправить</button>
    <Cards />
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
};
</script>
