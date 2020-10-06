<template>
    <div class="container">
        <b-container id="mosaico">
            <b-row class="text-center">
                <b-col>
                    <div :key="n" v-for="n in colummQtd">
                        <a v-b-modal.imageModal1>    
                            <img :src=url[n-1] v-on:click="selectedPhoto=url[n-1]">
                        </a>
                    </div>
                    <b-modal id="imageModal1" size="xl" centered="true">
                        <div class="d-block text-center">
                            <img id="modalImage" :src=selectedPhoto>
                        </div>
                    </b-modal>
                </b-col>
                <b-col>
                    <div :key="n" v-for="n in colummQtd">
                        <a v-b-modal.imageModal2>
                            <img :src=url[(n+colummQtd)-1] v-on:click="selectedPhoto=url[(n+colummQtd)-1]">
                        </a>
                    </div>
                    <b-modal id="imageModal2" size="xl">
                        <div class="d-block text-center">
                            <img id="modalImage" :src=selectedPhoto>
                        </div>
                    </b-modal>            
                </b-col>
                <b-col>
                    <div :key="n" v-for="n in colummQtd">
                        <a v-b-modal.imageModal2>
                            <img :src=url[(n+colummQtd*2)-1] v-on:click="selectedPhoto=url[(n+colummQtd*2)-1]">
                        </a>
                    </div>
                    <b-modal id="imageModal3" size="xl">
                        <div class="d-block text-center">
                            <img id="modalImage" :src=selectedPhoto>
                        </div>
                    </b-modal>   
                </b-col>
            </b-row>
        </b-container>
    </div>
</template>

<script>
import { constants } from 'crypto';
export default {
    name: 'photos',
    props:['currentAlbum'],
    watch: { 
        currentAlbum: function(newVal, oldVal) {
            if(newVal==0)
                this.PullPhotos();
            else{
                this.PullAlbum(newVal);
                console.log('Prop changed: ', newVal, ' | was: ', oldVal)
            }
        }
    },
    data: function(){
        return{
            photos: [],
            url: [],
            colummQtd: 0,
            selectedPhoto: ''
        }
    },
    methods: {
        PullPhotos() {
            this.$http.get('https://www.flickr.com/services/rest/?method=flickr.photos.search&api_key=567bbc77bc83f86d6698f83035908cea&user_id=74233873%40N00&sort=date-posted-desc&per_page=10000&page=1&format=json&nojsoncallback=1')
                .then((response) => {
                    this.photos = response.body.photos.photo;
                    console.log(response.body.photos.photo);
                    for (let i=0; i<this.photos.length; i++) {
                        this.url[i] = `http://farm${this.photos[i].farm}.staticflickr.com/${this.photos[i].server}/${this.photos[i].id}_${this.photos[i].secret}.jpg`;                                              
                    }
                    this.$forceUpdate();
                    console.log('All photos set!');
                });
        },
        PullAlbum(albumID) {
            this.$http.get(`https://www.flickr.com/services/rest/?method=flickr.photosets.getPhotos&api_key=567bbc77bc83f86d6698f83035908cea&photoset_id=${albumID}&user_id=74233873%40N00&per_page=10000&page=1&format=json&nojsoncallback=1`)
                .then((response) => {
                    this.photos = response.body.photoset.photo;
                    this.url = [];
                    for (let i=0; i<this.photos.length; i++) {
                        this.url[i] = `http://farm${this.photos[i].farm}.staticflickr.com/${this.photos[i].server}/${this.photos[i].id}_${this.photos[i].secret}.jpg`;                                              
                    }
                    this.$forceUpdate();
                    console.log('All photos set!');
                });
        },
        SetColummQtd() {
            this.colummQtd = Math.ceil(this.url.length/3)
            console.log(this.colummQtd);
        }
    },

    beforeMount() {
        this.PullPhotos();
    },
    updated() {
        this.SetColummQtd();
    }
}
</script>

<style>   
    img {
        width: 340px;
        margin-bottom: 28px;
        max-height: 480px;
        cursor: pointer;
    }

    #modalImage{
        width: auto;
    }

    #mosaico {
        margin: 28px 0 0 0;
    }
</style>
