<template>
    <div> <!-- without an outer container div this component template will not render -->
        <loader v-if="!dataLoaded"></loader>
        <transition name="fade">
            <div v-if="dataLoaded" v-cloak class="gem_packages">
                <div class="page_header" v-if="pageBanner" v-bind:style="{ backgroundImage: 'url(' + pageBanner.image_url + ')' }">
        			<div class="site_container">
        				<div class="header_content caps">
        				    <p>{{ $t("stores_page.header_desc") }}</p>
        					<h1>{{ $t("packages.diamond") }}</h1>
        				</div>
        			</div>
        		</div>
        		<div class="site_container">
        		    <h1 class="home_page_title caps">Banners</h1>
        		    
    		        
    		        <h3 class="home_page_title caps sub_title">Silmar Banner</h3>
    		        <silmar-banner :bannerList="banners"></silmar-banner>
    		        
    		        <div class="margin_60 hidden_phone"></div>
    		        <h3 class="home_page_title caps sub_title">Keele Banner</h3>
    		        <keele-banner :banners="banners"></keele-banner>
    		        <h1 class="home_page_title caps">Loaders</h1>
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
    .ball-clip-rotate-multiple.clearfix.loader-inner {
        position: absolute;
        left: 50%;
    }
</style>
<script>
    // gold
    define(["Vue", "vuex", "vue!vue-slick", "vue!edgeley-banner", "vue!chrislea-banner", "vue!weston-banner", "vue!keele-banner", "vue!silmar-banner"], function(Vue, Vuex, slick, edgeleyBanner, chrisleaBanner, westonBanner, keeleBanner, silmarBanner) {
        return Vue.component("diamond-component", {
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