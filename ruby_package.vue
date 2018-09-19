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
    		        <div class="row margin_40">
    		            <div class="col-md-12">
    		                <h1 class="home_page_title caps">Loaders</h1>    
    		            </div>
    		            <div class="col-md-12">
        		            <h3 class="home_page_title caps sub_title">Ball Grid Beat Loader</h3>
                		    <div class="text-center loaders_container">
                		        <div class="loader-inner clearfix ball-grid-beat">
                    		        <div></div><div></div><div></div>
                    		        <div></div><div></div><div></div>
                    		        <div></div><div></div><div></div>
                    		    </div>
                		    </div>
                		 </div>
        		        <div class="col-md-12">
        		            <h3 class="home_page_title caps sub_title">Ball Clip Rotate Loader</h3>
                		    <div class="text-center loaders_container">
                		        <div class="loader-inner clearfix ball-clip-rotate-multiple">
                    		        <div></div>
                    		        <div></div>
                    		    </div>
                		    </div>
                	    </div>
            		</div>
        		    <div class="margin_40"></div>
        		    <h1 class="home_page_title caps">Buttons</h1>
        		    <div class="row margin_30 button_examples">
        		        <div class="col-md-3 center">
    		               <button class="animated-btn no_border hvr-border-fade">Full Border</button>
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
        		            <button class="animated-btn no_border hvr-overline-reveal">Border Top</button> 
        		        </div>
        		        <div class="col-md-3 center">
		                    <button class="animated-btn no_border hvr-underline-reveal">Border Bottom</button> 
        		        </div>
        		        <div class="col-md-3 center">
		                    <button class="animated-btn no_border  hvr-underline-from-left">Border Left</button> 
        		        </div>
        		        <div class="col-md-3 center">
		                    <button class="animated-btn no_border hvr-underline-from-center">Border Center</button> 
        		        </div>
        		    </div>
        		    <div class="margin_40"></div>
        		    <h1 class="home_page_title caps">Feature Items</h1>
        		    
        		    <h3 class="home_page_title caps text-left sub_title">Mouse tracking hover</h3>
        		    <div class="text-center ">
        		        <tracking-image-hover :featureItems="feature_items"></tracking-image-hover>
        		    </div>
        		    <h3 class="home_page_title caps text-left sub_title">Mouse tracking hover</h3>
        		    <div id="feature_item_three">
        		        <div class="col-sm-4" v-for="feature in feature_items2">
    		               <div class="wrapper" >
                                <img :src="feature.image_url" />
                                <div id="title">
                                    <h3>{{feature.name}}</h3>
                                    <!--<h2>IPSUM</h2>-->
                                </div>
                                <div id="border-left"></div>
                                <div id="border-bottom"></div>
                                <div id="content">
                                    <p>{{feature.description}}</p>
                                </div>
                            </div>
        		        </div>
            		    
                    </div>
                </div>
            </div>
        </transition>
    </div>
</template>
<style>
    @import "https://mmvue.codecloudapp.com/loaders.css";
    @import "https://twinpines.codecloudapp.com/animate.css";
    
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
        min-width: 100%;
        height: 60px;
        position: relative;
         overflow: hidden; 
        outline: none;
         border: 3px solid #4f6726; 
        background: #e1e1e1;
        color: #4f6726;
        text-transform: uppercase;
        border: none;
    }
    #feature_item_three{
        position: relative;
        min-height: 250px;
    }
    #feature_item_three .wrapper {
        position: absolute;
        left: 50%;
        top: 5%;
        margin-left: -175px;
        width: 350px;
        height: 250px;
        overflow: hidden;
        cursor: pointer;
    }
    #feature_item_three .wrapper img {
      width: 100%;
      height: 250px;
      opacity: 0.75;
      -webkit-transition: all 0.25s ease;
      transition: all 0.25s ease;
    }
    #feature_item_three #title {
        position: absolute;
        top: 50%;
        left: 50%;
        margin-top: 20px;
        margin-left: -125px;
    }
    #feature_item_three #title h3 {
      font-size: 22px;
      text-align: center;
      line-height: 100%;
      color: #fff;
      letter-spacing: 1.1px;
    }
    #feature_item_three #title h2 {
      font-size: 18px;
      padding: 4px;
      text-align: center;
      line-height: 100%;
      background: #fff;
      color: #1a1a1a;
      margin-top: -20px;
      letter-spacing: 1.1px;
    }
    #feature_item_three #border-left {
      width: 3px;
      height: 0px;
      background: #fff;
      z-index: 2;
      position: absolute;
      left: 45px;
      top: 0;
      -webkit-transition: all 0.25s ease;
      transition: all 0.25s ease;
    }
    #feature_item_three #border-bottom {
      width: 0px;
      height: 3px;
      background: #fff;
      z-index: 2;
      position: absolute;
      bottom: 45px;
      left: 0px;
      -webkit-transition: all 0.25s ease;
      transition: all 0.25s ease;
    }
    #feature_item_three #content {
      position: absolute;
      bottom: 0;
      left: 45px;
      overflow: hidden;
      vertical-align: middle;
      display: table;
      text-align: center;
      height: 50px;
      color: #fff;
      opacity: 0;
      -webkit-transition: all 0.25s ease;
      transition: all 0.25s ease;
    }
    #feature_item_three #content p {
      vertical-align: middle;
      line-height: 100%;
      display: table-cell;
      overflow: hidden;
      width: 305px;
      padding-left: 2px;
      padding-right: 2px;
      box-sizing: border-box;
      font-size: 14px;
      letter-spacing: 1.1px;
    }
    #feature_item_three .wrapper:hover > img {
      opacity: 0.25;
    }
    #feature_item_three .wrapper:hover > #border-left {
      height: 400px;
    }
    #feature_item_three .wrapper:hover > #border-bottom {
      width: 400px;
      -webkit-transition-delay: 0.25s;
      transition-delay: 0.25s;
    }
    #feature_item_three .wrapper:hover > #content {
      opacity: 1;
      -webkit-transition-delay: 0.5s;
      transition-delay: 0.5s;
    }

</style>
<script>
    // silver
    define(["Vue", "vuex", "vue!vue-slick", "vue!edgeley-banner", "vue!silton-banner", "vue!tracking-image-hover"], function(Vue, Vuex, slick, edgeleyBanner, siltonBanner, trackingImageHover) {
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
                    pageBanner:null,
                    
                    feature_items: [
                        { "image_url": "//codecloud.cdn.speedyrails.net/sites/5ac3cb4b6e6f640eec120000/image/jpeg/1537283943000/1.jpg", "name": "Promotions", "description": "Description One" },
                        { "image_url": "//codecloud.cdn.speedyrails.net/sites/5ac3cb4b6e6f640eec120000/image/jpeg/1537283943000/2.jpg", "name": "Events", "description": "Description Two" },
                        { "image_url": "//codecloud.cdn.speedyrails.net/sites/5ac3cb4b6e6f640eec120000/image/jpeg/1537283943000/3.jpg", "name": "Contest", "description": "Enter to Win!" }
                    ],
                    feature_items2: [
                        { "image_url": "https://unsplash.it/1000/980?image=943", "name": "Promotions", "description": "Description One" },
                        { "image_url": "https://unsplash.it/1000/980?image=944", "name": "Events", "description": "Description Two" },
                        { "image_url": "https://unsplash.it/1000/980?image=945", "name": "Contest", "description": "Enter to Win!" }
                    ],
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