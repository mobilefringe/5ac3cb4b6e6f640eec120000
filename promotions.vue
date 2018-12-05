<template>
    <div> <!-- without an outer container div this component template will not render -->
        <loader v-if="!dataLoaded"></loader>
        <transition name="fade">
            <div v-if="dataLoaded" v-cloak>
        		<div class="page_header" v-if="pageBanner" v-bind:style="{ backgroundImage: 'url(' + pageBanner.image_url + ')' }">
        			<div class="site_container">
        				<div class="header_content caps">
        					<p>{{ $t("promos_page.promos_header_desc") }} {{ property.name }}</p>
        					<h1>{{ $t("promos_page.promos_header") }}</h1>
        				</div>
        			</div>
        		</div>
        		<div class="site_container page_content">
					<div class="promo_container" v-for="(item, index) in promotions" v-if="showMore > index">
					    <div class="promo_img" v-if="locale=='en-ca'" v-bind:style="{ backgroundImage: 'url(' + item.image_url + ')' }"></div>
					    <div class="promo_img" v-else v-bind:style="{ backgroundImage: 'url(' + item.promo_image2_url_abs + ')' }"></div>
					    <div class="promo_content">
					        <p class="promo_title" v-if="item.store">{{ item.store.name }}</p>
					        <p class="promo_title" v-else>{{ property.name }}</p>
					        <h3 class="" v-if="locale=='en-ca'">{{ item.name_short }}</h3>
							<h3 class="" v-else>{{ item.name_short_2 }}</h3>
							<p class="promo_dates" v-if="isMultiDay(item)">
							    {{ item.start_date | moment("MMMM D", timezone)}} to {{ item.end_date | moment("MMMM D", timezone)}}
                            </p>
                            <p class="promo_dates" v-else>{{ item.start_date | moment("MMMM D", timezone)}}</p>
							<router-link :to="'/promotions/'+ item.slug" >
							   <div class="promo_learn_more animated_btn swing_in">{{ $t("promos_page.read_more") }}</div>
						    </router-link>
					    </div>
					</div>
					<div class="row" v-if="!promotions.length">
        				<div class="col-md-12">
        					<p>{{$t("promos_page.no_promo_message")}}</p>
        				</div>
        			</div>
                    <div class="load_more animated_btn swing_in" v-if="promotions && showMore <= promotions.length" @click ="loadMore()">
                        <p>Load More</p>
                    </div>
                   
        		
    
        		</div>
	        </div>
	    </transition>
	</div>
</template>

<script>
    define(["Vue", "vuex", "moment", "moment-timezone", "vue-moment"], function(Vue, Vuex, moment, tz, VueMoment) {
        return Vue.component("promos-component", {
            template: template, // the variable template will be injected
            props:['locale'],
            data: function() {
                return {
                    dataLoaded: false,
                    pageBanner: null,
                    showMore: 3,
                    incrementBy: 3
                }
            },
            created() {
                this.loadData().then(response => {
                    var temp_repo = this.findRepoByName('Promotions Banner').images;
                    if(temp_repo != null) {
                        this.pageBanner = temp_repo[0];
                    } else {
                        this.pageBanner = "http://via.placeholder.com/1920x400/4f6726/4f6726";
                    }

                    this.dataLoaded = true;
                });
            },
            computed: {
                ...Vuex.mapGetters([
                    'property',
                    'findRepoByName',
                    'timezone',
                    'processedPromos'
                ]),
                promotions() {
                    var vm = this;
                    var temp_promo = [];
                    _.forEach(this.processedPromos, function(value, key) {
                        value.name_short = _.truncate(value.name, { 'length': 30, 'separator': ' ' });
                        value.name_short_2 = _.truncate(value.name_2, { 'length': 30, 'separator': ' ' });

                        if (_.includes(value.image_url, 'missing')) {
                            value.image_url = "http://placehold.it/1560x800/757575";
                        }
                        if (_.includes(value.promo_image2_url_abs, 'missing')) {
                            value.promo_image2_url_abs = "http://placehold.it/1560x800/757575";
                        }
                        
                        temp_promo.push(value);
                    });
                    _.sortBy(temp_promo, [function(o) { return o.start_date; }]);
                    return temp_promo;
                }
            },
            methods: {
                loadData: async function() {
                    try {
                        let results = await Promise.all([this.$store.dispatch("getData", "repos"), this.$store.dispatch("getData", "promotions")]);
                    } catch (e) {
                        console.log("Error loading data: " + e.message);
                    }
                },
                loadMore() {
                    if (this.showMore <= this.promotions.length) {
                        var num = this.showMore + this.incrementBy;
                        this.showMore = num;
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
                },
            }
        });
    });
</script>