<template>
<div>
    <div class="container">
    <div class="row">
        <div class="col-md-12 offset-md-0 bg-custome-semitrans mb-5">
            <br><img :src='musicianProfile.strArtistThumb' class="sizeImg" alt="musician pict"><br>
            <h1 class="mt-0 text-center">{{ musicianProfile.strArtist }}</h1>
            <hr class="my-3 new5">
            <div class="text-center">
                <div class="row justify-content-around">
                    <div class="col-4">
                        <button type="button" class="btn btn-sm btn-dark" @click.prevent="showAlbumModal">ALBUM LIST</button>
                    </div>
                    <div class="col-4">
                        <button type="button" class="btn btn-sm btn-warning" @click.prevent="addFavorite">ADD TO FAVORITE</button>
                        <p v-if="alreadyFavorite === true"><strong>Already in your favorite list</strong></p>
                    </div>
                </div>
                <AlbumModal ref="albumModalComponent" :artistAlbum='artistAlbum'></AlbumModal>
                <hr class="my-2 new1">
            </div>
            <div>
            <div v-if="musicianProfile.strCountry">
                <h3>Country</h3>
                <p class="text-justify">{{ musicianProfile.strCountry }}</p>
                <hr class="my-2 new1">
            </div>
            <div v-if="musicianProfile.intFormedYear && musicianProfile.intMembers > 1">
                <h3>Formed</h3>
                <p class="text-justify">{{ musicianProfile.intFormedYear }}</p>
                <hr class="my-2 new1">
            </div>
            <div v-if="musicianProfile.intBornYear && musicianProfile.intMembers == 1">
                <h3>Born</h3>
                <p class="text-justify">{{ musicianProfile.intBornYear }}</p>
                <hr class="my-2 new1">
            </div>
            <div v-if="musicianProfile.intDiedYear && musicianProfile.intMembers > 1">
                <h3>Disbanded</h3>
                <p class="text-justify">{{ musicianProfile.intDiedYear }}</p>
                <hr class="my-2 new1">
            </div>
            <div v-if="musicianProfile.intDiedYear && musicianProfile.intMembers == 1">
                <h3>Died</h3>
                <p class="text-justify">{{ musicianProfile.intDiedYear }}</p>
                <hr class="my-2 new1">
            </div>
            <div v-if="musicianProfile.strLabel">
                <h3>Label</h3>
                <p class="text-justify">{{ musicianProfile.strLabel }}</p>
                <hr class="my-2 new1">
            </div>
            <div v-if="musicianProfile.strStyle">
                <h3>Style</h3>
                <p class="text-justify">{{ musicianProfile.strStyle }}</p>
                <hr class="my-2 new1">
            </div>
            <div v-if="musicianProfile.strGenre">
                <h3>Genre</h3>
                <p class="text-justify">{{ musicianProfile.strGenre }}</p>
                <hr class="my-2 new1">
            </div>
            <div v-if="musicianProfile.strBiographyEN">
                <h3>Biography</h3>
                <p class="text-justify">{{ musicianProfile.strBiographyEN }}</p>
                <hr class="my-2 new1">
            </div>
            <div v-if="musicianProfile.strWebsite || musicianProfile.strFacebook || musicianProfile.strTwitter">
                <h3>Social Media</h3>
                <p class="text-justify my-0">{{ musicianProfile.strWebsite }}</p>
                <p class="text-justify my-0">{{ musicianProfile.strFacebook }}</p>
                <p class="text-justify my-0">{{ musicianProfile.strTwitter }}</p>
                <hr class="my-2 new1">
            </div>
        </div>
    </div>
</div>
</template>

<script>
import AlbumModal from './AlbumModal'
import axios from 'axios'
export default {
    name: 'MusicianData',
    props: [ 'musicianProfile', 'alreadyFavorite' ],
    components : {
        AlbumModal
    },
    data () {
        return {
            artistAlbum: {
                id: '',
                name: ''
            },
            musicianName: ''
        }
    },
    methods : {
        showAlbumModal() {
            this.artistAlbum.id = this.musicianProfile.idArtist
            this.artistAlbum.name = this.musicianProfile.strArtist
            this.$refs.albumModalComponent.showAlbum()
        },
        addFavorite() {
            this.musicianName = this.musicianProfile.strArtist
            this.$emit('addFavorite', this.musicianName)
        }
    }
}
</script>

<style>
    .bg-custome-semitrans{
        background-color: rgba(245, 245, 245, 0.87);
    }
    .sizeImg {
        display: block;
        margin: 0 auto;
        width: 40%;
    }
    hr.new5 {
        border: 2px solid rgb(81, 84, 81);
        border-radius: 5px;
    }
    hr.new1 {
        border-top: 1px dashed rgb(81, 84, 81);
    }
</style>