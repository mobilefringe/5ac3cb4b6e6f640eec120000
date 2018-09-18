<template>
    <div> <!-- without an outer container div this component template will not render -->
        <loader v-if="!dataLoaded"></loader>
        <transition name="fade">
            <div v-if="dataLoaded" v-cloak class="gem_packages">
                <div class="page_header" v-if="pageBanner" v-bind:style="{ backgroundImage: 'url(' + pageBanner.image_url + ')' }">
        			<div class="site_container">
        				<div class="header_content caps">
        				    <p>{{ $t("stores_page.header_desc") }}</p>
        					<h1>{{ $t("packages.sapphire") }}</h1>
        				</div>
        			</div>
        		</div>
        		<div class="site_container">
        		    <h1 class="home_page_title caps">Banners</h1>
        		    
    		        <h3 class="home_page_title caps text-left sub_title">Chrislea Banner</h3>
    		        <chrislea-banner :banners="banners" :key="1"></chrislea-banner>
    		        
        		    <div class="margin_60 hidden_phone"></div>
    		        <h3 class="home_page_title caps sub_title">Weston Banner</h3>
    		        <weston-banner :banners="banners" :key="2"></weston-banner>
    		        
    		        <h1 class="home_page_title caps">Button Transitions</h1>
    		        <div class="row margin_30">
                        <div class="col-md-3 center">
        		            <button class="animated-btn hvr-grow"> Click Here </button>    
        		        </div>
        		        <div class="col-md-3 center">
        		            <button class="animated-btn hvr-shrink"> Click Here </button>
        		        </div>
        		        <div class="col-md-3 center">
        		            <button class="animated-btn hvr-float"> Click Here </button>    
        		        </div>
        		        <div class="col-md-3 center">
        		            <button class="animated-btn hvr-bob"> Click Here </button>
        		        </div>
        		    </div>
        		    <div class="row margin_30">
                        <div class="col-md-3 center">
        		            <button class="animated-btn hvr-forward"> Click Here </button>    
        		        </div>
        		        <div class="col-md-3 center">
        		            <button class="animated-btn hvr-backward"> Click Here </button>
        		        </div>
        		        <div class="col-md-3 center">
        		            <button class="animated-btn hvr-rotate"> Click Here </button>    
        		        </div>
        		        <div class="col-md-3 center">
        		            <button class="animated-btn hvr-wobble-horizontal"> Click Here </button>
        		        </div>
        		    </div>
        		    <h1 class="home_page_title caps">Loaders</h1>
        		    <h3 class="home_page_title caps text-left sub_title">Ball Beat Loader</h3>
        		    <div class="text-center loaders_container">
        		        <div class="loader-inner ball-beat">
            		        <div></div>
            		        <div></div>
            		        <div></div>
            		    </div>
        		    </div>
        		    <div class="margin_40"></div>
        		    <h3 class="home_page_title caps text-left sub_title">Ball Pulse Loader</h3>
        		    <div class="text-center loaders_container">
        		        <div class="loader-inner ball-pulse">
            		        <div></div>
            		        <div></div>
            		        <div></div>
            		    </div>
        		    </div>
        		    <h1 class="home_page_title caps">Feature Items</h1>
        		    
        		    <div class="row margin_30 button_examples">
        		        <div class="col-md-12">
        		             <h3 class="home_page_title caps sub_title">Animate with Drop Shadow</h3>
        		        </div>
        		        <div v-if="feature_items" v-for="item in feature_items" class="col-md-4 center">
        		            <a :href="item.url" target="_blank">
                                <div class="card">
                        		    <div class="card-image" v-bind:style="{ backgroundImage: 'url(' + item.image_url + ')' }"></div>
                        		    <span class="card-description">
                        		        <h3>{{ item.name }}</h3>
                        			    <p>{{ item.description }}</p>    
                        		    </span>
                        	    </div>
                            </a>
        		        </div>
        		    </div>
        		    
        		    <div class="row margin_30 button_examples">
        		        <div class="col-md-12">
        		            <h3 class="home_page_title caps sub_title">Rotate & Scale Image</h3>
        		        </div>
        		        <div v-if="feature_items" v-for="item in feature_items" class="col-md-4 center">
        		            <a href="#">
            		            <figure class="snip1581">
            		                <img :src="item.image_url" alt="profile-sample2"/>
                                    <figcaption>
                                        <h3 class="title1">{{ item.name }}</h3>
                                        <p class="title2">{{ item.description }}</p>
                                    </figcaption>
                                </figure>
                            </a>
                        </div>
                    </div>
                </div>
            </div>
        </transition>
    </div>
</template>
<style>
    @import "/hover.css";
    @import "https://mmvue.codecloudapp.com/loaders.css";
    .animated-btn.no_border {
        border: none;
    }
    .hvr-border-fade, .hvr-hollow, .hvr-trim, .hvr-round-corners, .hvr-underline-from-center, .hvr-underline-from-left, .hvr-underline-reveal, .hvr-overline-reveal{
        background: #e1e1e1;
    }
    button.animated-btn {
        padding: 12px 50px;
        min-width: 200px;
        height: 60px;
        position: relative;
        /* overflow: hidden; */
        outline: none;
        /* border: 3px solid #4f6726; */
        background: #e1e1e1;
        color: #4f6726;
        text-transform: uppercase;
        border: none;
    }
   
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
    // bronze
    define(["Vue", "vuex", "vue!vue-slick", "vue!edgeley-banner", "vue!chrislea-banner", "vue!weston-banner", "vue!keele-banner", "vue!silmar-banner", "vue!tracking-image-hover"], function(Vue, Vuex, slick, edgeleyBanner, chrisleaBanner, westonBanner, keeleBanner, silmarBanner, trackingImageHover) {
        return Vue.component("sapphire-component", {
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
                    feature_items: [
                        { "image_url": "//codecloud.cdn.speedyrails.net/sites/5ac3cb4b6e6f640eec120000/image/jpeg/1537283943000/1.jpg", "name": "Promotions", "description": "Description One" },
                        { "image_url": "//codecloud.cdn.speedyrails.net/sites/5ac3cb4b6e6f640eec120000/image/jpeg/1537283943000/2.jpg", "name": "Events", "description": "Description Two" },
                        { "image_url": "//codecloud.cdn.speedyrails.net/sites/5ac3cb4b6e6f640eec120000/image/jpeg/1537283943000/3.jpg", "name": "Contest", "description": "Enter to Win!" }
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