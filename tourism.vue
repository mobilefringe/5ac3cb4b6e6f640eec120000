<template>
    <div class="tourism_page"> <!-- without an outer container div this component template will not render -->
        <loader v-if="!dataLoaded"></loader>
        <transition name="fade">
            <div v-if="dataLoaded" v-cloak>
                <div class="page_header" v-if="pageBanner" v-bind:style="{ backgroundImage: 'url(' + pageBanner.image_url + ')' }">
        			<div class="site_container">
        				<div class="header_content caps">
        					<h1>{{ pageContent.title }}</h1>
        				</div>
        			</div>
        		</div>
        		<div class="site_container">
                    <div class="program_header_container information hidden_phone">
        				<div class="program_button_container animated_btn" v-for="item in pages" @click="selectContent(item)" :class="{ active: item.isActive, last: item.isLast }">

        				    <span v-if="locale=='en-ca'">{{ item.title }}</span>
							<span v-else>{{ item.title_2 }}</span>
        				</div>
        			</div>
        			<div class="visible_phone margin_20">
        			    <label style="display: none;" for="pageSelect">Select a Page</label>
        				<v-select :options="dropDownSelect" :searchable="false" :on-change="selectPage" class="category-select" placeholder="Select a Page" inputId="pageSelect"></v-select>
        			</div>
        			<div class="row">
        			    <div :class="{'col-sm-12': currentPageContent.isActive}">
        			        <div v-if="currentPageContent">
        			            <div v-if="locale=='en-ca'" v-html="currentPageContent.body"></div>
        			            <div v-else v-html="currentPageContent.body_2"></div>
        			        </div>
        			    </div>
        			   <!--<div class="col-sm-6" v-if="pageSubpage1 && currentPageContent.isActive">-->
        			   <!--    <div v-if="pageSubpage1">-->
        			   <!--         <div v-if="locale=='en-ca'" v-html="pageSubpage1.body"></div>-->
        			   <!--         <div v-else v-html="pageSubpage1.body_2"></div>-->
        			   <!--     </div>-->
        			   <!--</div>-->
        		    </div>
        		    <div class="mall_info_images" v-if="currentPageContent.title == 'Travel Partners'">
        			    <div class="mall_images" v-for="item in travel_partners" v-if="travel_partners">
        			        <img class="max_width" :src="item.image_url" alt="" />
        			    </div>
        		    </div>
                </div>
            </div>
        </transition>
    </div>
</template>

<script>
    define(["Vue", "vuex", "vue-select"], function(Vue, Vuex, VueSelect) {
        return Vue.component("tourism-component", {
            template: template, // the variable template will be injected
            props:['locale'],
            data: function() {
                return {
                    dataLoaded: false,
                    pageBanner: null,
                    currentPageContent: null,
                    pageContent: null,
                    pageSubpage1: null,
                    pageSubpage2: null,
                    travel_partners: null
                }
            },
            watch: {
                selectedItem: function() {
                    console.log(this)
                },
            },
            created(){
                this.loadData().then(response => {
                    var temp_repo = this.findRepoByName('Mall Info Banner');
                    if (temp_repo && temp_repo.images) {
                        try {
                            this.pageBanner = temp_repo.images[0];
                        } catch(e) {
                            
                        }
                    } else {
                        this.pageBanner = { "image_url": "" }
                    }
                    var temp_repo1 = this.findRepoByName('Travel Partners');
                    if (temp_repo1 && temp_repo1.images) {
                        this.travel_partners = temp_repo1.images;
                    }
                    // this.leasingContent = response[1].data;
                    // this.leasingSubpage = response[1].data.subpages[0];
                    // this.leasingContent.isActive = true;
                    // this.marketingContent = response[2].data;
                    // this.areaContent = response[3].data;
                    if(response && response[1]){
                        this.pageContent = response[1].data;
                        if(response[1].data && response[1].data.subpages){
                            this.pageSubpage1 = response[1].data.subpages[0];
                            this.pageSubpage2 = response[1].data.subpages[1];
                        }
                    }
                    this.currentPageContent = this.pageContent;
                    this.selectContent(this.currentPageContent)
                    this.dataLoaded = true;
                });
            },
            computed: {
                ...Vuex.mapGetters([
                    'property',
                    'timezone',
                    'findRepoByName'
                ]),
                pages() {
                    var pages_json = [];
                    pages_json = _.concat(pages_json, this.pageContent, this.pageSubpage1, this.pageSubpage2)
                    _.forEach(pages_json, function (value, key) {
                        if ( _.includes([2], key)) {
                            value.isLast = true;
                        }
                    });
                    return pages_json
                },
                dropDownSelect() {
                    var cats = _.map(this.pages, 'title');
                    return cats;
                }
            },
            methods: {
                loadData: async function() {
                    try {
                        let results = await Promise.all([this.$store.dispatch("getData", "repos"), this.$store.dispatch('LOAD_PAGE_DATA', {url: this.property.mm_host + "/pages/twinpinesmall-tourism.json"})]);
                        return results;
                    } catch (e) {
                        console.log("Error loading data: " + e.message);
                    }
                },
                selectContent(item) {
                    _.forEach(this.pages, function (value, key) {
                        value.isActive = false;
                    });
                    
                    var selected_item = item
                    this.$nextTick(function () {
                      selected_item.isActive = true;
                    });
            
                    this.currentPageContent = selected_item;
                },
                selectPage(item) {
                    var _this = this
                    var item = item
                    _.forEach(this.pages, function (value, key) {
                        if (_.includes(value.title, item )) {
                            _this.$nextTick(function () {
                                this.currentPageContent = value;    
                            });
                        }
                    });
                }
            }
        });
    });
</script>
