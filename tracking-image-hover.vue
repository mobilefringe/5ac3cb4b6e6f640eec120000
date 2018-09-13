<template>
	<!-- Container for the images.-->
    <div id="feature_container_one" class="container">
        <!--   The markup for each image is a div with the class of card.  -->
        <div class="card">
            <!--   Each "card" has an image container, this is because you need the image to scale and move, we want the scaling to have a smooth transition. However if you add a transition for transform the transform property it will apply to both the scaling and the translation, causeing the translation to "lag" because as it updates where the mouse position is.   -->
            <div class="img-container">
                <img id="street" class="img" src="http://themenectar.com/demo/salient-frostwave/wp-content/uploads/2013/06/night-to-remember1-600x400.jpg" alt="street" />
            </div>
        </div>
  
        <div class="card">
            <div class="img-container">
                <img id="hill" class="img" src="http://themenectar.com/demo/salient-frostwave/wp-content/uploads/2013/06/great-valley1-600x400.jpg" alt="hill" />
            </div>
        </div>
  
        <div class="card">
            <div class="img-container">
                <img id="lake" class="img" src="http://themenectar.com/demo/salient-frostwave/wp-content/uploads/2013/06/on-the-lake1-600x400.jpg" alt="lake" />
            </div>
        </div>
    </div>
</template>

<style>

#feature_container_one.container {
  font-size: 0;
  width: 100%;
  margin-top: 50px;
  text-align: center;
}

#feature_container_one .card {
  overflow: hidden;
  position: relative;
  display: inline-block;
  height: 400px;
  width: 600px;
  /*
  Each "card" is set to 600x400px because that is the size of  the image, adjust as needed. Make sure the overflow is set to hidden or else when the img scales it will clip with the other images.
  */
}

#feature_container_one .img-container {
  transition: transform .1s ease;
}

.img-container:hover {
  transform: scale(1.1);
  /*
  Change the scale value as much as you want to change the amount of zoom on hover.
  */
}

.card img {
  opacity: .5;
  transform: translate(0,0);
  /*
  Change the opacity value to change how "faded" you want the image to appear when it is not hovered.
  */
  transition: opacity .25s ease-in-out;
}

.card img:hover {
  opacity: 1;
}
</style>
<script>
    define(["Vue", "jquery", "vue!vue-slick"], function(Vue, $, vueSlick) {
        return Vue.component("tracking-image-hover", {
            template: template, // the variable template will be injected
            props: {
                bannerList: {
                    type: Array,
                    required: true
                }
            },
            data () {
                return {
                    maxItems: this.bannerList.length,
                    slideLeftOptions: {
                        vertical: true,
                        verticalSwiping: true,
                        arrows: false,
                        infinite: true,
                        dots: true,
                        speed: 1000,
                        cssEase: "cubic-bezier(0.7, 0, 0.3, 1)"
                    },
                    slideRightOptions: { 
                        swipe: false,
                        vertical: true,
                        arrows: false,
                        infinite: true,
                        speed: 950,
                        cssEase: "cubic-bezier(0.7, 0, 0.3, 1)",
                        initialSlide: (this.maxItems-1)
                    },
                    slidetextOptions: {
                        swipe: false,
                        vertical: true,
                        arrows: false,
                        infinite: true,
                        speed: 900,
                        cssEase: "cubic-bezier(0.7, 0, 0.3, 1)"
                    },
                }  
            },
            mounted() {
                console.log(this.$refs.sliderRight, this.$refs.sliderLeft);
                var left_slider= $(".slider.slideshow-left");
                console.log("left_slider",left_slider.width());
                var left_slider_width= left_slider.width();
                var right_slider = document.querySelector('#silmar_banner .slideshow.slideshow-right .slider');//[0];
                right_slider.setAttribute("style", "width: "+left_slider_width+"px;")
                console.log(right_slider);
                
            },
            computed: {
                allBanners () {
                    var banners = this.bannerList;
                    // banners_image = ["https://raw.githubusercontent.com/supahfunk/supah-codepen/master/canyon-2.jpg","https://raw.githubusercontent.com/supahfunk/supah-codepen/master/canyon-3.jpg","https://raw.githubusercontent.com/supahfunk/supah-codepen/master/canyon-4.jpg", "https://raw.githubusercontent.com/supahfunk/supah-codepen/master/canyon-1.jpg"];
                    // _.forEach(banners, function (val, key){
                    //     val.image_url = banners_image[key];
                    // });
                    return banners;
                },
                allBannersReverse() {
                    return _.reverse(this.allBanners);
                }
            },
            methods: {
                beforeChange (event, slick, currentSlide, nextSlide) {
                    var rightEL = this.$refs.sliderRight.$el;
                    var textEL = this.$refs.textSlider.$el;
                    if (
                      currentSlide > nextSlide &&
                      nextSlide == 0 &&
                      currentSlide == this.maxItems - 1
                    ) {
                      $(rightEL).slick("slickGoTo", -1);
                      $(textEL).slick("slickGoTo", this.maxItems);
                    } else if (
                      currentSlide < nextSlide &&
                      currentSlide == 0 &&
                      nextSlide == this.maxItems - 1
                    ) {
                      $(rightEL).slick("slickGoTo", this.maxItems);
                      $(textEL).slick("slickGoTo", -1);
                    } else {
                      $(rightEL).slick(
                        "slickGoTo",
                        this.maxItems - 1 - nextSlide
                      );
                      $(textEL).slick("slickGoTo", nextSlide);
                    }
                }
            }
        })
    });
</script>
