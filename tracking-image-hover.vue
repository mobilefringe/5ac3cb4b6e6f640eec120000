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

#feature_container_one .img-container:hover {
  transform: scale(1.1);
  /*
  Change the scale value as much as you want to change the amount of zoom on hover.
  */
}

#feature_container_one .card img {
  opacity: .5;
  transform: translate(0,0);
  /*
  Change the opacity value to change how "faded" you want the image to appear when it is not hovered.
  */
  transition: opacity .25s ease-in-out;
}

#feature_container_one .card img:hover {
  opacity: 1;
}
</style>
<script>
    define(["Vue", "jquery"], function(Vue, $) {
        return Vue.component("tracking-image-hover", {
            template: template, // the variable template will be injected
            props: {
                bannerList: {
                    type: Array,
                    // required: true
                }
            },
            data () {
                return {
                    
                }  
            },
            mounted() {
                
            },
            computed: {
               
            },
            methods: {
                
            }
        })
    });
</script>
