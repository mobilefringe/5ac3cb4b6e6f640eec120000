<template>
	<!-- Container for the images.-->
	<div id="feature_container_two" class="container">
		<article class='gallery'>
			<a v-for="feature in feature_items" class='gallery-link' :href='feature.image_url' >
				<figure class='gallery-image'>
					<img :src='feature.image_url'>
					<figcaption>Photo caption</figcaption>
				</figure>
			</a>
			<!--<a class='gallery-link' href='https://unsplash.it/1000/1600?image=1014'>-->
			<!--	<figure class='gallery-image'>-->
			<!--		<img height='1600' src='https://unsplash.it/1000/1600?image=1014' width='1000'>-->
			<!--		<figcaption>Photo caption</figcaption>-->
			<!--	</figure>-->
			<!--</a>-->
			<!--<a class='gallery-link' href='https://unsplash.it/1600/1280?image=267'>-->
			<!--	<figure class='gallery-image'>-->
			<!--		<img height='1280' src='https://unsplash.it/1600/1280?image=267' width='1600'>-->
			<!--		<figcaption>Photo caption</figcaption>-->
			<!--	</figure>-->
			<!--</a>-->
			<!--<a class='gallery-link' href='https://unsplash.it/1400/1400?image=266'>-->
			<!--	<figure class='gallery-image'>-->
			<!--		<img height='1400' src='https://unsplash.it/1400/1400?image=266' width='1400'>-->
			<!--		<figcaption>Photo caption</figcaption>-->
			<!--	</figure>-->
			<!--</a>-->
			<!--<a class='gallery-link' href='https://unsplash.it/1000/1400?image=634'>-->
			<!--	<figure class='gallery-image'>-->
			<!--		<img height='1400' src='https://unsplash.it/1000/1400?image=634' width='1000'>-->
			<!--		<figcaption>Photo caption</figcaption>-->
			<!--	</figure>-->
			<!--</a>-->
			<!--<a class='gallery-link' href='https://unsplash.it/1600/1000?image=923'>-->
			<!--	<figure class='gallery-image'>-->
			<!--		<img height='1000' src='https://unsplash.it/1600/1000?image=923' width='1600'>-->
			<!--		<figcaption>Photo caption</figcaption>-->
			<!--	</figure>-->
			<!--</a>-->
			<!--<a class='gallery-link' href='https://unsplash.it/1200/1600?image=682'>-->
			<!--	<figure class='gallery-image'>-->
			<!--		<img height='1600' src='https://unsplash.it/1200/1600?image=682' width='1200'>-->
			<!--		<figcaption>Photo caption</figcaption>-->
			<!--	</figure>-->
			<!--</a>-->
			<!--<a class='gallery-link' href='https://unsplash.it/1400/1000?image=173'>-->
			<!--	<figure class='gallery-image'>-->
			<!--		<img height='1000' src='https://unsplash.it/1400/1000?image=173' width='1400'>-->
			<!--		<figcaption>Photo caption</figcaption>-->
			<!--	</figure>-->
			<!--</a>-->
			<!--<a class='gallery-link' href='https://unsplash.it/1000/980?image=943'>-->
			<!--	<figure class='gallery-image'>-->
			<!--		<img height='980' src='https://unsplash.it/1000/980?image=943' width='1000'>-->
			<!--		<figcaption>Photo caption</figcaption>-->
			<!--	</figure>-->
			<!--</a>-->
		</article>
	</div>
</template>

<style>
import "https://cdnjs.cloudflare.com/ajax/libs/magnific-popup.js/1.1.0/magnific-popup.min.css"

#feature_container_two {
    font-size: 0;
    width: 100%;
    margin-top: 50px;
    text-align: center;
}
html:not(.touch) #feature_container_two .gallery-image figcaption, #feature_container_two .touch .gallery-image figcaption, #feature_container_two .mfp-with-zoom .mfp-title {
  position: absolute;
  top: 50%;
  left: 50%;
  -webkit-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
  font-size: 14px;
  color: rgba(255, 255, 255, 0);
  padding: 1em;
  transition: all 0.2s ease;
  font-weight: 600;
  max-width: calc(100% - 9em);
  line-height: 1.25;
  text-align: center;
  box-sizing: border-box;
}
html:not(.touch) #feature_container_two .gallery-image figcaption:before, #feature_container_two .touch .gallery-image figcaption:before, #feature_container_two .mfp-with-zoom .mfp-title:before, #feature_container_two .gallery-image figcaption:after, #feature_container_two .touch .gallery-image figcaption:after, #feature_container_two .mfp-with-zoom .mfp-title:after {
  content: "";
  position: absolute;
  background: rgba(0, 0, 0, 0.2);
  width: 100%;
  height: 100%;
  padding: 1em;
  transition: all 0.3s ease-in-out;
  opacity: 0;
  z-index: -1;
    -webkit-box-sizing: unset; 
    -moz-box-sizing: unset;
    box-sizing: unset; 
}
html:not(.touch) #feature_container_two .gallery-image figcaption:before, #feature_container_two .touch .gallery-image figcaption:before, #feature_container_two .mfp-with-zoom .mfp-title:before, #feature_container_two html:not(.touch) .gallery-image figcaption:after, #feature_container_two .touch .gallery-image figcaption:after, #feature_container_two .mfp-with-zoom .mfp-title:after {
  right: 100%;
  bottom: 100%;
}
html:not(.touch) #feature_container_two .gallery-image figcaption:after, #feature_container_two .touch .gallery-image figcaption:after, #feature_container_two .mfp-with-zoom .mfp-title:after {
  left: 100%;
  top: 100%;
}
html:not(.touch) #feature_container_two .gallery-image figcaption.visible,html:not(.touch)  #feature_container_two .gallery-image:hover figcaption, #feature_container_two .touch .gallery-image figcaption, #feature_container_two .mfp-with-zoom .visible.mfp-title, #feature_container_two .mfp-with-zoom.mfp-ready .mfp-title {
  color: white;
  text-shadow: 0 0 1px rgba(0, 0, 0, 0.2);
  transition: all 0.2s ease 0.3s;
}
html:not(.touch) #feature_container_two .gallery-image figcaption.visible:before,html:not(.touch)  #feature_container_two .gallery-image:hover figcaption:before, #feature_container_two .touch .gallery-image figcaption:before, #feature_container_two .mfp-with-zoom .visible.mfp-title:before, #feature_container_two .mfp-with-zoom.mfp-ready .mfp-title:before, #feature_container_two html:not(.touch) .gallery-image figcaption.visible:after,html:not(.touch) #feature_container_two .gallery-image:hover figcaption:after, #feature_container_two .touch .gallery-image figcaption:after, #feature_container_two .mfp-with-zoom .visible.mfp-title:after, #feature_container_two .mfp-with-zoom.mfp-ready .mfp-title:after {
  opacity: 1;
}
html:not(.touch) #feature_container_two .gallery-image figcaption.visible:before,html:not(.touch)  #feature_container_two .gallery-image:hover figcaption:before, #feature_container_two .touch .gallery-image figcaption:before, #feature_container_two .mfp-with-zoom .visible.mfp-title:before, #feature_container_two .mfp-with-zoom.mfp-ready .mfp-title:before {
  right: -1.5em;
  bottom: -1.5em;
}
html:not(.touch) #feature_container_two .gallery-image figcaption.visible:after,html:not(.touch) #feature_container_two .gallery-image:hover figcaption:after, #feature_container_two .touch .gallery-image figcaption:after, #feature_container_two .mfp-with-zoom .visible.mfp-title:after, #feature_container_two .mfp-with-zoom.mfp-ready .mfp-title:after {
  left: -1.5em;
  top: -1.5em;
}
html #feature_container_two {
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  text-rendering: optimizelegibility;
}

#feature_container_two .gallery {
  -webkit-column-gap: 0;
  column-gap: 0;
}
@media (min-width: 480px) {
  #feature_container_two .gallery {
    -webkit-column-count: 2;
    column-count: 2;
  }
}
@media (min-width: 1260px) {
  #feature_container_two .gallery {
    -webkit-column-count: 3;
    column-count: 3;
  }
}
#feature_container_two .gallery-image {
  position: relative;
  margin: 0;
  padding: 0;
}
#feature_container_two .gallery-image:before, #feature_container_two .gallery-image:after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  border: 16px solid rgba(0, 0, 0, 0.1);
  transition: all 0.2s;
  will-change: border;
}
#feature_container_two .gallery-image:after {
  border-width: 0;
}
#feature_container_two .gallery-image img {
  display: block;
  max-width: 100%;
  height: auto;
}
html:not(.touch) #feature_container_two .gallery-image {
  overflow: hidden;
}
html:not(.touch) #feature_container_two .gallery-image:hover:before {
  border-width: 16px;
}
html:not(.touch) #feature_container_two .gallery-image:hover:after {
  border-width: 32px;
}
#feature_container_two .touch .gallery-image figcaption {
  top: auto;
  bottom: 2em;
}
#feature_container_two .mfp-with-zoom .mfp-container, #feature_container_two .mfp-with-zoom.mfp-bg {
  opacity: 0;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  transition: all 0.3s ease-out;
}
#feature_container_two .mfp-with-zoom.mfp-bg {
  background-color: rgba(0, 0, 0, 0.9);
}
#feature_container_two .mfp-with-zoom.mfp-ready .mfp-container {
  opacity: 1;
}
#feature_container_two .mfp-with-zoom.mfp-ready.mfp-bg {
  opacity: 1;
}
#feature_container_two .mfp-with-zoom.mfp-removing .mfp-container, #feature_container_two .mfp-with-zoom.mfp-removing.mfp-bg {
  opacity: 0;
}
#feature_container_two .mfp-with-zoom img.mfp-img {
  padding: 0;
}
#feature_container_two .mfp-with-zoom .mfp-figure:after {
  top: 0;
  bottom: 0;
}
#feature_container_two .mfp-with-zoom .mfp-container {
  padding: 0;
}
#feature_container_two .mfp-with-zoom .mfp-content {
  overflow: hidden;
}
#feature_container_two .mfp-with-zoom .mfp-bottom-bar {
  top: auto;
  bottom: 0;
  margin-top: 0;
}
#feature_container_two .mfp-with-zoom .mfp-title {
  top: auto;
  bottom: 2em;
}
#feature_container_two .mfp-arrow {
  opacity: 1;
  margin-top: 0 !important;
  width: 20%;
  height: 30%;
  -webkit-transform: translateY(-50%);
  transform: translateY(-50%);
}
#feature_container_two .mfp-arrow:before, #feature_container_two .mfp-arrow:after {
  margin: 0;
  border: none;
  width: 2rem;
  height: 2rem;
  -webkit-transform: rotate(-45deg) translate(-50%, -100%);
  transform: rotate(-45deg) translate(-50%, -100%);
  opacity: 1;
  top: 50%;
  left: 50%;
  transition: all 0.15s;
}
#feature_container_two .mfp-arrow:active {
  -webkit-transform: translateY(-50%) scale(0.95);
  transform: translateY(-50%) scale(0.95);
}
#feature_container_two .mfp-arrow-left {
  left: 0;
}
#feature_container_two .mfp-arrow-left:before, #feature_container_two .mfp-arrow-left:after {
  border-top: 2px solid white;
  border-left: 2px solid white;
}
#feature_container_two .mfp-arrow-left:after {
  margin-left: 2rem;
}
#feature_container_two .mfp-arrow-left:hover:before, #feature_container_two .mfp-arrow-left:active:before {
  margin-left: 2rem;
}
#feature_container_two .mfp-arrow-left:hover:after, #feature_container_two .mfp-arrow-left:active:after {
  margin-left: 0;
}
#feature_container_two .mfp-arrow-right {
  right: 0;
}
#feature_container_two .mfp-arrow-right:before, #feature_container_two .mfp-arrow-right:after {
  border-right: 2px solid white;
  border-bottom: 2px solid white;
}
#feature_container_two .mfp-arrow-right:after {
  margin-left: 2rem;
}
#feature_container_two .mfp-arrow-right:hover:before {
  margin-left: 2rem;
}
#feature_container_two .mfp-arrow-right:hover:after {
  margin-left: 0;
}
#feature_container_two button.mfp-close {
  opacity: 1;
  margin-top: 0 !important;
  width: 20%;
  height: 30%;
  font: 0/0 serif;
  text-shadow: none;
  color: transparent;
}
#feature_container_two button.mfp-close:before, #feature_container_two button.mfp-close:after {
  content: "";
  position: absolute;
  top: 50%;
  left: 50%;
  margin: 0;
  border: none;
  width: 2rem;
  height: 2rem;
  opacity: 1;
  transition: all 0.15s;
  -webkit-transform-origin: 0 0;
  transform-origin: 0 0;
  border-top: 2px solid white;
  border-left: 2px solid white;
}
#feature_container_two button.mfp-close:before {
  -webkit-transform: rotate(-45deg);
  transform: rotate(-45deg);
}
#feature_container_two button.mfp-close:after {
  -webkit-transform: rotate(135deg);
  transform: rotate(135deg);
}
#feature_container_two button.mfp-close:hover:before {
  -webkit-transform: rotate(135deg);
  transform: rotate(135deg);
}
#feature_container_two button.mfp-close:hover:after {
  -webkit-transform: rotate(315deg);
  transform: rotate(315deg);
}
#feature_container_two button.mfp-close:active {
  -webkit-transform: scale(0.95);
  transform: scale(0.95);
}
#feature_container_two a {
  text-decoration: none;
  color: inherit;
}
/*#feature_container_two [id=footer] {*/
/*  margin-top: 10vh;*/
/*  padding: 10vh 0;*/
/*  text-align: center;*/
/*}*/
/*#feature_container_two [id=footer] .container {*/
/*  position: relative;*/
/*}*/
/*#feature_container_two [id=footer] .container:before, #feature_container_two [id=footer] .container:after {*/
/*  content: "";*/
/*  position: absolute;*/
/*  bottom: 100%;*/
/*  left: 20px;*/
/*  z-index: 10;*/
/*  border-top: 2px solid;*/
/*  width: 10%;*/
/*  margin-bottom: 10vh;*/
/*}*/
/*#feature_container_two [id=footer] .container:after {*/
/*  left: auto;*/
/*  right: 20px;*/
/*}*/
/*#feature_container_two [id=footer] * {*/
/*  display: block;*/
/*}*/
/*#feature_container_two [id=footer] * + * {*/
/*  margin-top: 5vh;*/
/*}*/
/*#feature_container_two [id=footer] .logo {*/
/*  font-weight: 600;*/
/*  font-size: 1.5em;*/
/*}*/
/*#feature_container_two [id=footer] .copy {*/
/*  text-transform: uppercase;*/
/*  font-size: 0.75em;*/
/*  font-weight: 600;*/
/*}*/



</style>
<script>
    define(["Vue", "jquery", "magnific-popup"], function(Vue, $, MagnigicPopup) {
        return Vue.component("magnific-gallery", {
            template: template, // the variable template will be injected
            props: {
                featureItems: {
                    type: Array,
                    required: true
                }
            },
            data () {
                return {
                    
                }  
            },
            mounted() {
                //Creates an event that fires every time the mouse moves over any div with the class of "img".
                $(".img").mousemove(function(event){
                  
                  //Both the x and y value are calculated by taking the mouse x,y position on the page and subtracting it from the x,y position of the image on the page. "this" is the hovered element with the class of "img"
                  var mousex = event.pageX - $(this).offset().left;
                  var mousey = event.pageY - $(this).offset().top;
                  
                  
                  //If you just used the mouse position values the translation effect will only go up and to the right, by subtracting half of the length / width of the imagevfrom the values  we get either a positive or negitive number so that the image will move in any direction.
                  
                  //The 40 controls the amount of "movement" that will happen by giving us a smaller number, feel free to change it to get the effect that you want.
                  var imgx = (mousex - 300) / 40;
                  var imgy = (mousey - 200) / 40;
                  
                  //Adds a translation css styles to the image element
                  $(this).css("transform", "translate(" + imgx + "px," + imgy + "px)");
                });
                
                //This function will fire every time the user mouses off of the image. It resets the translation back to 0.
                $(".img").mouseout(function(){
                  $(this).css("transform", "translate(0px,0px)");
                });
            }
        })
    });
</script>
