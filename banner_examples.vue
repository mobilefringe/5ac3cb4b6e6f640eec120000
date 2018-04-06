<template>
    <div> <!-- without an outer container div this component template will not render -->
        <loader v-if="!dataLoaded"></loader>
        <transition name="fade">
            <div v-if="dataLoaded" v-cloak>
        		<div class="site_container">
        		    <div class="margin_60 hidden_phone"></div>
                    <div>
        		        <h3 class="home_page_title caps">{{$t("home_page.twitter_feed")}}</h3>
        		    </div>
        		    <div>
        		        <slick ref="slick" :options="slickOptions">
        					<div class="" v-for="banner in banners" v-if="banners">
        						<div class="home_banner" v-bind:style="{ backgroundImage: 'url(' + banner.image_url + ')' }"></div>
        					</div>
        				</slick>
        		    </div>
                </div>
            </div>
        </transition>
    </div>
</template>

<script>
    define(["Vue", "vuex", "vue!twitter-slider"], function(Vue, Vuex, TwitterSlider) {
        return Vue.component("banners-component", {
            template: template, // the variable template will be injected
            data: function() {
                return {
                    dataLoaded: false,
                    banners: [{
                        "image_url", "http://nikolaywerner.ru/files/2017-02/-nwf9500.jpg"
                    }]
                    
                }
            },
            created(){
                this.loadData().then(response => {
                   this.dataLoaded = true;
                });
            },
            computed: {
                ...Vuex.mapGetters([
                    'property',
                    'timezone'
                ]),
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
