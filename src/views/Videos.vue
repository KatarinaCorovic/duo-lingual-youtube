<template>

<div>

    <!-- <button v-on:click="ds">Serbian</button>
    <button v-on:click="ds">English</button> -->
 
    <h1>{{translations.mainHeading[this.lang]}} ({{ $route.params.lang }})</h1>

    <h2>{{translations.listOfVideos[this.lang]}}</h2>

    <ul>
        <li v-for="(video, index) in videos[this.lang]" v-bind:key="index">
            <img v-on:click="toggleModal(video.id)" v-bind:src="generateThumbnailUrl(video.id)" alt="">
            <h3 v-on:click="toggleModal(video.id)"> 
                {{video.title}}
            </h3>
        </li>
    </ul>

    <div v-on:click="toggleModal" v-show="showModal" id="modal">
        <iframe width="560" height="315" :src="embedVideo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div>
</div>
    
</template>

<script>
export default {
    name: 'Videos',
    data(){
        return{
            lang:this.$route.params.lang,
            showModal:false,
            embedVideo:null,
            cookieObj:null,
            videos:{
                en:[
                        {
                        title: "VIVALDI - Four Seasons - Alexandra Conunova - Orchestre International de Genève",
                        id: "YnDLlajMxyo"
                        },

                        {
                        title: "Tom And Jerry:Santa Lucia",
                        id: "nBEYUphu1v8"
                        },

                        {
                        title: "Hans Zimmer - Time",
                        id: "IQj8e60USMM"
                        },
                            
                    ],
                rs:[
                      {
                        title: "Branimir Štulić 'USNE VRELE VIŠЊE'",
                        id: "Qudotq4Zi1I"
                        },
                        {
                        title: "Neno Belan & Fiumens - RIJEKA SNOVA",
                        id: "qF8CgqrkoC0"
                        },
                        {
                        title: "Rade Serbedzija- Vec sam ti pricao to (1995)",
                        id: "ns1-TyGHt-A"
                        },
                            
                     ]
            },
            translations:{
                mainHeading:{
                    en: 'Welcome to Duo Lingual Yotube',
                    rs: 'Dobrodosli na dvojezicni Youtube'
                },

                listOfVideos: {
                    en: 'List of videos',
                    rs:'Lista klipova'
                }
            },

            translations2:{
                en:{
                    mainHeading:'Welcome to Duo Lingual YouTube',
                    listOfVideos:'List of Videos'
                },
                rs:{
                    mainHeading:'Dobrodosli na dvojezicni YouTube',
                    listOfVideos:'Lista klipova'
                }
            }
        }

    },

methods: {

    toggleModal: function(videoIdOrUrl){
        if(this.showModal === false){
            this.embedVideo = this.generateEmbedUrl(videoIdOrUrl);
            this.showModal = true;
            
        }else{
            this.showModal = false;
            this.embedVideo = null;
        }

    },
    
    /**
     * Expects an argument that is either a youtube URL or a ID,
     * and returns back the ID.
     */
    getIdFromUrl: function(videoIdOrUrl) {
        if (videoIdOrUrl.indexOf('http') === 0) {
            return videoIdOrUrl.split('v=')[1];
        } else {
            return videoIdOrUrl;
        }
    },
    
    /**
     * Expects an argument that is either a youtube URL or a ID,
     * and returns back the URL of the thumbnail for that video.
     */
    generateThumbnailUrl: function(videoIdOrUrl) {
        return 'https://i3.ytimg.com/vi/' + this.getIdFromUrl(videoIdOrUrl) + '/default.jpg';
    },

    /**
     * Expects an argument that is either a youtube URL or a ID,
     * and returns back the URL for that video.
     */
    generateWatchUrl: function(videoIdOrUrl) {
        return 'https://www.youtube.com/watch?v=' + this.getIdFromUrl(videoIdOrUrl);
    },
    
    /**
     * Expects an argument that is either a youtube URL or a ID,
     * and returns back the embed URL for that video.
     */
    generateEmbedUrl: function(videoIdOrUrl) {
        return 'https://www.youtube.com/embed/' + this.getIdFromUrl(videoIdOrUrl);

            }
                              //         changeToEnglish function(){
            
                              //             if()
               //  }   
        },

        mounted(){
            this.cookieObj = new this.$cookie;
            this.cookieObj.create('language', this.$route.params.lang, 10);
            
            
          
        }
        
    }   
</script>

<style lang="scss">

ul{
    padding:0;
    list-style:none;
    width:600px;
    text-align:left;
    margin: 0 auto;

    li{
        border: 1px solid rgb(155, 141, 141);
        margin:20px;
        display:flex;
        align-items: center;
    }

    img{
        max-width: 100%;
        cursor: pointer;
       
    }

    h3{
        margin-left: 23px;
        cursor: pointer;
    }

}

#modal{
    position:fixed;
    top:0;
    left:0;
    height: 100%;
    width:100%;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;

}

</style>