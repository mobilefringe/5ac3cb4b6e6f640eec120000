<template>
    <footer v-if="footerBanner" v-bind:style="{ backgroundImage: 'url(' + footerBanner.image_url + ')' }">
        <div class="newsletter_subscription hidden_phone">
            <div class="newsletter_content_container">
                <h3 class="caps hidden_phone">{{$t("footer.newsletter")}}</h3>
                <h1 class="caps hidden_phone">{{$t("footer.subscription")}}</h1>
                <h3 class="newsletter_desc caps hidden_phone">{{$t("footer.newsletter_desc")}}</h3>
                <div id="newsletter_form">
                    <label for="fieldEmail" style="display:none"></label>
                    <input id="fieldEmail" name="cm-tkyhii-tkyhii" class="form-control" type="email" v-model="newsletter_email" :placeholder="$t('footer.enter_email')" required/> 
                    <router-link data-i18n="general.submit" :to="'/newsletter?email='+ newsletter_email">
                        <div class="newsletter_btn animated_btn">{{$t("footer.subscribe")}}</div>
                    </router-link>
                    <span id="success_subscribe" class="hidden_now">{{$t("footer.subscribe_thankyou")}}</span>
                </div>
            </div>
        </div>
		<div class="footer">
			<div class="site_container">
			    <div class="row footer_logo">
			        <div class="col-md-3 center-block">
			            <div class="property_logo">
					        <router-link to="/">
					            <img src="//codecloud.cdn.speedyrails.net/sites/5ac3cb4b6e6f640eec120000/image/png/1522945678000/tplogo.png" alt="Property Logo"/>
				            </router-link>
				        </div>    
			        </div>
			        <div class="col-xs-12 visible_phone">
			            <div class="row">
			                <div class="col-xs-4">
			                    <div class="language_select">
					                <span @click="changeLocale('en-ca')">EN</span> | <span @click="changeLocale('fr-ca')">FR</span>
				                </div>    
			                </div>
			                <div class="col-xs-8">
			                    <div class="header_search_container">
                			        <search-component v-model="search" :list="processedStores" :suggestion-attribute="suggestionAttribute" :placeholder="$t('header.search')" @select="onOptionSelect">
                                        <template slot="item" scope="option">
                                            <article class="media">
                                                <p>{{ option.data.name }}</p>
                                            </article>
                                        </template>
                                    </search-component>
                                </div>
			                </div>
			            </div>
			        </div>
			        <div class="col-md-6">
			            <nav id="footer_nav">
    						<ul>
    						    <li v-for="item in footer_menu_items" class="menu_item">
    						        <router-link :to="item.href">{{$t(item.name)}}</router-link>
    						    </li>
    						</ul>
    					</nav>    
			        </div>
			        <div class="col-md-3">
			            <div class="social_icons">
                            <span v-for="item in social_media">
                                <a :href="item.url" target="_blank">
                                    <i :class="item.iconClass" aria-hidden="true"></i>
                                </a>
                            </span>
                        </div>    
			        </div>
			    </div>
				<div class="footer_terms">
					<p>&copy; {{copyright_year}} <span class="caps">{{property.name}}</span> {{$t("footer.all_rights")}} <router-link to="/pages/bonniedoon-privacy-policy">{{$t("footer.privacy_policy")}}</router-link> <span class="hidden_phone">|</span><br class="visible_phone"/><span> {{$t("footer.powered_by")}} <a href="//www.mallmaverick.com" target="_blank">Mall Maverick</a></span></p>
				</div>
			</div>
		</div>
    </footer>
</template>

<script>
var _extends=Object.assign||function(e){for(var t=1;t<arguments.length;t++){var n=arguments[t];for(var o in n)Object.prototype.hasOwnProperty.call(n,o)&&(e[o]=n[o])}return e};define(["Vue","vuex","moment","moment-timezone","vue-moment","vue!search-component"],function(e,t,n){return e.component("footer-component",{template:template,data:function(){return{footerBanner:null,suggestionAttribute:"name",search:"",newsletter_email:""}},props:["footer_menu_items","social_media"],created:function(){var e=this;this.loadData().then(function(){e.dataLoaded=!0;var t=e.findRepoByName("Footer Banner");t&&(e.footerBanner=t.images[0])})},computed:_extends({},t.mapGetters(["property","findRepoByName","processedStores"]),{locale:{get:function(){return this.$store.state.locale},set:function(e){this.$store.commit("SET_LOCALE",{lang:e})}},copyright_year:function(){return n().year()}}),methods:{loadData:function(){var e;return regeneratorRuntime.async(function(t){for(;;)switch(t.prev=t.next){case 0:return t.prev=0,t.next=3,regeneratorRuntime.awrap(Promise.all([this.$store.dispatch("getData","repos")]));case 3:e=t.sent,t.next=9;break;case 6:t.prev=6,t.t0=t["catch"](0),console.log("Error loading data: "+t.t0.message);case 9:case"end":return t.stop()}},null,this,[[0,6]])},changeLocale:function(e){this.locale=e},onOptionSelect:function(e){console.log("Selected option:",e),this.$nextTick(function(){this.search=""}),this.$router.push("/stores/"+e.slug)}}})});
</script>