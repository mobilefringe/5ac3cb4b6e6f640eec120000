
<template>
	<div class="row page_content" id="slide_container">
	    <main>
            <section class="slides"> 
              
              <section class="slides-nav">
                <nav class="slides-nav__nav">
                  <button class="slides-nav__prev js-prev" ref="js_prev" @click="prevSlide">Prev</button>
                  <button class="slides-nav__next js-next" ref="js_next" @click="nextSlide">Next</button>
                </nav>
              </section>
            
              <section class="slide" v-for = "(banner,index) in banners" :class="{'is-active': (index==0)}">
                <div class="slide__content">
                  <figure class="slide__figure"><div class="slide__img" :style="{ backgroundImage: 'url(' + banner.image_url + ')' }"></div></figure>
                  <header class="slide__header">
                    <h2 class="slide__title">
                      <span class="title-line"><span>{{banner.name}}</span></span>
                      <span class="title-line"><span>{{banner.description}}</span></span>
                    </h2>
                  </header>
                </div>
              </section>
            </section>
        </main>
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
// .sli
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
