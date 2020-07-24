<template>
    <div class="container">
        Faca uma busca
        <SearchBar @eventChange="onTermChange"  ></SearchBar>
        <div clas="row">
            <VideoDetail :video="selectedVideo" />
            <VideoList :videos="videos" @videoSelect="onVideoSelect" > </VideoList>
        </div>
    </div>
</template>

<script>
import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';
import VideoDetail from './components/VideoDetail';

import axios from 'axios';

const API_KEY = "AIzaSyD805M8w45pQ6x_oe9bvV7deLJZWEGz9qM";

export default {
    name: 'App',
    components: {
        SearchBar,
        VideoList,
        VideoDetail
    },
    data(){
        return { videos: [], selectedVideo: null };
    },
    methods: {
        onTermChange(searchTerm){
            axios.get('https://www.googleapis.com/youtube/v3/search', {
            params:{
                key: API_KEY,
                type: 'video',
                part: 'snippet',
                q: searchTerm
            }
            }).then(response => {
                this.videos = response.data.items
            });
        },
        onVideoSelect(video){
            this.selectedVideo(video);
        }
    }
}
</script>