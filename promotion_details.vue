<template>
    <div> <!-- without an outer container div this component template will not render -->
        <loader v-if="!dataLoaded"></loader>
        <transition name="fade">
            <div v-if="dataLoaded" v-cloak>
        		<div class="site_container page_content">
        		    <div class="margin_60"></div>
        			<div id="promos_container">
    					<div class="promo_container">
    					    <div class="promo_content center">
    					        <p class="promo_title" v-if="currentPromo.store">{{ currentPromo.store.name }}</p>
    					        <p class="promo_title" v-else>{{ property.name }}</p>
    					        <h3 class="margin_60" v-if="locale=='en-ca'">{{ currentPromo.name }}</h3>
    							<h3 class="margin_60" v-else>{{ currentPromo.name_2 }}</h3>
    							<p class="promo_desc">
    							    {{ currentPromo.start_date | moment("MMM D", timezone) }} - {{ currentPromo.end_date | moment("MMM D", timezone) }}
    							</p>
    					    </div>
    					    <div class="promo_img" v-if="locale=='en-ca'" v-lazy:background-image="currentPromo.image_url"></div>
    					    <div class="promo_img" v-else v-lazy:background-image="currentPromo.promo_image2_url_abs"></div>
    					    <div class="promo_details_desc">
            				    <div v-if="locale=='en-ca'" v-html="currentPromo.rich_description"></div>
            				    <div v-else v-html="currentPromo.rich_description_2"></div>
            				</div>
            				<div class="promo_details_share">
            				    <social-sharing v-if="currentPost" :url="shareURL(currentPromo.slug)" :title="currentPromo.title" :description="currentPromo.body" :quote="truncate(currentPromo.body)" twitter-user="NorthParkCenter" :media="currentPromo.image_url" inline-template>
                                    <div class="blog-social-share">
                                        <network network="facebook">
                                            <i class="fa fa-facebook-square"></i>
                                        </network>
                                        <network network="twitter">
                                            <i class="fa fa-twitter-square"></i>
                                        </network>
                                        <network network="pinterest">
                                            <i class="fa fa-pinterest-square"></i>
                                        </network>
                                        <h5>Share</h5>
                                    </div>
                                </social-sharing>
            				</div>
    					</div>
        			</div>
		        </div>
		    </div>
		</transition>
	</div>
</template>

<script>
    define(['Vue', 'vuex', 'moment', 'vue-lazy-load', 'vue-social-sharing'], function(Vue, Vuex, moment, VueLazyload, SocialSharing) {
        Vue.use(VueLazyload);
        return Vue.component("promo-details-component", {
            template: template, // the variable template will be injected,
            props:['id', 'locale'],
            data: function() {
                return {
                    dataLoaded: false,
                    currentPromo: null
                }
            },
            beforeRouteUpdate(to, from, next) {
                this.currentPromo = this.findPromoBySlug(to.params.id);
                    if (this.currentPromo === null || this.currentPromo === undefined){
                        this.$router.replace({ name: '404'});
                    }
                next();
                this.dataLoaded = true;
            },
            created(){
                this.loadData().then(response => {
                    this.updateCurrentPromo(this.id);
                    this.dataLoaded = true;
                });
            },
            watch: {
                currentPromo : function (){
                    if (this.currentPromo != null && this.currentPromo != undefined) {
                        if(_.includes(this.currentPromo.image_url, 'missing')) {
                            this.currentPromo.image_url = "http://via.placeholder.com/1560x800/757575";
                        }
                        if(_.includes(this.currentPromo.promo_image2_url_abs, 'missing')) {
                            this.currentPromo.promo_image2_url_abs = "http://via.placeholder.com/1560x800/757575";
                        }
                    }
                }
            },
            computed: {
                ...Vuex.mapGetters([
                    'property',
                    'timezone',
                    'processedPromos',
                    'findPromoBySlug',
                    'findPromoById'
                ])
            },
            methods: {
                updateCurrentPromo (id) {
                    this.currentPromo = this.findPromoBySlug(id);
                    if (this.currentPromo === null || this.currentPromo === undefined){
                        this.$router.replace({ name: '404'});
                    }
                },
                loadData: async function() {
                    try {
                        // avoid making LOAD_META_DATA call for now as it will cause the entire Promise.all to fail since no meta data is set up.
                        let results = await Promise.all([this.$store.dispatch("getData", "promotions")]);
                    } catch (e) {
                        console.log("Error loading data: " + e.message);
                    }
                }
            }
        });
    });
</script>