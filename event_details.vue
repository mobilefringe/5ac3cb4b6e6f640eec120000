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
    					        <p class="promo_title">{{ $t("events_page.events") }}</p>
    					        <h3 class="margin_60" v-if="locale=='en-ca'">{{ currentEvent.name }}</h3>
    							<h3 class="margin_60" v-else>{{ currentEvent.name_2 }}</h3>
    							<p class="promo_desc">
    							    {{ currentEvent.start_date | moment("MMM D", timezone) }} - {{ currentEvent.end_date | moment("MMM D", timezone) }}
    							</p>
    					    </div>
    					    <div class="promo_img" v-if="locale=='en-ca'" v-lazy:background-image="currentEvent.image_url"></div>
    					    <div class="promo_img" v-else v-lazy:background-image="currentEvent.event_image2_url_abs"></div>
    					    <div class="promo_details_desc">
            				    <div v-if="locale=='en-ca'" v-html="currentEvent.rich_description"></div>
            				    <div v-else v-html="currentEvent.rich_description_2"></div>
            				</div>
            				<div class="promo_details_share">
            				    <social-sharing v-if="currentEvent" :url="shareURL(currentEvent.slug)" :title="currentEvent.title" :description="currentEvent.body" :quote="truncate(currentEvent.body)" :media="currentEvent.image_url" inline-template>
                                    <div class="margin_20 details_share_container">
                                        <span>Share On: </span>
                                        <network network="facebook">
                                            <i class="fab fa-facebook-square"></i>
                                        </network>
                                        <network network="twitter">
                                            <i class="fab fa-twitter"></i>
                                        </network>
                                    </div>
                                </social-sharing>
                                <div v-if="currentEvent.promotionable_type == 'Store'">
                                    <a v-if="currentEvent.store.phone" :href="'tel:' + currentEvent.store.phone" target="_blank">
                				        <div class="promo_details_store_btn animated_btn swing_in">{{currentEvent.store.phone}}</div>
                				    </a>
                                    <router-link :to="'/stores/'+ currentEvent.store.slug" >
    							        <div class="promo_details_store_btn animated_btn swing_in">{{ $t("promos_page.visit_store") }}</div>
    					            </router-link>
					            </div>
					            <div v-else>
					                
					            </div>
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
        return Vue.component("event-details-component", {
            template: template, // the variable template will be injected,
            data: function() {
                return {
                    dataLoaded: false,
                    currentEvent: null,
                }
            },
            props:['id', 'locale'],
            beforeRouteUpdate(to, from, next) {
                this.currentEvent = this.findEventBySlug(to.params.id);
                    if (this.currentEvent === null || this.currentEvent === undefined){
                        this.$router.replace({ name: '404'});
                    }
                next();
            },
            created(){
                this.loadData().then(response => {
                    this.updatecurrentEvent(this.id);
                    this.dataLoaded = true;
                });
            },
            watch: {
                currentEvent : function (){
                    if (this.currentEvent != null && this.currentEvent != undefined) {
                        if(_.includes(this.currentEvent.image_url, 'missing')) {
                            this.currentEvent.image_url = "http://via.placeholder.com/1560x800/757575";
                        }
                        if(_.includes(this.currentEvent.event_image2_url_abs, 'missing')) {
                            this.currentEvent.event_image2_url_abs = "http://via.placeholder.com/1560x800/757575";
                        }
                    }
                }
            },
            computed: {
                ...Vuex.mapGetters([
                    'property',
                    'timezone',
                    'processedEents',
                    'findEventBySlug'
                ])
            },
            methods: {
                updatecurrentEvent (id) {
                    this.currentEvent = this.findEventBySlug(id);
                    if (this.currentEvent === null || this.currentEvent === undefined){
                        this.$router.replace({ name: '404'});
                    }
                },
                loadData: async function() {
                    try {
                        // avoid making LOAD_META_DATA call for now as it will cause the entire Promise.all to fail since no meta data is set up.
                        let results = await Promise.all([this.$store.dispatch("getData", "events")]);
                    } catch (e) {
                        console.log("Error loading data: " + e.message);
                    }
                },
                shareURL(slug) {
                    var share_url = "http://www.northparkcenter.com/posts/" + slug
                    return share_url
                },
                truncate(val_body) {
                    var truncate = _.truncate(val_body, { 'length': 99, 'separator': ' ' });
                    return truncate;
                }
            }
        });
    });
</script>