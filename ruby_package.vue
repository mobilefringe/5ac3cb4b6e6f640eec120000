<template>
    <div> <!-- without an outer container div this component template will not render -->
        <loader v-if="!dataLoaded"></loader>
        <transition name="fade">
            <div v-if="dataLoaded" v-cloak class="gem_packages">
                <div class="page_header" v-if="pageBanner" v-bind:style="{ backgroundImage: 'url(' + pageBanner.image_url + ')' }">
        			<div class="site_container">
        				<div class="header_content caps">
        				    <p>{{ $t("stores_page.header_desc") }}</p>
        					<h1>{{ $t("packages.ruby") }}</h1>
        				</div>
        			</div>
        		</div>
        		<div class="site_container">
        		    <h1 class="home_page_title caps">Banners</h1>
        		    
    		        <h3 class="home_page_title caps sub_title">Edgeley Banner</h3>
    		        <edgeley-banner :banners="banners"></edgeley-banner>
    		        <h3 class="home_page_title caps sub_title">Silton Banner</h3>
    		        <silton-banner :banners="banners"></silton-banner>
    		        
    		        <h1 class="home_page_title caps">Loaders</h1>
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
        background-color: transparent;
        width: 60px;
        height: 60px;
    }
    .square-spin.logo_example_2 > div {
        background-image: url("//codecloud.cdn.speedyrails.net/sites/5ac3cb4b6e6f640eec120000/image/png/1529338460509/tplogo_small.png");
        background-color: transparent;
        width: 120px;
        height: 15px;
    }
    .ball-clip-rotate-multiple.clearfix.loader-inner {
        position: absolute;
        left: 50%;
    }
</style>
<script>
    // silver
    define(["Vue", "vuex", "vue!vue-slick", "vue!edgeley-banner", "vue!silton-banner"], function(Vue, Vuex, slick, edgeleyBanner, siltonBanner) {
        return Vue.component("ruby-component", {
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
                    },
                    pageBanner:null
                }
            },
            created(){
                this.loadData().then(response => {
                    this.dataLoaded = true;
                    var temp_repo = this.findRepoByName('Directory Banner').images;
                    if(temp_repo != null) {
                        this.pageBanner = temp_repo[0];
                    } else {
                        this.pageBanner = "http://via.placeholder.com/1920x400/4f6726/4f6726";
                    }
                });
            },
            computed: {
                ...Vuex.mapGetters([
                    'property',
                    'processedStores',
                    'findRepoByName'
                ]),
                allStores() {
                    var store_list = this.processedStores;
                    this.filteredStores = store_list;
                    return store_list
                }
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