<template>
	<!-- Container for the images.-->
<div class="container">
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
#silmar_banner {
    position:relative;
    height: 100%;
    background: #110101;
    font-family: 'Roboto', sans-serif;
    /*overflow: hidden;*/
}
#silmar_banner.split-slideshow{
    height: 700px;
}
#silmar_banner .slideshow {
  position: absolute;
  z-index: 1;
  top: 0;
  left: 0;
  width: 100%;
  height: 700px;
  overflow: hidden;
}

#silmar_banner .slideshow .slider {
    width: 100%;
    height: 700px;
    z-index: 2;
}

#silmar_banner .slideshow .slider .item {
  height: 700px;
  width: 100%;
  position: relative;
  overflow: hidden;
  border: none;
}

#silmar_banner .slideshow .slider .item .text {
  display: none;
}

#silmar_banner .slideshow .slider .item img {
  min-width: 100%;
  min-height: 100%;
  position: absolute;
  top: 50%;
  left: 50%;
  -webkit-transform: translate(-50%, -50%);
      -ms-transform: translate(-50%, -50%);
          transform: translate(-50%, -50%);
}

#silmar_banner .slideshow .slick-dots {
  position: absolute;
  z-index: 100;
  width: 40px;
  height: auto;
  bottom: auto;
  top: 50%;
  right: 0;
  -webkit-transform: translateY(-50%);
      -ms-transform: translateY(-50%);
          transform: translateY(-50%);
  left: auto;
  color: #fff;
  display: block;
}

#silmar_banner .slideshow .slick-dots li {
  display: block;
  width: 100%;
  height: auto;
}

#silmar_banner .slideshow .slick-dots li button {
    position: relative;
    width: 20px;
    height: 15px;
    text-align: center;
    background-color: transparent;
    border: none;
}

#silmar_banner .slideshow .slick-dots li button:before {
  content: "";
  background: #fff;
  color: #fff;
  height: 2px;
  width: 20px;
  -webkit-border-radius: 0;
          border-radius: 0;
  position: absolute;
  top: 50%;
  right: 0;
  left: auto;
  -webkit-transform: translateY(-50%);
      -ms-transform: translateY(-50%);
          transform: translateY(-50%);
  -webkit-transition: all .3s ease-in-out;
  -o-transition: all .3s ease-in-out;
  transition: all .3s ease-in-out;
  opacity: 0.6;
}

#silmar_banner .slideshow .slick-dots li.slick-active button:before {
  width: 40px;
  opacity: 1;
}

#silmar_banner .slideshow.slideshow-right {
  left: 0;
  z-index: 1;
  width: 50%;
  pointer-events: none;
}

#silmar_banner .slideshow.slideshow-right .slider {
  left: 0;
  position: absolute;
}

#silmar_banner .slideshow-text {
  position: absolute;
  top: 50%;
  left: 50%;
  -webkit-transform: translate(-50%, -50%);
      -ms-transform: translate(-50%, -50%);
          transform: translate(-50%, -50%);
  z-index: 100;
  font-size: 80px;
  width: 100%;
  text-align: center;
  color: #fff;
  font-family: 'Roboto Condensed', sans-serif;
  font-weight: 100;
  pointer-events: none;
  text-transform: uppercase;
  letter-spacing: 20px;
  line-height: 0.8;
}

@media (max-width: 767px) {
    #silmar_banner .slideshow-text {
      font-size: 40px;
    }
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
