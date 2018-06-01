<template>
	<div class="row page_content" id="silmar_banner">
        <div class="split-slideshow">
            <div class="slideshow">
                <div class="slider">
                    <div class="item">
                        <img src="https://raw.githubusercontent.com/supahfunk/supah-codepen/master/canyon-2.jpg" />
                    </div>
                    <div class="item">
                        <img src="https://raw.githubusercontent.com/supahfunk/supah-codepen/master/canyon-3.jpg" />
                    </div>
                    <div class="item">
                        <img src="https://raw.githubusercontent.com/supahfunk/supah-codepen/master/canyon-4.jpg" />
                     </div>
                    <div class="item">
                        <img src="https://raw.githubusercontent.com/supahfunk/supah-codepen/master/canyon-1.jpg" />
                    </div>
                </div>
            </div>
            <div class="slideshow-text">
                <div class="item">Canyon</div>
                <div class="item">Desert</div>
                <div class="item">Erosion</div>
                <div class="item">Shape</div>
            </div>
        </div>
    </div>
</template>

<style lang="scss">
body,
html {
    height: 100%;
    background: #110101;
    font-family: 'Roboto', sans-serif;
    overflow: hidden;
}
#silmar_banner * {
  outline: none;
}
#silmar_banner .slideshow {
    position: absolute;
    z-index: 1;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    overflow: hidden;
  
    #silmar_banner .slider {
        width: 100vw;
        height: 100vw;
        z-index: 2;
        
    
    
    .item {
      height: 100vh;
      width: 100vw;
      position: relative;
      overflow: hidden;
      border: none;
      
      .text {
        display: none;
      }
      
      img {
        min-width: 101%;
        min-height: 101%;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
      }
    }
  }
  
  .slick-dots {
    position: fixed;
    z-index: 100;
    width: 40px;
    height: auto;
    bottom: auto;
    top: 50%;
    right: 0;
    transform: translateY(-50%);
    left: auto;
    color: #fff;
    display: block;
    
    li {
      display: block;
      width: 100%;
      height: auto;
      
      & button {
        position: relative;
        width: 20px;
        height: 15px;
        text-align: center;
        
        &:before {
          content: '';
          background: #fff;
          color: #fff;
          height: 2px;
          width: 20px;
          border-radius: 0;
          position: absolute;
          top: 50%;
          right: 0;
          left: auto;
          transform: translateY(-50%);
          transition: all .3s ease-in-out;
          opacity: 0.6;
        }
      }
      
      &.slick-active {
        button {
          &:before {
            width: 40px;
            opacity: 1;
          }
        }
      }
    }
  }
  
  &.slideshow-right {
    left: 0;
    z-index: 1;
    width: 50vw;
    pointer-events: none;
    
    .slider {
      left: 0;
      position: absolute;
    }
  }
}

.slideshow-text {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 100;
  font-size: 80px;
  width: 100vw;
  text-align: center;
  color: #fff;
  font-family: 'Roboto Condensed', sans-serif;
  font-weight: 100;
  pointer-events: none;
  text-transform: uppercase;
  letter-spacing: 20px;
  line-height: 0.8;
  
  @media (max-width: 767px) {
    font-size: 40px;
  }
  
}

</style>
<script>
    define(["Vue", "jquery"], function(Vue, $) {
        return Vue.component("silmar-banner", {
            template: template, // the variable template will be injected
            props: {
                banners: {
                    type: Array,
                    required: true
                },
                delta: {
                    type: Number,
                    default: 0
                },
                autoPlaySpeed: {
                    type:Number,
                    default: 10000
                }
            },
            data () {
                return {
                    currentSlideIndex: 0,
                    scrollThreshold: 40,
                    slides: [],
                    numSlides: this.banners.length
                }  
            },
            mounted() {
                this.slides = $('.slide');
                this.interval = setInterval(function () {
                    this.nextSlide();
                }.bind(this), this.autoPlaySpeed); 
            },
            methods: {
                prevSlide() {
                    // If on first slide, loop to last
                    if (this.currentSlideIndex <= 0) {
                        this.currentSlideIndex = this.numSlides;
                    }
                    this.currentSlideIndex--;

                    this.showSlide();
                },
                nextSlide() {
                    this.currentSlideIndex++;

                    // If on last slide, loop to first
                    if (this.currentSlideIndex >= this.numSlides) {
                        this.currentSlideIndex = 0;
                    }

                    this.showSlide();
                },
                showSlide() {
                    var vm = this;
                    // reset
                    this.delta = 0;
                    // Bail if we're already sliding
                    if ($('#slide_container').hasClass('is-sliding')) {
                        return;
                    }
                    // Loop through our slides
                    this.slides.each(function(i, slide) {
                        // Toggle the is-active class to show slide
                        $(slide).toggleClass('is-active', (i === vm.currentSlideIndex));
                        $(slide).toggleClass('is-prev', (i === vm.currentSlideIndex - 1));
                        $(slide).toggleClass('is-next', (i === vm.currentSlideIndex + 1));
                        
                        // Add and remove is-sliding class
                        $('#slide_container').addClass('is-sliding');

                        setTimeout(function() {
                            $('#slide_container').removeClass('is-sliding');
                        }, 1000);
                    });
                }
            }
        })
    });
</script>
