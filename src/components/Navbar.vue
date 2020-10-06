<template>
<div id="nav">
    <b-container>
        <b-navbar prop="fixed" toggleable="lg" type="light" id="navbar">
            <b-navbar-brand href="#" id="brand" v-on:click="SetAlbum('0')">Glenio Campregher</b-navbar-brand>
            <b-collapse id="nav-text-collapse" is-nav>
                <b-navbar-nav>
                    <b-nav-text id="sub">Produção Audiovisual.</b-nav-text>
                </b-navbar-nav>
            </b-collapse>

            <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

            <b-collapse id="nav-collapse" is-nav>
                <b-navbar-nav class="ml-auto">
                <b-nav-item href="#" v-on:click="SetAlbum('72157619481635205')">Live</b-nav-item>
                <b-nav-item href="#" v-on:click="SetAlbum('72157594487138743')">Places</b-nav-item>
                <b-nav-item href="#" v-on:click="SetAlbum('72157618896766631')">Things</b-nav-item>
                <b-nav-item href="#" v-on:click="SetAlbum('72157594417127424')">People</b-nav-item>
                <b-nav-item href="#" v-on:click="SetAlbum('72157604951562815')">Chandelier</b-nav-item>
                <b-nav-item href="#" v-on:click="SetAlbum('72157646686687804')">FIT BH 2014</b-nav-item>
                </b-navbar-nav>
            </b-collapse>
        </b-navbar>
    </b-container>
</div>
</template>

<script>

export default {
    name: 'Navbar',
    props:['currentAlbum'],
    methods: {
        SetAlbum(newAlbum){
            this.$emit('updateAlbum',newAlbum)
        }
    }
}
</script>

<style>
    @import url('https://fonts.googleapis.com/css?family=Staatliches&display=swap');

    #nav{
        background-color: #E6EBE0;
    }

    #brand{
        font-size: 30px;
        font-family: 'Staatliches', cursive;
        color: #433633;
    }

    #sub{
        font-size: 12px;
    }
</style>
