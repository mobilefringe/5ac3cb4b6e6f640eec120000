<template>
    <div> <!-- without an outer container div this component template will not render -->
        <loader v-if="!dataLoaded"></loader>
        <transition name="fade">
            <div v-if="dataLoaded" v-cloak>
                <div class="page_header" v-if="pageBanner" v-bind:style="{ backgroundImage: 'url(' + pageBanner.image_url + ')' }">
        			<div class="site_container">
        				<div class="header_content caps">
        				    <p>{{ $t("hours_page.header_desc") }}</p>
        					<h1>{{$t("hours_page.hours")}}</h1>
        				</div>
        			</div>
        		</div>  
                <div class="site_container">
                    <div class="all_hours_container">
                        <div class="row">
                            <div class="col-sm-6">
                                <h5 class="caps">{{ $t("hours_page.reg_hours") }}</h5>
                                <div id="hours_container" class="hours_container">
                                    <div class="hours_div text-left" v-for="hour in hours">
                                        <span :class="hour.todays_hour">
                                            <span>{{ hour.day_of_week | moment("dddd", timezone) }}: </span>
                                            <span v-if="hour.is_closed == true">Closed</span>
                                            <span v-else>
                                                {{hour.open_time | moment("h:mm A", timezone)}} - {{hour.close_time | moment("h:mm A", timezone)}}
                                            </span>
                                        </span>
                                    </div>
                                </div>
                            </div>
                            <div class="col-sm-6">
                                <h5 class="caps">{{$t("hours_page.holiday_hours")}}</h5>
                                <div id="holidays_hours_container" class="hours_container">
                                    <div class="hours_div text-left"  v-for="hour in holidayHours">
                                        <span>
                                            <span v-if="locale=='en-ca'">{{hour.holiday_name}} / </span>
                                            <span v-else>{{hour.holiday_name_2}} / </span>
                                            {{ hour.holiday_date | moment("MMM D YYYY", timezone) }} /
                                        </span>
                                        <span v-if="hour.is_closed == true">{{ $t("hours_page.closed") }}</span>
                                        <span v-else>
                                            {{ hour.open_time | moment("h:mm A", timezone)}} - {{hour.close_time | moment("h:mm A", timezone) }}
                                        </span>
                                    </div>
                                </div>
                            </div>
                            <div class="col-sm-6">
                                <h5 class="caps">{{$t("hours_page.extended_hours")}}</h5>
                                <div id="holidays_hours_container" class="hours_container">
                                    <div class="hours_div text-left"  v-for="hour in extendedHours">
                                        <span>
                                            <span v-else>{{hour.holiday_name_2}} / </span>
                                            {{ hour.holiday_date | moment("MMM D YYYY", timezone) }} /
                                        </span>
                                        <span v-if="hour.is_closed == true">{{ $t("hours_page.closed") }}</span>
                                        <span v-else>
                                            {{ hour.open_time | moment("h:mm A", timezone)}} - {{hour.close_time | moment("h:mm A", timezone) }}
                                        </span>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="padding_top_40"></div>
                    </div>
                </div >
            </div>    
        </transition>        
    </div>
</template>

<script>
    define(["Vue", "vuex", "moment", "moment-timezone", "vue-moment", "vue-meta"], function(Vue, Vuex, moment, tz, VueMoment, Meta) {
        Vue.use(Meta);
        return Vue.component("hours-component", {
            template: template, // the variable template will be injected
            props:['locale'],
            data: function() {
                return {
                    dataLoaded: false,
                    pageBanner : null
                }
            },
            created() {
                this.loadData().then(response => {
                    var temp_repo = this.findRepoByName('Hours Banner').images;
                    if(temp_repo != null) {
                        this.pageBanner = temp_repo[0];
                    } else {
                        this.pageBanner = "http://via.placeholder.com/1920x400/4f6726/4f6726";
                    }
                    
                    this.dataLoaded = true;
                });
            },
            watch : {
                locale: function(val, oldVal) {
                    console.log("locale", this.locale);
                },
            },
            computed: {
                ...Vuex.mapGetters([
                    'property',
                    'timezone',
                    'getPropertyHours',
                    'getPropertyHolidayHours',
                    'getPropertyExtendedHours',
                    'findRepoByName'
                ]),
                hours () {
                    var today = moment().day()
                    var hours = this.getPropertyHours;
                    _.forEach(hours, function(value) {
                        if( today == value.day_of_week ){
                            value.todays_hour = "todays_hour"
                        }    
                    });
                    return hours;
                },
                holidayHours () {
                    return this.getPropertyHolidayHours;
                },
                extendedHours () {
                    return this.getPropertyExtendedHours;
                }
            },
            methods : {
                loadData: async function() {
                    try {
                        // avoid making LOAD_META_DATA call for now as it will cause the entire Promise.all to fail since no meta data is set up.
                        let results = await Promise.all([this.$store.dispatch("getData", "repos")]);
                        return results;
                    } catch (e) {
                        console.log("Error loading data: " + e.message);
                    }
                },
            }
        });
    });
</script>
