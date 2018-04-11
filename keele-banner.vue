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
.keele {
    position: relative;
}

.slide {
    padding: 0;
    width: 100%;
    height: 500px;
    /*position: absolute;*/
    z-index: -1;
    transition: z-index 1s ease;
}
/* Bring active layer to foreground */
.slick-active.is-active {
    z-index: 19;
    transition: z-index 1s ease;
}
.slide__content {
    position: relative;
    margin: 0 auto;
    height: 500px;
    /*height: $slide-content-size-sm;*/
    width: $slide-content-size-sm;
    top: (100% - $slide-content-size-sm) / 2;
}
.slide__figure {
    z-index: 7;
    position: absolute;
    left: 0;
    right: 0;
    margin: 0 auto;
    height: 100%;
    width: 100%;
    //overflow-y: hidden;
    transition: transform 0.5s $ease-cb-2;
}
/* Scale Image */
    /*.is-sliding &{*/
    /*  transform: scale(0.8);*/
    /*  transition: transform 0.5s $ease-cb-2;*/
    /*}*/

.slide__img {
    position: relative;
    display: block;
    background-size: cover;
    background-attachment: fixed;
    background-position: 50%;
    -webkit-backface-visibility: hidden;
    height: 0%;
    width: 100%;
    filter: grayscale(0%);
    transition: height 1s 1.4s $ease-cb-2, filter 0.4s 0.1s ease;
}

.slick-active.is-active .slide__img {
    height: 500px;
    opacity: 1;
    transition: height .5s .3s $ease-cb-3, filter 0.4s 0.1s ease;
}
    /*.is-sliding &{*/
    /*  filter: grayscale(100%);*/
    /*}*/

    /*@media (min-width: $mq-med){*/
    /*  height: $slide-content-size;*/
    /*  width: $slide-content-size;*/
    /*  top: (100% - $slide-content-size) / 2;*/
    /*}*/

</style>

<script>
    define(["Vue", "vue!vue-slick"], function (Vue, slick) {
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