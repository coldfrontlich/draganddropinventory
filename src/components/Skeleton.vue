<template>
  <div class="skeleton-wrapper">
    <div class="skeleton"></div>
  </div>
</template>

<style scoped>
.skeleton-wrapper {
  width: 100%;
  display: flex;
  justify-content: center;
}

.skeleton {
  width: 90%;
  height: 40px;
  background: linear-gradient(90deg, #3C3C3C 25%, #444444 50%, #333333 75%);
  background-size: 200% 100%;
  animation: loading 1.5s infinite linear;
  border-radius: 10px;
}

@keyframes loading {
  0% {
    background-position: 200% 0;
  }
  100% {
    background-position: -200% 0;
  }
}
</style>