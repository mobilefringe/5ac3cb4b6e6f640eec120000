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
			
			
			
			    <!--<div class="banner" v-bind:style="{ backgroundImage: 'url(' + banner.image_url + ')' }">-->
                    <!--<div class="banner-legend"></div> -->
                    <!--<div class="banner-content"> -->
                    <!--    <div class="banner-content-txt"> -->
                    <!--        <h3>{{ banner.name }}</h3> -->
                    <!--        <p>{{ banner.description }}</p> -->
                    <!--    </div> -->
                    <!--</div> -->
                <!--</div> -->
			</div>
		</slick>
		<div class="next"></div>
    </div>
</template>

<style>
.weston {
    position: relative;
}

.slide{
  z-index: -1;
  padding: 0;
  position: absolute;
  width: 100%;
  height: 100vh;
  transition: z-index 1s ease;
  
  // Bring active layer to foreground
  &.is-active{
    z-index: 19;
    transition: z-index 1s ease;
  }
</style>

<script>
    define(["Vue", "vue!vue-slick"], function (Vue, slick) {
        return Vue.component("keele-banner", {
            template: template, // the variable template will be injected,
            props:['banners'],
            data: function() {
                return {
                    westonOptions: {
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