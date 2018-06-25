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
        		    <h3 class="home_page_title caps sub_title">Ball Grid Beat Loader</h3>
        		    <div class="text-center loaders_container">
        		        <div class="loader-inner clearfix ball-grid-beat">
            		        <div></div><div></div><div></div>
            		        <div></div><div></div><div></div>
            		        <div></div><div></div><div></div>
            		    </div>
        		    </div>
        		    <div class="margin_40"></div>
        		    <h3 class="home_page_title caps sub_title">Ball Clip Rotate Loader</h3>
        		    <div class="text-center loaders_container">
        		        <div class="loader-inner clearfix ball-clip-rotate-multiple">
            		        <div></div>
            		        <div></div>
            		    </div>
        		    </div>
        		    <div class="margin_40"></div>
        		    <h1 class="home_page_title caps">Buttons</h1>
        		    <div class="row margin_30 button_examples">
        		        <div class="col-md-3 center">
    		               <button class="animated-btn no_border hvr-border-fade">Click Here</button>
        		        </div>
        		        <div class="col-md-3 center">
    		               <button class=" hvr-outline-out">Click Here</button>
        		        </div>
        		        <div class="col-md-3 center">
        		            <button class="hvr-outline-in"> Click Here </button> 
        		        </div>
        		        <div class="col-md-3 center">
		                    <button class="animated-btn no_border hvr-hollow"> Click Here  </button> 
        		        </div>
        		    </div>
        		    <div class="row margin_30 button_examples">
        		        <div class="col-md-3 center">
        		            <button class="animated-btn no_border hvr-overline-reveal"> Click Here </button> 
        		        </div>
        		        <div class="col-md-3 center">
		                    <button class="animated-btn no_border hvr-underline-reveal"> Click Here</button> 
        		        </div>
        		        <div class="col-md-3 center">
		                    <button class="animated-btn no_border  hvr-underline-from-left"> Click Here</button> 
        		        </div>
        		        <div class="col-md-3 center">
		                    <button class="animated-btn no_border hvr-underline-from-center"> Click Here  </button> 
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
    @import "https://twinpines.codecloudapp.com/animate.css";
   
    .button_examples .animated-btn.no_border {
        border: none;
    }
    .button_examples .hvr-border-fade,.button_examples .hvr-hollow,.button_examples .hvr-trim,.button_examples .hvr-round-corners,.button_examples .hvr-underline-from-center,.button_examples .hvr-underline-from-left,.button_examples .hvr-underline-reveal,.button_examples .hvr-overline-reveal{
        background: #e1e1e1;
    }
    .button_examples .hvr-hollow:hover,.button_examples .hvr-hollow:focus,.button_examples .hvr-hollow:active {
        background: none;
    }
    .button_examples button {
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