<script setup lang="ts">
import type { DropdownMenuItem } from '@nuxt/ui'

const { loggedIn, user, signOut, ready } = useUserSession()

const items: DropdownMenuItem[] = [
  {
    label: 'Profile',
    icon: 'i-lucide-user',
    onSelect: () => navigateTo('/profile')
  }, {
    label: 'Log Out',
    icon: 'i-lucide-log-out',
    onSelect: () => signOut()
  }
]
</script>

<template>
  <div class="flex items-center gap-2">
    <UButton
      v-if="!ready"
      loading
    >
      Loading
    </UButton>
    <UDropdownMenu
      v-if="ready && loggedIn"
      :items="items"
      :ui="{ content: 'w-48' }"
    >
      <UButton
        :avatar="{ src: user?.image ?? undefined }"
        :icon="user?.image ? undefined : 'lucide:log-out'"
      >
        {{ user?.name }}
      </UButton>
    </UDropdownMenu>
    <UButton
      v-if="ready && !loggedIn"
      icon="lucide:log-in"
      @click="navigateTo('/login')"
    >
      Login
    </UButton>
  </div>
</template>
