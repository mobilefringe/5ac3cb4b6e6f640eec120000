<template>
	<div id="silton_banner">
		<div class="Modern-Slider">
		    <slick ref="slick" :options="siltonOptions">
    			<!-- Item -->
    			<div class="item" v-for="banner in banners">
    				<div class="img-fill">
    					<img :src="banner.image_url" alt="">
    					<div class="info">
    						<div>
    							<h3>{{banner.name}}</h3>
    							<h5>{{banner.description}}</h5>
    						</div>
    					</div>
    				</div>
    			</div>
    			<!-- // Item -->
		    </slick>
		</div>
	</div>
</template>

<style>
@import "/silton_banner.css";
</style>

<script>
    define(["Vue", "vue!vue-slick"], function (Vue, slick) {
        return Vue.component("silton-banner", {
            template: template, // the variable template will be injected,
            props:['banners'],
            data: function() {
                return {
                    siltonOptions: {
                        autoplay:true,
                        autoplaySpeed:10000,
                        speed:600,
                        slidesToShow:1,
                        slidesToScroll:1,
                        pauseOnHover:false,
                        dots:true,
                        pauseOnDotsHover:true,
                        cssEase:'linear',
                       // fade:true,
                        draggable:false,
                        prevArrow:'<button class="PrevArrow"></button>',
                        nextArrow:'<button class="NextArrow"></button>'
                    }
                }
            }
        });
    });
</script>