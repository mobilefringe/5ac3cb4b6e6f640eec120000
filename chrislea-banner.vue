<template>
    <div id="slider" class="banners">
        <div class="prev"></div>
        <slick ref="slick" :options="chrisleaOptions">
			<div v-for="banner in banners" v-if="banners">
				<div class="slider">
                    <div class="banner-legend"></div> 
                    <div class="banner-content"> 
                        <div class="banner-content-txt"> 
                            <h3>{{ banner.name }}</h3> 
                            <p>{{ banner.description }}</p> 
                        </div> 
                    </div> 
                    <div class="images"> 
                        <img :src="banner.image_url"> 
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
                        autoplaySpeed: 8000,
                        cssEase: 'ease',
                        dots: true,
                        infinite: true,
                        nextArrow: '.next',
                        prevArrow: '.prev',
                        speed: 500
                    }
                }
            }
        });
    });
</script>