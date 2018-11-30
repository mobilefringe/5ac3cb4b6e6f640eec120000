<template>
    <div> <!-- without an outer container div this component template will not render -->
        <loader v-if="!dataLoaded"></loader>
        <transition name="fade">
            <div v-if="dataLoaded" v-cloak>
        		<div class="page_header" v-if="pageBanner" v-bind:style="{ backgroundImage: 'url(' + pageBanner.image_url + ')' }">
        			<div class="site_container">
        				<div class="header_content caps">
        					<p>{{ property.name }} {{ $t("events_page.events_header_desc") }} </p>
        					<h1>{{ $t("events_page.events_header") }}</h1>
        				</div>
        			</div>
        		</div>
        		<div class="site_container page_content">
        			<div id="promos_container" class="clearfix" v-if="promos.length > 0">
        				<paginate name="promos" v-if="promos" :list="promos" class="paginate-list margin-60" :per="3">
        					<div class="promo_container clearfix" v-for="(promo, index) in paginated('promos')">
        					    <div class="promo_img" v-if="locale=='en-ca'" v-bind:style="{ backgroundImage: 'url(' + promo.image_url + ')' }"></div>
        					    <div class="promo_img" v-else v-bind:style="{ backgroundImage: 'url(' + promo.event_image2_url_abs + ')' }"></div>
        					    <div class="promo_content">
        					        <p class="promo_title">{{ $t("events_page.events") }}</p>
        					        <h3 class="" v-if="locale=='en-ca'">{{ promo.name_short }}</h3>
        							<h3 class="" v-else>{{ promo.name_short_2 }}</h3>
        							<p class="promo_dates" v-if="isMultiDay(promo)">
        							    {{ promo.start_date | moment("MMMM D", timezone)}} to {{ promo.end_date | moment("MMMM D", timezone)}}
                                    </p>
                                    <p class="promo_dates" v-else>{{ promo.start_date | moment("MMMM D", timezone)}}</p>
        							<router-link :to="'/events/'+ promo.slug" >
        								   <div class="promo_learn_more animated_btn swing_in">{{ $t("events_page.read_more") }}</div>
        						    </router-link>
        					    </div>
        					</div>
        				</paginate>
        			</div>
        			<div class="row" v-else>
        				<div class="col-md-12">
        					<p>{{$t("events_page.no_event_message")}}</p>
        				</div>
        			</div>
        			<div class="row">
        				<div class="col-md-12">
        					<paginate-links for="promos" :async="true" :limit="3" :show-step-links="true"></paginate-links>
        				</div>
        			</div>
        		</div>
	        </div>
	    </transition>
	</div>
</template>

<script>
    define(["Vue", "vuex", "moment", "moment-timezone", "vue-moment", "vue-paginate"], function(Vue, Vuex, moment, tz, VueMoment, VuePaginate) {
        Vue.use(VuePaginate);
        return Vue.component("promos-component", {
            template: template, // the variable template will be injected
            props:['locale'],
            data: function() {
                return {
                    dataLoaded: false,
                    pageBanner: null,
                    promos : null,
                    paginate: ['promos']
                }
            },
            created() {
                this.loadData().then(response => {
                    var temp_repo = this.findRepoByName('Events Banner').images;
                    if(temp_repo != null) {
                        this.pageBanner = temp_repo[0];
                    } else {
                        this.pageBanner = "http://via.placeholder.com/1920x400/4f6726/4f6726";
                    }

                    this.promos = this.events;
                    this.dataLoaded = true;
                });
            },
            computed: {
                ...Vuex.mapGetters([
                    'property',
                    'timezone',
                    'findRepoByName',
                    'processedEvents'
                ]),
                events() {
                    var vm = this;
                    var temp_event = [];
                    var temp_job = [];
                    _.forEach(this.processedEvents, function(value, key) {
                        value.name_short = _.truncate(value.name, { 'length': 30, 'separator': ' ' });

                        if (_.includes(value.image_url, 'missing')) {
                            value.image_url = "http://placehold.it/1560x800/757575";
                        }
                        if (_.includes(value.event_image2_url_abs, 'missing')){
                            value.event_image2_url_abs  = "http://placehold.it/1560x800/757575";
                        }

                        temp_event.push(value);
                    });
                    _.sortBy(temp_event, [function(o) { return o.start_date; }]);
                    return temp_event;
                },
            },
            methods: {
                loadData: async function() {
                    try {
                        // avoid making LOAD_META_DATA call for now as it will cause the entire Promise.all to fail since no meta data is set up.
                        let results = await Promise.all([this.$store.dispatch("getData", "repos"), this.$store.dispatch("getData", "events")]);
                    } catch (e) {
                        console.log("Error loading data: " + e.message);
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