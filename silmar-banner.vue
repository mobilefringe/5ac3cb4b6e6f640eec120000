<template>
	<div class="row page_content" id="slide_container">
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

<style>
    /******* SLICE SLIDER STYLE *********/
.slide__title{
    font-size: 3.75em;
    color: #fff;
    line-height: normal;
    color: #eee;
    text-shadow: #000 0px -1px;
}
.slides-nav button{
    font-family: $font_family;  
}
.slides-nav button:after {
    height:2px;
    top:auto;
    bottom:0;
}
.slides-nav {
    z-index: 99;
    position: absolute;
    right: auto;
    display: block;
    /* align-items: center; */
    height: auto;
    width: 100%;
    bottom: 25px;
}
.slides-nav__nav {
    position: relative;
    right: 0;
    display: block;
    font-size: 1em;
    transform: initial;
    transform-origin: unset;
    text-align: center;
}

</style>
<script>
    define(["Vue", "jquery"], function(Vue, $) {
        return Vue.component("keele-banner", {
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
