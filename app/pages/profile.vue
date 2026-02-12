<template>
  <div class="flex flex-col items-center justify-center gap-4 p-4">
    <UCard class=" w-full max-w-2xl">
      <template #header>
        Profil
      </template>
      <div class="space-y-2">
        <div class="flex items-start justify-between gap-3">
          <img
            v-if="user?.image"
            :src="user.image"
            alt="User Avatar"
            class="w-20 h-20 rounded-full object-cover"
          >
          <div class="flex flex-col gap-1 grow">
            <UFormField
              label="Name"
              required
            >
              <UInput
                v-model="name"
                placeholder="Enter your name"
                icon="i-lucide-user"
              />
            </UFormField>
          </div>
        </div>
      </div>
      <template #footer>
        <div class="flex justify-end gap-2">
          <UButton
            @click="updateUser({ name })"
          >
            Update with useUserSession
          </UButton>
          <UButton
            @click="client?.updateUser({ name })"
          >
            Update with Client
          </UButton>
        </div>
      </template>
    </UCard>
  </div>
</template>

<script setup lang="ts">
const name = ref('')

const { user, updateUser, client } = useUserSession()

watch(user, (newUser) => {
  name.value = newUser?.name ?? ''
}, { immediate: true })
</script>
