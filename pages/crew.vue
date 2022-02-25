<template>
  <ul>
    <li v-for="member in crew" :key="member.id">
      {{ member.title.rendered }}
    </li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      crew: [],
    }
  },
  methods: {
    async loadData() {
      const response = await fetch(
        'https://space.wp.seiwald.hak-stjo.schulwebspace.at/wp-json/wp/v2/crew'
      )
      this.crew = await response.json()
    },
  },
  mounted() {
    this.loadData()
    console.log('mounted')
  },
}
</script>
