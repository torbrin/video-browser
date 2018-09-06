<template>
    <div class="container">
        <SearchBar @termChange="onTermChange"></SearchBar>
        <div class="row">
            <VideoDetail
                    :video="selectedVideo"
            ></VideoDetail>
            <VideoList
                    :videos="videos"
                    @videoSelect="onVideoSelect"
            ></VideoList>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    import SearchBar from './components/SearchBar';
    import VideoList from './components/VideoList';
    import VideoDetail from './components/VideoDetail';
    const API_KEY = 'AIzaSyC0-gfvo37Gt--pZtsRCq9byoffG6po4RM';

	export default {
		name: 'App',
		components: {
			VideoDetail,
			VideoList,
			SearchBar
		},
        data() {
			return {
				videos:[],
                selectedVideo:  null
            };
        },
        methods: {
			onTermChange(searchTerm) {
				axios.get('https://www.googleapis.com/youtube/v3/search', {
					params: {
						key: API_KEY,
                        type: 'video',
                        part: 'snippet',
                        q: searchTerm
                    }
                }).then(response => { this.videos = response.data.items; });
            },
            onVideoSelect(video) {
				this.selectedVideo = video;
            }
        }
	}
</script>

<style scoped>

</style>