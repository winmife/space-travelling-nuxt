/* eslint-disable vue/multi-word-component-names */
<template>
  <div>
    <div class="container flow flex crew">
      <div id="content" v-if="technology">
        <h1 class="numbered-title"><span>01</span> Space Launch 101</h1>
        <img :src="technology['image-landscape'].guid" alt="Start-Foto" />

        <ul class="dot-indicators flex">
          <li
            v-for="(item, index) in technologies"
            :key="item['technology-name']"
            @click="setTechnology(index)"
          >
            {{ index + 1 }}
          </li>
        </ul>
        <h3 class="terminology uppercase text-accent">The Terminology</h3>
        <h1 class="technology uppercase ff-serif">
          {{ technology['technology-name'] }}
        </h1>
        <p class="description text-accent">{{ technology.description }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      technologies: [],
      activeTechnologyValue: 0,
    }
  },
  computed: {
    technology() {
      return this.technologies[
        this.technologies.length - 1 - this.activeTechnologyValue
      ]
    },
  },
  methods: {
    async loadData() {
      const response = await fetch(
        'https://space.wp.seiwald.hak-stjo.schulwebspace.at/wp-json/wp/v2/technology'
      )
      this.technologies = await response.json()
    },
    setTechnology(value) {
      this.activeTechnologyValue = value
    },
  },
  mounted() {
    this.loadData()
    document.body.style.backgroundImage =
      "url('background-technology-mobile.jpg')"
  },
}
</script>

<style scoped>
.dot-indicators {
  list-style-type: none;
  justify-content: center;
  padding-top: 15px;
}
.terminology {
  text-align: center;
  padding-top: 10px;
}
.technology {
  text-align: center;
  padding-bottom: 10px;
}
.description {
  text-align: center;
}
</style>
