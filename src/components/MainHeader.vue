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
  width: 100%;
  height: 300px;
  overflow: hidden;
}

.header-image {
  width: 1358px;
  height: 192px;
  object-fit: cover;
}

@media (max-width: 768px) {
  .header {
    height: 100px;
  }

  .header-image {
    width: 100%;
    height: auto;
  }
}
</style>
