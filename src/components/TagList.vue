<template>
  <div class="tags-container">
    <v-flex v-for="(tag, index) in visibleTags" :key="index" class="tag" v-show="isVisible(tag)">
      <v-icon v-if="tag.icon" class="tag-icon">{{ tag.icon }}</v-icon>
      <span class="tag-text">{{ tag.text }}</span>
    </v-flex>
  </div>
</template>

<script>
  export default {
    props: {
      tags: {
        type: Array,
        required: true
      },
      alignment: {
        type: String,
        default: 'left'
      }
    },
    data() {
      return {
        visibleTags: []
      }
    },
    mounted() {
      window.addEventListener('resize', this.updateVisibleTags)
      this.updateVisibleTags()
    },
    destroyed() {
      window.removeEventListener('resize', this.updateVisibleTags)
    },
    methods: {
      updateVisibleTags() {
        const containerWidth = this.$el.offsetWidth
        const tags = this.tags.slice().reverse()
        let totalWidth = 0

        this.visibleTags = []

        tags.forEach(tag => {
          const width = this.getTagWidth(tag)

          if (totalWidth + width <= containerWidth) {
            totalWidth += width
            this.visibleTags.unshift(tag)
          }
        })

        this.visibleTags = this.visibleTags.reverse()
      },
      getTagWidth(tag) {
        const iconWidth = tag.icon ? 24 : 0
        const textWidth = Math.ceil(tag.text.length * 8) // Assuming 8px per character

        return iconWidth + textWidth
      },
      isVisible(tag) {
        return this.visibleTags.indexOf(tag) !== -1
      }
    }
  }
</script>

<style scoped>
  .tags-container {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: flex-start;
  }

  .tag {
    display: flex;
    align-items: center;
    margin-right: 8px;
    margin-bottom: 8px;
  }

  .tag-icon {
    margin-right: 4px;
  }

  .tag-text {
    white-space: nowrap;
  }
</style>
