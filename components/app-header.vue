<script setup>
const supabase = useSupabaseClient()
const user = useSupabaseUser()
const items = [
  [
      {
        slot: 'account',
        disabled: true
      }
  ],
  [
      {
        label: 'Settings',
        icon: 'i-heroicons-cog-8-tooth',
        onClick: () => console.log('Link to settings in the future')
      },
      {
        label: 'Sign out',
        icon: 'i-heroicons-arrow-left-on-rectangle',
        click: async () => {
          await supabase.auth.signOut()
          return navigateTo('/login')
        }
      }
  ]
]
</script>
<template>
  <header>
    <NuxtLink to="/" class="link">
      Finance Tracker
    </NuxtLink>
    <div>
      <UDropdown
          :items="items"
          :ui="{
            item: {
              disabled: 'cursor-text select-text'
              },
              width: 'w-64'
          }"
          v-if="user">
        <UAvatar src="https://avatars.githubusercontent.com/u/739984?v=4" alt="Avatar" />

        <template #account="{ item }">
          <div class="text-left">
            <p>
              Signed in as
            </p>
            <p class="font-medium text-gray-900 dark:text-white">
              {{ user.email }}
            </p>
          </div>
        </template>

        <template #item="{ item }">
          <span class="truncate">{{ item.label }}</span>

          <UIcon :name="item.icon" class="icon" />
        </template>
      </UDropdown>
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

  .icon {
    @apply
    flex-shrink-0
    h-4 w-4
    text-gray-400 dark:text-gray-500
    ms-auto
  }
</style>