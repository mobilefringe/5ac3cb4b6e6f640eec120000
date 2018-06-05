<template>
    <div> <!-- without an outer container div this component template will not render -->
        <loader v-if="!dataLoaded"></loader>
        <transition name="fade">
            <div v-if="dataLoaded" v-cloak>
        		<div class="site_container">
        		    <div class="margin_60 hidden_phone"></div>
    		        <h3 class="home_page_title caps">Edgeley Banner</h3>
    		        <edgeley-banner :banners="banners"></edgeley-banner>

        		    <div class="margin_60 hidden_phone"></div>
    		        <h3 class="home_page_title caps">Chrislea Banner</h3>
    		        <chrislea-banner :banners="banners"></chrislea-banner>
    		        
        		    <div class="margin_60 hidden_phone"></div>
    		        <h3 class="home_page_title caps">Weston Banner</h3>
    		        <weston-banner :banners="banners"></weston-banner>
    		        
    		        <div class="margin_60 hidden_phone"></div>
    		        <h3 class="home_page_title caps">Keele Banner</h3>
    		        <keele-banner :banners="banners"></keele-banner>
    		        
    		        <div class="margin_60 hidden_phone"></div>
    		        <h3 class="home_page_title caps">Silmar Banner</h3>
    		        <silmar-banner :bannerList="banners"></silmar-banner>
    		        
        		    <div class="margin_60 hidden_phone"></div>
    		        <h3 class="home_page_title caps">Store Logo Scroll</h3>
        		    <div class="banners banner_option_3">
        		        <slick ref="slick" :options="slickOptions3" key="banners3">
        					<div class="" v-for="store in allStores" v-if="allStores">
        					    <div class="slide">
        					        <img :src="store.store_front_url_abs" alt="" />
    					            <p>{{ store.name }}</p>    
        					    </div>
        					</div>
        				</slick>
        		    </div>
                </div>
            </div>
        </transition>
    </div>
</template>

<script>
// bronze
    define(["Vue", "vuex", "vue!vue-slick", "vue!edgeley-banner", "vue!chrislea-banner", "vue!weston-banner", "vue!keele-banner", "vue!silmar-banner"], function(Vue, Vuex, slick, edgeleyBanner, chrisleaBanner, westonBanner, keeleBanner, silmarBanner) {
        return Vue.component("banners-component", {
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
                ...Vuex.mapGetters([
                    'processedStores'
                ]),
                allStores() {
                    var store_list = this.processedStores
                    // var vm = this;
                    // var hover_image = "";
                    // _.forEach(store_list, function(value, key) {
                    //     if(value.assets != undefined){
                    //         //Stores JSON
                    //         var store_id = value.id
                    //         vm.$store.dispatch('LOAD_PAGE_DATA', { url: vm.property.mm_host + "/api/v4/thegateway/stores/" + store_id + "/store_files.json" }).then(response => {
                    //             if(response.data != undefined) {
                    //                 hover_image = response.data.store_files[0].url
                    //                 value.hover_img = 'https://www.mallmaverick.com' + hover_image
                    //                 vm.filteredStores = null;
                    //                 vm.filteredStores = store_list; 
                    //                 vm.filteredStores[key].hover_img = 'https://www.mallmaverick.com' + hover_image
                    //             }
                    //         }, error => {
                    //             console.error("Could not retrieve data from server. Please check internet connection and try again.");
                    //             vm.$router.replace({ name: 'home' });
                    //         });
                    //     }    
                    // });
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