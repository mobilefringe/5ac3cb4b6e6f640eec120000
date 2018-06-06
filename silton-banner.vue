<template>
	<div id="silton_banner">
		<div class="Modern-Slider">
			<!-- Item -->
			<div class="item">
				<div class="img-fill">
					<img src="https://i.imgur.com/JNKiMHU.jpg" alt="">
					<div class="info">
						<div>
							<h3>Full Width Slider With Layers</h3>
							<h5>You can easily add image, html formatted texts and video layers over each slide and each layer accepts unique animation.</h5>
						</div>
					</div>
				</div>
			</div>
			<!-- // Item -->
		</div>
	</div>
</template>

<style>

</style>

<script>
    define(["Vue", "vue!vue-slick"], function (Vue, slick) {
        return Vue.component("silton-banner", {
            template: template, // the variable template will be injected,
            props:['banners'],
            data: function() {
                return {
                    edgeleyOptions: {
                        autoplay: true,
                        autoplaySpeed: 8000,
                        centerMode: true,
                        centerPadding: '12%',
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