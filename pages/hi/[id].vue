<script setup lang="ts">
const route = useRoute<'hi-id'>()
const user = useUserStore()
const name = route.params.id

watchEffect(() => {
  user.setNewName(route.params.id)
})

definePageMeta({
  layout: 'home',
})
</script>

<template>
  <div>
    <div i-twemoji:waving-hand inline-block animate-shake-x animate-duration-5000 text-4xl />
    <h3 text-2xl font-500>
      Hi,
    </h3>
    <div text-xl text-secondary>
      {{ $t('welcome') }}
      {{ name }}!
      <h3 text-4xl text-primary>
        {{ $t('distance') }}
      </h3>
    </div>

    <template v-if="user.otherNames.length">
      <p my-4 text-sm>
        <span op-50>Also as known as:</span>
        <ul>
          <li v-for="otherName in user.otherNames" :key="otherName">
            <router-link :to="`/hi/${otherName}`" replace>
              {{ otherName }}
            </router-link>
          </li>
        </ul>
      </p>
    </template>

    <ExamplesCounter />

    <div>
      <NuxtLink
        class="m-3 text-sm btn"
        to="/"
      >
        Back
      </NuxtLink>
    </div>
  </div>
</template>
