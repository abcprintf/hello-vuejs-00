<template>
    <ul class="list-group col-md-4">
       <VideoListItem 
            v-for="video in videos" 
            :key="video.etag"
            :video="video"
            @onVideoSelect="onVideoSelect"
        >
        </VideoListItem>
    </ul>
</template>

<script>
import VideoListItem from './VideoListItem';

export default {
    name: 'VideoList',
    components: {
        VideoListItem
    },
    props: ['videos'],
    methods: {
        onVideoSelect(video) {
            this.$emit('onVideoSelect', video);
        }
    }
}
</script>

<style scoped>

</style>