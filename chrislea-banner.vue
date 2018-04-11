<template>
    <div class="banners chrislea banner_option_2">
        <div class="prev"></div>
        <slick ref="slick" :options="chrisleaOptions" key="banners2">
			<div class="" v-for="banner in banners" v-if="banners">
				<div class="banner" v-bind:style="{ backgroundImage: 'url(' + banner.image_url + ')' }">
				    <div class="details">
    					<span class="title">
    					    <h3>{{ banner.name }}</h3>
					    </span>
    					<!--<span class="title" v-else>-->
    					<!--    <h3>{{ feature.name_2 }}</h3>-->
					    <!--</span>-->
    					<span class="info">
    					    <p>{{ banner.description }}</p>
					    </span>
    					<!--<span class="info" v-else>-->
    					<!--    <p>{{ feature.description_2 }}</p>-->
					    <!--</span>-->
    				</div>
				</div>
			</div>
		</slick>
		<div class="next"></div>
    </div>
</template>

<style>

</style>

<script>
    define(["Vue", "vue!vue-slick"], function (Vue, slick) {
        return Vue.component("weston-banner", {
            template: template, // the variable template will be injected,
            props:['banners'],
            data: function() {
                return {
                    chrisleaOptions: {
                        autoplay: true,
                        autoplaySpeed: 6000,
                        cssEase: 'ease',
                        dots: true,
                        infinite: true,
                        nextArrow: '.banner_option_2 .next',
                        prevArrow: '.banner_option_2 .prev',
                        slidesToShow: 1,
                    }
                }
            }
        });
    });
</script>