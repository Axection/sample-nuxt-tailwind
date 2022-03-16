<template>
  <div class="flex justify-center gap-2">
    <div class="ex-link">
      <nuxt-link to="/one">
        Exercise One
      </nuxt-link>
    </div>
    <div class="ex-link">
      <nuxt-link to="/two">
        Exercise Two
      </nuxt-link>
    </div>
  </div>
</template>

<style scoped>
.ex-link {
  @apply p-2 border-2 border-green-300 border-solid rounded-lg;
  @apply hover:bg-slate-200;
}
</style>
