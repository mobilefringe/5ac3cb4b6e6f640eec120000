<template>
    <div class="banners edgeley">
        <div class="prev"></div>
        <slick ref="slick" :options="edgeleyOptions">
			<div v-for="banner in banners" v-if="banners">
				<div class="banner" v-bind:style="{ backgroundImage: 'url(' + banner.image_url + ')' }"></div>
			</div>
		</slick>
		<div class="next"></div>
    </div>
</template>

<style>
.edgeley {
    margin: 20px auto;
    padding: 0 8px;
    width: 100%;
    position: relative;
    box-sizing: border-box;
}
.edgeley .slick-slide {
    padding: 0 8px;
    box-sizing: border-box;
}
.edgeley .slick-slide .banner {
    max-width: 100%;
    position: relative;
    transform: scale(0.9);
    transition: all 1s ease-out;
    opacity: 0.5;    
}
.edgeley .slick-slide.slick-center .banner {
    transform: scale(1.1);
    transition: all 1s ease-out;
    opacity: 1;    
}
</style>

<script>
    define(["Vue", "vue!vue-slick"], function (Vue, slick) {
        return Vue.component("edgeley-banner", {
            template: template, // the variable template will be injected,
            props:['banners'],
            data: function() {
                return {
                    edgeleyOptions: {
                        autoplay: true,
                        autoplaySpeed: 8000,
                        centerMode: true,
                        centerPadding: '15%',
                        slidesToShow: 1,
                        speed: 1000,
                        nextArrow: '.next',
                        prevArrow: '.prev',
                    }
                }
            }
        });
    });
</script>