<!-- 
  Container for the images.
-->
<div class="container">
  <!-- 
    The markup for each image is a div with the class of card. 
  -->
  <div class="card">
    <!-- 
      Each "card" has an image container, this is because you need the image to scale and move, we want the scaling to have a smooth transition. However if you add a transition for transform the transform property it will apply to both the scaling and the translation, causeing the translation to "lag" because as it updates where the mouse position is. 
    -->
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