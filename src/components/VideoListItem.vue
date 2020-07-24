<template>
        <li class="list-group-item">
            <img class="mr-3" :src="thumbnailUrl" @click="onVideoSelect" />
            <div class="media-body">
                  {{ video.snippet.title }}
            </div>
        </li>
</template>

<script>

export default {
    name: 'VideoListItem',
    props: ['video'],
    computed: {
        thumbnailUrl(){
            return this.video.snippet.thumbnails.default.url
        }
    },
    methods: {
        onVideoSelect(){
            this.$emit('videoSelect', this.video);
        }
    }
}
</script>

<style scope>

li {
    display: flex;
    cursor: pointer;
}

li:hover {
    background-color: grey;
}

</style>

