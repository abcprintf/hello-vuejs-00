<template>
    <div class="container">
      <SearchBar @termChange="onTermChange"></SearchBar>
      <div class="row">
        <VideoDetail v-bind:video="this.selectedVideo" />
        <VideoList @onVideoSelect="onVideoSelect" v-bind:videos="this.myListOfVideos"></VideoList>
      </div>
    </div>
</template>

<script>
import axios from 'axios';
import config from './config/ulity';

import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';
import VideoDetail from './components/VideoDetail';

const API_KEY = config.API_KEY;

export default {
  name: 'App',
  components: {
    SearchBar,
    VideoList,
    VideoDetail
  },
  data() {
    return {
      myListOfVideos: [],
      selectedVideo: null
    }
  },
  methods: {
    onVideoSelect(video) {
      this.selectedVideo = video;
    },
    onTermChange(searchTerm) {
      if(searchTerm !== null){
        axios.get('https://www.googleapis.com/youtube/v3/search', {
          params: {
            key: API_KEY,
            type: 'video',
            part: 'snippet',
            q: searchTerm
          }
        }).then(response => {
          this.myListOfVideos = response.data.items;
        });
      }else{
        this.myListOfVideos = [];
      }
    }
  },
  computed() {
    console.log("computed....");
  }
}
</script>