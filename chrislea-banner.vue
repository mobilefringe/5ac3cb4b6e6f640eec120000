<template>
    <div class="banners chrislea">
        <div class="prev"></div>
        <slick ref="slick" :options="chrisleaOptions">
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
.chrislea {
    margin: 20px auto;
    width: 100%;
    position: relative;
    box-sizing: border-box;
}
.banner {
    opacity: 0;
    position: relative;
    z-index: 0;
    transition: all 3s ease;
    width: 100%;
}
.details {
	padding: 20px;
	color: #FFF;
	position: absolute;
	bottom: 0;
	left: 0;
	z-index: 3;
}
.details span {
	display: block;
	opacity: 0;
	position: relative;
	top: 100px;
	transition-property: top, opacity;
	transition-duration: 0.3s;
	transition-delay: 0s;
}
.details .title h3 {
    font-weight: 600;
    line-height: 1;
}
.details .title .info {
	margin-top: 5px;
}
.slick-slide.slick-active .banner {
    opacity: 1;
}
.slick-slide.slick-active .banner .details:before, .slick-slide.slick-active .banner .details span {
	opacity: 1;
}
.slick-slide.slick-active .banner .details:before {
	top: 50%;
}
.slick-slide.slick-active .banner .details span {
	top: 0;
}
.slick-slide.slick-active .banner .details .title {
	transition-delay: 0.35s;
}
.slick-slide.slick-active .banner .details .info {
	transition-delay: 0.45s;
}
</style>

<script>
    define(["Vue", "vue!vue-slick"], function (Vue, slick) {
        return Vue.component("chrislea-banner", {
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
                        nextArrow: '.next_chris',
                        prevArrow: '.prev_chris'
                    }
                }
            }
        });
    });
</script>