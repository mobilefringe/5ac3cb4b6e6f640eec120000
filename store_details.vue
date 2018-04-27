<template>
    <div> <!-- without an outer container div this component template will not render -->
        <loader v-if="!dataLoaded"></loader>
        <transition name="fade">
            <div v-if="dataLoaded" v-cloak class="site_container">
                <div class="">
                    <div class="details_store_name">
                        <div class="details_border">
                            <div>
                                <h2>{{ currentStore.name}}</h2>
                                <p>{{ storeCategory }}</p>
                            </div>
                        </div>
                    </div>
					<div class="details_store_image">
						<img v-lazy="currentStore.store_front_url_abs" class="image"/>
						<div class="details_btn_container">
						    <a v-if="currentStore.phone" :href="'tel:' + currentStore.phone" target="_blank">
        				        <div class="details_store_website animated_btn swing_in">{{currentStore.phone}}</div>
        				    </a>
    				        <a v-if="currentStore.website" :href="'//' + currentStore.website" target="_blank">
        				        <div class="details_store_website animated_btn swing_in">{{$t("stores_page.store_website")}}</div>
        				    </a>
						</div>
					</div>
    				<div class="details_store_desc">
    				    <div v-html="currentStore.description"></div>
    				</div>
    			</div>
    			<div class="store_promo_container" v-if="currentStore && currentStore.total_published_promos > 0">
    			    Promotions
    			    <div class="promo_container clearfix" v-for="promo in promotions">
					    <div class="promo_img" v-if="locale=='en-ca'" v-lazy:background-image="promo.image_url"></div>
					    <div class="promo_img" v-else v-lazy:background-image="promo.promo_image2_url_abs"></div>
					    <div class="promo_content">
					        <p class="promo_title" v-if="promo.store">{{ promo.store.name }}</p>
					        <p class="promo_title" v-else>{{ property.name }}</p>
					        <h3 class="" v-if="locale=='en-ca'">{{ promo.name_short }}</h3>
							<h3 class="" v-else>{{ promo.name_short_2 }}</h3>
							<p class="promo_dates" v-if="isMultiDay(promo)">
							    {{ promo.start_date | moment("MMMM D", timezone)}} to {{ promo.end_date | moment("MMMM D", timezone)}}
                            </p>
                            <p class="promo_dates" v-else>{{ promo.start_date | moment("MMMM D", timezone)}}</p>
							  
					  <!--      <p class="promo_desc"  v-if="locale=='en-ca'" >{{ promo.description_short }}</p>-->
							<!--<p class="promo_desc" v-else>{{ promo.description_short_2 }}</p>-->
							<router-link :to="'/promotions/'+ promo.slug" >
							   <div class="promo_learn_more animated_btn swing_in">{{ $t("promos_page.read_more") }}</div>
						    </router-link>
					    </div>
					</div>
    			</div>
		    </div>
		</transition>
	</div>
</template>

<script>
    define(['Vue', 'vuex', 'moment', 'vue-lazy-load'], function(Vue, Vuex, moment, VueLazyload) {
        Vue.use(VueLazyload);
        return Vue.component("store-details-component", {
            template: template, // the variable template will be injected,
            data: function() {
                return {
                    dataLoaded: false,
                    currentStore: null,
                    promotions : []
                }
            },
            props:['id', 'locale'],
            beforeRouteUpdate(to, from, next) {
                this.currentStore = this.findStoreBySlug(to.params.id);
                if (this.currentStore === null || this.currentStore === undefined){
                    this.$router.replace({ name: '404'});
                }
                next();
            },
            created (){
                this.loadData().then(response => {
                    this.updateCurrentStore(this.id);
                    this.dataLoaded = true;
                });
            },
            watch: {
                currentStore: function() {
                    console.log(this.currentStore)
                    console.log(this.currentStore.store_front_url_abs)
                    if ( _.includes(this.currentStore.store_front_url_abs, 'missing')) {
                        this.currentStore.store_front_url_abs = "//codecloud.cdn.speedyrails.net/sites/5a81f86a6e6f6404f6030000/image/png/1516652189884/ES_logo_red2.png";
                    }
                    
                    var vm = this;
                    var temp_promo = [];
                    _.forEach(this.currentStore.promotions, function(value, key) {
                        console.log(value)
                        var current_promo = vm.findPromoById(value);
                        console.log(current_promo)
                        // current_promo.description_short = _.truncate(current_promo.description, {
                        //     'length': 70
                        // });
                        temp_promo.push(current_promo);
                    }); 
                    this.promotions = temp_promo;
                    console.log(this.promotions)
                },
                locale: function(val, oldVal) {
                    console.log("locale", this.locale);
                }
            },
            computed: {
                ...Vuex.mapGetters([
                    'property',
                    'timezone',
                    'processedStores',
                    'findStoreBySlug',
                    'findCategoryById',
                    'findPromoById'
                ]),
                storeCategory() {
                    var currentStoreCategory = this.currentStore.categories[0];
                    category = this.findCategoryById(currentStoreCategory)
                    return category.name
                }
            },
            methods: {
                loadData: async function() {
                    try {
                        // avoid making LOAD_META_DATA call for now as it will cause the entire Promise.all to fail since no meta data is set up.
                        let results = await Promise.all([this.$store.dispatch("getData", "categories")]);
                    } catch (e) {
                        console.log("Error loading data: " + e.message);
                    }
                },
                updateCurrentStore (id) {
                    this.currentStore = this.findStoreBySlug(id);
                    if (this.currentStore === null || this.currentStore === undefined){
                        this.$router.replace({ name: '404'});
                    }
                },
                isMultiDay(promo) {
                    var timezone = this.timezone
                    var start_date = moment(promo.start_date).tz(timezone).format("MM-DD-YYYY")
                    var end_date = moment(promo.end_date).tz(timezone).format("MM-DD-YYYY")
                    if (start_date === end_date) {
                        return false
                    } else {
                        return true
                    }
                }
            }
        });
    });
</script>