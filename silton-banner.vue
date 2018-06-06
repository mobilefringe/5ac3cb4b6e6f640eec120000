<template>
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
  <!-- Item -->
  <div class="item">
    <div class="img-fill">
      <img src="https://i.imgur.com/ESMjChq.jpg" alt="">
      <div class="info">
        <div>
          <h3>Fully responsive Scales with its container</h3>
          <h5>Donec id ornare dui. Aenean tristique condimentum elit, quis blandit nisl varius sit amet. Sed eleifend felis quis massa viverra</h5>
        </div>
      </div>
    </div>
  </div>
  <!-- // Item -->
  <!-- Item -->
  <div class="item">
    <div class="img-fill">
      <img src="https://i.imgur.com/TDxSvHH.jpg" alt="">
      <div class="info">
        <div>
          <h3>Awesome Transtions With CSS3</h3>
          <h5>Donec id ornare dui. Aenean tristique condimentum elit, quis blandit nisl varius sit amet. Sed eleifend felis quis massa viverra</h5>
        </div>
      </div>
    </div>
  </div>
  <!-- // Item -->
  <!-- Item -->
  <div class="item">
    <div class="img-fill">
      <img src="https://i.imgur.com/p1XZ3Mu.jpg" alt="">
      <div class="info">
        <div>
          <h3>Separate settings per breakpoint</h3>
          <h5>Donec id ornare dui. Aenean tristique condimentum elit, quis blandit nisl varius sit amet. Sed eleifend felis quis massa viverra</h5>
        </div>
      </div>
    </div>
  </div>
  <!-- // Item -->
</div>
</template>

<style>
.edgeley {
    margin: 20px auto;
    padding: 0 8px;
    width: 100%;
    position: relative;
    box-sizing: border-box;
}
.edgeley .slick-slide {
    padding: 0 8px;
    box-sizing: border-box;
}
.edgeley .slick-slide .banner {
    max-width: 100%;
    position: relative;
    transform: scale(0.9);
    transition: all 1s ease-out;
    opacity: 0.5;    
}
.edgeley .slick-slide.slick-center .banner {
    transform: scale(1.1);
    transition: all 1s ease-out;
    opacity: 1;    
}
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