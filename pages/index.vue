<template>
  <div class="mt-28 w-full flex items-center justify-center">
    <ul class="flex flex-col items-center gap-2">
      <li v-for="link in links" :key="link.id">
        <NuxtLink :to="link.href">{{ link.title }}</NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',

  // name: "smt",
  data() {
    return {
      links: [{ id: 1, title: 'first-drag-and-drop', href: '/first' }],
    }
  },
}
</script>
