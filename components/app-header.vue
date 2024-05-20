<template>
  <header>
    <NuxtLink to="/" class="link">
      Finance Tracker
    </NuxtLink>
    <div>
      <UAvatar
          src="https://avatars.githubusercontent.com/u/739984?v=4"
          alt="Avatar"
      />
    </div>
  </header>
</template>

<style scoped>
  header {
    @apply
    flex items-center justify-between
    mt-10
  }

  header .link {
    @apply
    text-xl font-bold
  }
</style>