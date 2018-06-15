<template>
    <div> <!-- without an outer container div this component template will not render -->
        <loader v-if="!dataLoaded"></loader>
        <transition name="fade">
            <div v-if="dataLoaded" v-cloak>
        		<div class="site_container">
        		<div class="margin_40"></div>
        		    <h3 class="home_page_title caps">2D Transitions</h3>
        		    
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
        		    <div class="margin_40"></div>
        		    <h3 class="home_page_title caps">Background Transitions</h3>
        		    
        		    <!--<div class="row margin_30">-->
                    <!--          <div class="col-md-3 center">-->
        		    <!--        <button class="animated-btn btn-fill-vert"> Click Here </button>    -->
        		    <!--    </div>-->
        		    <!--    <div class="col-md-3 center">-->
        		    <!--        <button class="animated-btn btn-fill-vert fill"> Click Here </button>-->
        		    <!--    </div>-->
        		    <!--    <div class="col-md-3 center">-->
        		    <!--        <button class="animated-btn btn-fill-horz"> Click Here </button>    -->
        		    <!--    </div>-->
        		    <!--    <div class="col-md-3 center">-->
        		    <!--        <button class="animated-btn btn-fill-horz fill"> Click Here </button>-->
        		    <!--    </div>-->
        		    <!--</div>-->
        		    
        		    <div class="row margin_30">
                        <div class="col-md-3 center">
        		            <button class="animated-btn hvr-sweep-to-right"> Click Here </button>    
        		        </div>
        		        <div class="col-md-3 center">
        		            <button class="animated-btn hvr-sweep-to-bottom"> Click Here </button>
        		        </div>
        		        <div class="col-md-3 center">
        		            <button class="animated-btn hvr-shutter-out-horizontal"> Click Here </button>         
        		        </div>
        		        <div class="col-md-3 center">
	                        <button class="animated-btn hvr-shutter-out-vertical"> Click Here </button> 
        		        </div>
        		    </div>
        		    <div class="row margin_30">
        		        <div class="col-md-3 center">
	                        <button class="animated-btn hvr-fade"> Click Here </button> 
        		        </div>
        		        <div class="col-md-3 center">
        		            <button class="animated-btn hvr-bounce-to-right"> Click Here </button>   
        		        </div>
        		        <div class="col-md-3 center">
    		                <button class="animated-btn hvr-bounce-to-top"> Click Here </button>       
        		        </div>
        		        <div class="col-md-3 center">
	                        <button class="animated-btn hvr-rectangle-out"> Click Here </button> 
        		        </div>
        		    </div>
        		    <!--<div class="row margin_30">-->
        		    <!--    <div class="col-md-3 center">-->
		            <!--        <button class="animated-btn hvr-radial-out"> Click Here </button> -->
        		    <!--    </div>-->
        		    <!--    <div class="col-md-3 center">-->
        		    <!--        <button class="animated-btn hvr-radial-in"> Click Here </button>         -->
        		    <!--    </div>-->
        		    <!--    <div class="col-md-3 center">-->
        		    <!--        <button class="animated-btn hvr-rectangle-in"> Click Here </button>   -->
        		    <!--    </div>-->
        		    <!--    <div class="col-md-3 center">-->
	             <!--           <button class="animated-btn hvr-rectangle-out"> Click Here </button> -->
        		    <!--    </div>-->
        		    <!--</div>-->
        		    <!--<div class="row margin_30">-->
        		    <!--    <div class="col-md-3 center">-->
		            <!--        <button class="animated-btn hvr-shutter-in-horizontal"> Click Here </button> -->
        		    <!--    </div>-->
        		    <!--    <div class="col-md-3 center">-->
        		    <!--        <button class="animated-btn hvr-sweep-to-left"> Click Here </button>-->
        		    <!--    </div>-->
        		    <!--    <div class="col-md-3 center">-->
        		    <!--        <button class="animated-btn hvr-sweep-to-top"> Click Here </button>-->
        		    <!--    </div>-->
        		        <!--<div class="col-md-3 center">-->
        		        <!--    <button class="animated-btn hvr-shutter-out-horizontal"> Click Here </button>         -->
        		        <!--</div>-->
        		        <!--<div class="col-md-3 center">-->
        		        <!--    <button class="animated-btn hvr-shutter-in-vertical"> Click Here </button>   -->
        		        <!--</div>-->
        		        <!--<div class="col-md-3 center">-->
	                 <!--       <button class="animated-btn hvr-shutter-out-vertical"> Click Here </button> -->
        		        <!--</div>-->
        		    <!--</div>-->
        		    <!--<div class="row margin_30">-->
        		    <!--    <div class="col-md-3 center">-->
        		    <!--        <button class="animated-btn swing_in"> Click Here </button>   -->
        		    <!--    </div>-->
        		    <!--    <div class="col-md-3 center">-->
	             <!--           <button class="animated-btn btn-border"> Click Here </button> -->
        		    <!--    </div>-->
        		    <!--    <div class="col-md-3 center">-->
        		    <!--        <button class="animated-btn hvr-back-pulse"> Click Here </button> -->
        		    <!--    </div>-->
        		    <!--    <div class="col-md-3 center">-->
	             <!--           <button class="animated-btn hvr-bounce-to-left"> Click Here </button> -->
        		    <!--    </div>-->
        		    <!--    <div class="col-md-3 center">-->
        		    <!--       <button class="animated-btn hvr-bounce-to-bottom"> Click Here </button>          -->
        		    <!--    </div>-->
        		    <!--</div>-->
        		    <h3 class="home_page_title caps">Icon Transitions</h3>
        		    <div class="row margin_30">
        		        <!--<div class="col-md-3 center">-->
    		            <!--   <button class="animated-btn text-slide" data-hover="Send!"><div><i class="fa fa-arrow-right"></i></div></button>-->
        		        <!--</div>-->
        		        <div class="col-md-3 center">
        		            <button class="animated-btn hvr-icon-fade"> Click Here  <i class="fa fa-tags hvr-icon" style="margin-left:5px;"></i></button> 
        		        </div>
        		        <div class="col-md-3 center">
		                    <button class="animated-btn hvr-icon-forward"> Click Here  <i class="fa fa-chevron-right hvr-icon" style="margin-left:5px;"></i></button> 
        		        </div>
        		        <div class="col-md-3 center">
        		            <button class="animated-btn hvr-icon-push"> Click Here  <i class="fa fa-star hvr-icon" style="margin-left:5px;"></i></button> 
        		        </div>
        		        <div class="col-md-3 center">
		                    <button class="animated-btn hvr-icon-rotate">Click Here <i class="fa fa-tags hvr-icon" style="margin-left:5px;"></i></button> 
        		        </div>
        		        
        		    </div>
        		    <div class="row margin_30">
        		        <div class="col-md-3 center">
        		            <button class="animated-btn hvr-icon-float"> Click Here  <i class="fa fa-tags hvr-icon" style="margin-left:5px;"></i></button> 
        		        </div>
        		        <div class="col-md-3 center">
		                    <button class="animated-btn hvr-icon-grow-rotate"> Click Here  <i class="fa fa-star hvr-icon" style="margin-left:5px;"></i></button> 
        		        </div>
        		        <div class="col-md-3 center">
        		            <button class="animated-btn hvr-icon-pop"> Click Here  <i class="fa fa-star hvr-icon" style="margin-left:5px;"></i></button> 
        		        </div>
        		        <div class="col-md-3 center">
		                    <button class="animated-btn hvr-icon-bob">Click Here <i class="fa fa-tags hvr-icon" style="margin-left:5px;"></i></button> 
        		        </div>
        		        
        		    </div>
        		    <h3 class="home_page_title caps">Border Transitions</h3>
        		    <div class="row margin_30">
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
        		    <div class="row margin_30">
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
    @import "//codecloud.cdn.speedyrails.net/sites/5ac3cb4b6e6f640eec120000/text/css/1522155272000/hover.css";
    
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
