<template>
  <header class="header">
    <img src="@/assets/header-image.svg" alt="Header Image" class="header-image">
  </header>
</template>

<script>
export default {
  name: 'MainHeader',
};
</script>

<style scoped>
.header {
  display: flex;
  width: 100%;
  height: 300px;
  overflow: hidden;
}

.header-image {
  display: flex;
  width: 1358px;
  height: 192px;
}

@media (max-width: 880px) {
  .header {
    height: 100px;
  }

  .header-image {
    width: 100%;
    height: auto;
  }
}

@media (max-width: 1355px) {
  .header {
    height: 100px;
  }

  .header-image {
    width: 100%;
    height: auto;
  }
}
</style>
