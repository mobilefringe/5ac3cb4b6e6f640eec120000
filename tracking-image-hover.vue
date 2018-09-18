<template>
	<!-- Container for the images.-->
    <div id="feature_container_one" class="container">
        <!--   The markup for each image is a div with the class of card.  -->
        <div class="card" v-for="item in featureItems">
            <!--   Each "card" has an image container, this is because you need the image to scale and move, we want the scaling to have a smooth transition. However if you add a transition for transform the transform property it will apply to both the scaling and the translation, causeing the translation to "lag" because as it updates where the mouse position is.   -->
            <div class="img-container">
                <img :id="item.name" class="img" :src="item.image_url" alt="item.name" />
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
  width: 300px;
      margin: 15px;
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
