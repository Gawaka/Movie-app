<template>
<header>
  <router-link to="/">
    <h1><span>Movies</span>Search</h1>
  </router-link>
</header>
<main>
  <router-view/>
</main>
</template>

<script>
</script>

<style lang="scss">
@import '@/assets/__variables.scss';
@import '@/assets/__mixins.scss';

header {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px 15px;
  background-color: $primary-color;
  box-shadow: $box-shadow-color;

  h1 {
    color: $text-color;
    font-size: 28px;

    span{
      color: $secondary-color;
    }
  }

  &:active {
    h1  {
      color: $secondary-color;
      transition: 0.4s;
    }

    span {
      color: $text-color;
      transition: 0.4s ease-in-out;
    }
  }
}
</style>
