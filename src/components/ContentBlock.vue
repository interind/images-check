<template>
  <div class="content">
    <h1 class="content__title">{{ msg }}</h1>
    <div class="content__check"><span class="content__mark">Перенесите файл сюда</span></div>
    <button class="button button_type_check" type="button">Отправить</button>
    <div class="content__result">
      <img class="logo" alt="Vue logo" src="../assets/logo.png">
      <img class="logo" alt="Vue logo" src="../assets/logo.png">
      <img class="logo" alt="Vue logo" src="../assets/logo.png">
      <img class="logo" alt="Vue logo" src="../assets/logo.png">
      <img class="logo" alt="Vue logo" src="../assets/logo.png">
      <img class="logo" alt="Vue logo" src="../assets/logo.png">
      <img class="logo" alt="Vue logo" src="../assets/logo.png">
      <img class="logo" alt="Vue logo" src="../assets/logo.png">
      <img class="logo" alt="Vue logo" src="../assets/logo.png">
      <img class="logo" alt="Vue logo" src="../assets/logo.png">
      <img class="logo" alt="Vue logo" src="../assets/logo.png">
      <img class="logo" alt="Vue logo" src="../assets/logo.png">
      <img class="logo" alt="Vue logo" src="../assets/logo.png">
      <img class="logo" alt="Vue logo" src="../assets/logo.png">
    </div>
  </div>
</template>

<script>
export default {
  name: 'ContentBlock',
  props: {
    msg: String,
  },
};
</script>
