<template>
  <div>
    <div v-if="member">
      <div>
        {{ member['crew-name'] }}
      </div>
      <img :src="member['webp-image'].guid" alt="" />
    </div>
    <button
      v-for="(item, index) in crew"
      :key="index"
      @click="setMember(index)"
    >
      {{ index + 1 }}
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      crew: [],
      active: 0,
    }
  },
  computed: {
    member() {
      return this.crew[this.crew.length - 1 - this.active]
    },
  },
  methods: {
    async loadData() {
      const response = await fetch(
        'https://space.wp.seiwald.hak-stjo.schulwebspace.at/wp-json/wp/v2/crew'
      )
      this.crew = await response.json()
    },
    setMember(value) {
      this.active = value
    },
  },
  mounted() {
    this.loadData()
    document.body.style.backgroundImage = "url('background-crew-mobile.jpg')"
  },
}
</script>
