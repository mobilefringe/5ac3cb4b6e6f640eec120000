<template>
    <div> <!-- without an outer container div this component template will not render -->
        <loader v-if="!dataLoaded"></loader>
        <transition name="fade">
            <div v-if="dataLoaded" v-cloak>
        		<div class="site_container">
        		    <div class="margin_40"></div>
        		    <h3 class="home_page_title caps">Ball Beat Loader</h3>
        		    <div class="text-center loaders_container">
        		        <div class="loader-inner ball-beat">
            		        <div></div>
            		        <div></div>
            		        <div></div>
            		    </div>
        		    </div>
        		    <div class="margin_40"></div>
        		    <h3 class="home_page_title caps">Ball Grid Beat Loader</h3>
        		    <div class="text-center loaders_container">
        		        <div class="loader-inner clearfix ball-grid-beat">
            		        <div></div><div></div><div></div>
            		        <div></div><div></div><div></div>
            		        <div></div><div></div><div></div>
            		    </div>
        		    </div>
        		    <div class="margin_40"></div>
        		    <h3 class="home_page_title caps">Ball Pulse Loader</h3>
        		    <div class="text-center loaders_container">
        		        <div class="loader-inner ball-pulse">
            		        <div></div>
            		        <div></div>
            		        <div></div>
            		    </div>
        		    </div>
        		    <div class="margin_40"></div>
        		    <h3 class="home_page_title caps">Line Scale Pulse Loader</h3>
        		    <div class="text-center loaders_container">
        		        <div class="loader-inner clearfix line-scale-pulse-out-rapid">
            		        <div></div>
            		        <div></div>
            		        <div></div>
            		        <div></div>
            		        <div></div>
            		    </div>
        		    </div>
        		    <div class="margin_40"></div>
        		    <h3 class="home_page_title caps">Square Spin Loader</h3>
        		    <div class="text-center loaders_container">
        		        <div class="loader-inner clearfix square-spin">
            		        <div></div>
            		    </div>
        		    </div>
        		    <div class="margin_40"></div>
        		    <h3 class="home_page_title caps">Square Spin Loader (Logo Example 1)</h3>
        		    <div class="text-center loaders_container">
        		        <div class="loader-inner clearfix square-spin logo_example_1">
            		        <div></div>
            		    </div>
        		    </div>
        		    <div class="margin_40"></div>
        		    <h3 class="home_page_title caps">Ball Clip Rotate Loader</h3>
        		    <div class="text-center loaders_container">
        		        <div class="loader-inner clearfix ball-clip-rotate-multiple">
            		        <div></div>
            		        <div></div>
            		    </div>
        		    </div>
                </div>
            </div>
        </transition>
    </div>
</template>
<style>
    @import "https://mmvue.codecloudapp.com/loaders.css";
    .loaders_container {
        background-color: #4f6726;
        padding: 50px;
    }
    .loader-inner  {
        margin:auto;
        text-align: center;
    }
    .square-spin > div {
        margin:auto;
    }
    .square-spin.logo_example_1 > div {
        background-image: url("//codecloud.cdn.speedyrails.net/sites/5ac3cb4b6e6f640eec120000/image/png/1529333770000/twinpineslogo-Square.png");
    }
    .ball-clip-rotate-multiple.clearfix.loader-inner {
        position: absolute;
        left: 50%;
    }
</style>
<script>
    define(["Vue"], function(Vue) {
        return Vue.component("loader-example-component", {
            template: template, // the variable template will be injected
            data: function() {
                return {
                    dataLoaded: false,
                    banners: [
                        { "image_url": "http://nikolaywerner.ru/files/2017-02/-nwf9500.jpg", "name": "Slide One", "description": "Description One" },
                        { "image_url": "http://nikolaywerner.ru/files/2017-02/-nwf9506.jpg", "name": "Slide Two", "description": "Description Two" },
                        { "image_url": "http://nikolaywerner.ru/files/2017-02/-nwf9449.jpg", "name": "Slide Three", "description": "Description Three" },
                        { "image_url": "http://nikolaywerner.ru/files/2017-02/-nwf9541.jpg", "name": "Slide Four", "description": "Description Four" }
                    ],
                    slickOptions3: {
                        arrows: false,
                        autoplay: true,
                        centerMode: true,
                        centerPadding: '5%',
                        cssEase:'ease-in-out',
                        slidesToShow: 5,
                    }
                }
            },
            created(){
                this.loadData().then(response => {
                   this.dataLoaded = true;
                });
            },
            computed: {

            },
            methods: {
                loadData: async function() {
                    try {
                        let results = await Promise.all([this.$store.dispatch("getData", "repos")]);
                        return results;
                    } catch (e) {
                        console.log("Error loading data: " + e.message);
                    }
                }
            }
        });
    });
</script>
