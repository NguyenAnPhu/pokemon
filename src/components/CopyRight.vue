<template>
  <div class="copyright">
    <span>This is owned by Puh -</span>
    <a href="#">View here</a>
  </div>
</template>
<style lang="css" scoped>
.copyright {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  bottom: 1.5rem;
  color: var(--light);
  z-index: 3;
  width: 100%;
  padding: 0 1rem;
  text-align: center;
  font-size: clamp(1rem, 4vw, 1.5rem);
}

.copyright a {
  color: #f4dc26;
}
</style>
