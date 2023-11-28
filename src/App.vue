<template>
    <div class="app">
        <tags-list :tags="tags1" alignment="left" />
        <tags-list :tags="tags1" alignment="center" />
        <tags-list :tags="tags2" alignment="left" class="half-width" />
        <tags-list :tags="tags2" alignment="center" class="half-width" />
    </div>
</template>

<script>
    import TagsList from './components/TagList'

    export default {
        components: {
            TagsList
        },
        data() {
            return {
                tags1: [
                    { text: 'текст1', icon: 'mdi-check' },
                    { text: 'текст2', icon: 'mdi-check' },
                    { text: 'текст3', icon: 'mdi-check' },
                    { text: 'текст4', icon: 'mdi-check' },
                ],
                tags2: [
                    { text: 'текст1', icon: 'mdi-check' },
                    { text: 'текст2', icon: 'mdi-check' },
                    { text: 'текст3', icon: 'mdi-check' },
                    { text: 'текст4', icon: 'mdi-check' },
                ]
            }
        }
    }
</script>

<style scoped>
    .half-width {
        width: 50%;
    }
</style>
