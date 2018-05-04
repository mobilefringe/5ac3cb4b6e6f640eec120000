<template>
    <header>
        <div class="sticky">
			<div class="site_container">
				<div class="row header_logo">
					<div class="col-md-3 hidden_phone">
					    <div class="language_select">
					        <span @click="changeLocale('en-ca')">en</span> | <span @click="changeLocale('fr-ca')">fr</span>
				        </div>	
					</div>
					<div class="col-xs-12 col-md-6 mobile_header">
					    <div class="property_logo center-block">
							<router-link to="/">
							    <img src="//codecloud.cdn.speedyrails.net/sites/5ac3cb4b6e6f640eec120000/image/png/1522945678000/tplogo.png" alt="The Twin Pines Mall Logo"/>
						    </router-link>
						</div>
						<div class="mobile_menu_icon visible_phone" @click="showMenu = !showMenu">
					        <span>Menu</span>
				            <i v-if="!showMobileMenu" class="fa fa-angle-down"></i>
				            <i v-if="showMobileMenu" class="fa fa-angle-up"></i>
					    </div>
					</div>
					<div class="col-md-3 hidden_phone">
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
				<div class="row">
				    <div class="col-md-2 hidden_phone"></div>
					<div class="col-sm-12 col-md-8">
						<nav id="primary_nav" class="hidden_phone">
							<ul>
							    <li class="menu_item" v-for="item in menu_items" :id="item.id">
							        <router-link :to="item.href">{{$t(item.name)}}</router-link>
							        <ul v-if="item.sub_menu">
							            <li v-for="sub_menu in item.sub_menu" class="dropdown_item">
							                <router-link :to="sub_menu.href">{{$t(sub_menu.name)}}</router-link>
							            </li>
									</ul>
							    </li>
							</ul>
						</nav>
					</div>
					<div class="nav_container visible_phone">
					    <transition name="custom-classes-transition" enter-active-class="animated slideInDown" leave-active-class="animated slideOutUp">
    					    <nav id="mobile_nav" v-show="showMenu" class="">
    					        <ul>
    					            <li v-for="(item,key) in menu_items" class="menu_item">
    							        <router-link :to="item.href" v-if="item.sub_menu == undefined">{{$t(item.name)}}</router-link>
    							        <div v-else>
    							            <b-card no-body class="mb-1">
                                                <b-card-header header-tag="header" class="p-1" role="tab">
                                                    <b-btn block @click="item.show_sub_menu = !item.show_sub_menu" :class="item.show_sub_menu ? 'collapsed' : null" :aria-controls="$t(item.name)" :aria-expanded="item.show_sub_menu ? 'true' : 'false'">
                                                        {{$t(item.name)}}
                                                        <i v-if="item.show_sub_menu"  class="fa fa-minus"></i>
                                                        <i v-else  class="fa fa-plus"></i>
                                                    </b-btn>
                                                </b-card-header>
                                                <b-collapse v-model="item.show_sub_menu" :id="$t(item.name)" :visible="item.show_sub_menu" :accordion="$t(item.name)" role="tabpanel" class="accordion_body">
                                                    <b-card-body v-for="sub_menu in item.sub_menu">
                                                        <p class="card-text">
                                                            <router-link :to="sub_menu.href">{{$t(sub_menu.name)}}</router-link>
                                                        </p>
                                                    </b-card-body>
                                                </b-collapse>
                                            </b-card>
    							        </div>
    							    </li>
    					        </ul>
    						    <div class="mobile_nav_content visible_phone">
    							    <div class="social_icons center">
                                        <span v-for="item in social_media">
                                            <a :href="item.url" target="_blank">
                                                <p class="accessibility">{{item.name}}</p>
                                                <i :class="item.iconClass" aria-hidden="true"></i>
                                            </a>
                                        </span>
                                    </div> 
                                    <div class="mobile_property_address center">
                                        <p>{{ property.name }}<br>
                                            <a href="https://goo.gl/maps/RJ5dV8dxP1y" target="_blank">{{ property.address1 }}<br>{{ property.city }} {{ property.province_state }} {{ property.postal_code }}</a>
                                        </p>
                                        
                                    </div>
    							</div>
    						</nav>
    				    </transition>
    				</div>
					<div class="col-md-2 hidden_phone">
					    <div class="social_icons pull-right">
                            <span v-for="item in social_media">
                                <a :href="item.url" target="_blank">
                                    <p class="accessibility">{{item.name}}</p>
                                    <i :class="item.iconClass" aria-hidden="true"></i>
                                </a>
                            </span>
                        </div>	
					</div>
				</div>
			</div>
		</div>
    </header>
</template>

<script>
var _extends=Object.assign||function(t){for(var e=1;e<arguments.length;e++){var n=arguments[e];for(var o in n)Object.prototype.hasOwnProperty.call(n,o)&&(t[o]=n[o])}return t};define(["Vue","vuex","vue_router","routes","bootstrap-vue"],function(t,e,n,o,i){return t.use(i),t.component("header-component",{template:template,props:["menu_items","social_media"],data:function(){return{suggestionAttribute:"name",search:"",showMenu:!1,showMobileMenu:!1,noScroll:!1,windowWidth:0}},watch:{$route:function(){this.windowWidth<=768&&(this.showMenu=!1),_.forEach(this.menu_items,function(t){t.show_sub_menu=!1})},showMenu:function(){1==this.showMenu?document.body.classList.add("no_scroll"):0==this.showMenu&&document.body.classList.remove("no_scroll")}},created:function(){this.$nextTick(function(){window.addEventListener("resize",this.getWindowWidth),this.getWindowWidth()})},computed:_extends({},e.mapGetters(["property","timezone","processedStores"]),{locale:{get:function(){return this.$store.state.locale},set:function(t){this.$store.commit("SET_LOCALE",{lang:t})}}}),methods:{changeLocale:function(t){this.locale=t},getWindowWidth:function(){this.windowWidth=window.innerWidth},onOptionSelect:function(t){this.$nextTick(function(){this.search=""}),this.$router.push("/stores/"+t.slug)}},beforeDestroy:function(){window.removeEventListener("resize",this.getWindowWidth)}})});
</script>