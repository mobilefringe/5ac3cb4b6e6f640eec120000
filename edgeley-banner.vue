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
                        autoplaySpeed: 6000,
                        cssEase: 'ease',
                        dots: true,
                        infinite: true,
                        nextArrow: '.next',
                        prevArrow: '.prev'
                    }
                }
            }
        });
    });
</script>