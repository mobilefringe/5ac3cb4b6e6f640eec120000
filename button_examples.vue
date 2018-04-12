<template>
    <div> <!-- without an outer container div this component template will not render -->
        <loader v-if="!dataLoaded"></loader>
        <transition name="fade">
            <div v-if="dataLoaded" v-cloak>
        		<div class="site_container">
        		    <div class="row">
        		        <div class="col-md-3">
        		            
        		        </div>
        		        <div class="col-md-3">
        		            <div class="btn btn-slice">Slice</div>    
        		        </div>
        		        <div class="col-md-3">
        		            <div class="btn btn-slice-fill">Slice</div>    
        		        </div>
        		        <div class="col-md-3">
        		            
        		        </div>
        		    </div>
                </div>
            </div>
        </transition>
    </div>
</template>

<style>
    /*.btn {*/
    /*    position: relative;*/
    /*    display: block;*/
    /*    overflow: hidden;*/
    /*    height: 30px;*/
    /*    max-width: 250px;*/
    /*    margin: 1rem auto;*/
    /*    text-transform: uppercase;*/
    /*    border: 1px solid #000;*/
    /*}*/
    /*.btn-slice {*/
    /*    $btn-color: random-color($max:200);*/
    /*    $btn-color-dark: shade($btn-color, 40%);*/
    /*    color: tint($btn-color);*/
    /*    @include triangle(up-right, 0, $btn-color-dark, true);*/
    /*    @include triangle(down-left, 0, $btn-color-dark, true, before);*/
    /*}*/
    /*.btn-slice:before, .btn-slice:after {*/
    /*    content: '';*/
    /*    position: absolute;*/
    /*    width: 0;*/
    /*    height: 0;*/
    /*    border: 0 solid;*/
    /*    transform: rotate(360deg);*/
    /*}*/
    /*.btn-slice:before {*/
    /*    bottom: 0;*/
    /*    left: 0;*/
    /*    border-color: transparent transparent transparent $btn-color-dark;*/
    /*}*/
    /*.btn-slice:after {*/
    /*    top: 0;*/
    /*    right: 0;*/
    /*    border-color: transparent $btn-color-dark transparent transparent;*/
    /*}*/
    /*.btn-slice:hover {*/
    /*    color: tint($btn-color, 75%);*/
    /*}*/
    /*.btn-slice:hover .btn-slice:before, .btn-slice:hover .btn-slice:after {*/
    /*    border-width: $btn-height $btn-width*1.05;*/
    /*}*/
</style>
<script>
    define(["Vue"], function(Vue) {
        return Vue.component("buttons-component", {
            template: template, // the variable template will be injected
            data: function() {
                return {
                    dataLoaded: false,
                    // banners: [
                    //     { "image_url": "http://nikolaywerner.ru/files/2017-02/-nwf9500.jpg", "name": "Slide One", "description": "Description One" },
                    //     { "image_url": "http://nikolaywerner.ru/files/2017-02/-nwf9506.jpg", "name": "Slide Two", "description": "Description Two" },
                    //     { "image_url": "http://nikolaywerner.ru/files/2017-02/-nwf9449.jpg", "name": "Slide Three", "description": "Description Three" },
                    //     { "image_url": "http://nikolaywerner.ru/files/2017-02/-nwf9541.jpg", "name": "Slide Four", "description": "Description Four" }
                    // ],
                    // slickOptions3: {
                    //     arrows: false,
                    //     autoplay: true,
                    //     centerMode: true,
                    //     centerPadding: '5%',
                    //     cssEase:'ease-in-out',
                    //     slidesToShow: 5,
                    // }
                }
            },
            created(){
                // this.loadData().then(response => {
                   this.dataLoaded = true;
                // });
            },
            computed: {

            },
            methods: {
                // loadData: async function() {
                //     try {
                //         let results = await Promise.all([this.$store.dispatch("getData", "repos")]);
                //         return results;
                //     } catch (e) {
                //         console.log("Error loading data: " + e.message);
                //     }
                // }
            }
        });
    });
</script>
