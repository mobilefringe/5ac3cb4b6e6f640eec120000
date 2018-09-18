<template>
	<!-- Container for the images.-->
	<div id="feature_container_two" class="container">
		<article class='gallery'>
			<a class='gallery-link' href='https://unsplash.it/1600/1000?image=1081'>
				<figure class='gallery-image'>
					<img height='1000' src='https://unsplash.it/1600/1000?image=1081' width='1600'>
					<figcaption>Photo caption</figcaption>
				</figure>
			</a>
			<a class='gallery-link' href='https://unsplash.it/1000/1600?image=1014'>
				<figure class='gallery-image'>
					<img height='1600' src='https://unsplash.it/1000/1600?image=1014' width='1000'>
					<figcaption>Photo caption</figcaption>
				</figure>
			</a>
			<a class='gallery-link' href='https://unsplash.it/1600/1000?image=267'>
				<figure class='gallery-image'>
					<img height='1000' src='https://unsplash.it/1600/1000?image=267' width='1600'>
					<figcaption>Photo caption</figcaption>
				</figure>
			</a>
			<a class='gallery-link' href='https://unsplash.it/1400/1400?image=266'>
				<figure class='gallery-image'>
					<img height='1400' src='https://unsplash.it/1400/1400?image=266' width='1400'>
					<figcaption>Photo caption</figcaption>
				</figure>
			</a>
			<a class='gallery-link' href='https://unsplash.it/1000/1000?image=634'>
				<figure class='gallery-image'>
					<img height='1000' src='https://unsplash.it/1000/1000?image=634' width='1000'>
					<figcaption>Photo caption</figcaption>
				</figure>
			</a>
			<a class='gallery-link' href='https://unsplash.it/1600/1000?image=923'>
				<figure class='gallery-image'>
					<img height='1000' src='https://unsplash.it/1600/1000?image=923' width='1600'>
					<figcaption>Photo caption</figcaption>
				</figure>
			</a>
			<a class='gallery-link' href='https://unsplash.it/1200/1600?image=682'>
				<figure class='gallery-image'>
					<img height='1600' src='https://unsplash.it/1200/1600?image=682' width='1200'>
					<figcaption>Photo caption</figcaption>
				</figure>
			</a>
			<a class='gallery-link' href='https://unsplash.it/1400/1000?image=173'>
				<figure class='gallery-image'>
					<img height='1000' src='https://unsplash.it/1400/1000?image=173' width='1400'>
					<figcaption>Photo caption</figcaption>
				</figure>
			</a>
			<a class='gallery-link' href='https://unsplash.it/1000/1000?image=943'>
				<figure class='gallery-image'>
					<img height='1000' src='https://unsplash.it/1000/1000?image=943' width='1000'>
					<figcaption>Photo caption</figcaption>
				</figure>
			</a>
		</article>
	</div>
</template>

<style>

#feature_container_two {
    font-size: 0;
    width: 100%;
    margin-top: 50px;
    text-align: center;
}


</style>
<script>
    define(["Vue", "jquery"], function(Vue, $) {
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
