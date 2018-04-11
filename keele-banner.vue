<template>
    <div class="keele banners">
        <div class="prev"></div>
        <slick ref="slick" :options="keeleOptions">
			<div v-for="banner in banners" v-if="banners">
			    <div class="slide">
                    <div class="slide__content">
                        <figure class="slide__figure">
                            <div class="slide__img" v-bind:style="{ backgroundImage: 'url(' + banner.image_url + ')' }"></div>
                        </figure>
                        <header class="slide__header">
                            <h2 class="slide__title">
                                <span class="title-line"><span>Click, Key</span></span>
                                <span class="title-line"><span>Or Scroll Fool</span></span>
                            </h2>
                        </header>
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
    define(["Vue", "jquery", "slice"], function (Vue, $, slice) {
        return Vue.component("keele-banner", {
            template: template, // the variable template will be injected,
            props:['banners'],
            data: function() {
                return {
                    keeleOptions: {
                        // autoplay: true,
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