<template>
    <div class="weston">
        <div class="prev"></div>
        <slick ref="slick" :options="westonOptions">
			<div v-for="banner in banners" v-if="banners">
			    <div class="banner" v-bind:style="{ backgroundImage: 'url(' + banner.image_url + ')' }">
                    <div class="banner-legend"></div> 
                    <div class="banner-content"> 
                        <div class="banner-content-txt"> 
                            <h3>{{ banner.name }}</h3> 
                            <p>{{ banner.description }}</p> 
                        </div> 
                    </div> 
                </div> 
			</div>
		</slick>
		<div class="next"></div>
    </div>      
</template>

<style>
.weston {
    position: relative;
}
.prev {
    position: absolute;
    top: 50%;
    -moz-transform: translate(-50%, -50%);
	-webkit-transform: translate(-50%, -50%);
	-ms-transform: translate(-50%, -50%);
	transform: translate(-50%, -50%);
    left: -28px;
}

.prev:after {
    content: '\f104';
    font-family: FontAwesome;
    font-size: 2.75rem;
    font-weight: normal;
    font-style: normal;
    color: #000;    
}

.weston .next {
    position: absolute;
    top: 50%;
    -moz-transform: translate(-50%, -50%);
	-webkit-transform: translate(-50%, -50%);
	-ms-transform: translate(-50%, -50%);
	transform: translate(-50%, -50%);
    right: -36px;
}
.weston .next:after {
    content: '\f105';
    font-family: FontAwesome;
    font-size: 2.75rem;
    font-weight: normal;
    font-style: normal;
    color: #000;    
} 
.weston .prev:hover, .weston .next:hover {
    cursor: pointer;
}
.slick-dots button {
    background-color: #FFF;
    border: 2px solid #FFF;
    opacity: 0.5;
}
.slick-active button {
    opacity: 1;
}

/* Legend */
.banner-legend {
    position: absolute;
    bottom: 0;
    border: 500px solid transparent;
    border-left: 500px solid rgba(0, 0, 0, .7);
    border-bottom: 0;
}

/* Contents */
.banner-content {
    width: 100%;
    height: 100%;
    max-height: 500px;
    position: absolute;
    overflow: hidden;
}
.banner-content-txt {
    width: 400px;
    height: 150px;
    position: absolute;
    bottom: 0;
}
.banner-content-txt h3 {
    margin: 0 0 10px 30px;
    color: #FFF;
    text-align: left;
    text-transform: uppercase;
}
.banner-content-txt p {
    margin-left: 30px;
    color: #FFF;
    text-align :left;
}
.slick-slide.slick-active .banner-content-txt{
    animation: content-s 7.5s;
}

/* Text Animation */
@-webkit-keyframes content-s {
    0%  { left: -420px; }
    20% { left: 20px; }
    40% { left: 0; }
    60% { left: 0; }
    80% { left: 0; }
    100% { left: 0; }
}
@-moz-keyframes content-s {
    0%  { left: -420px; }
    20% { left: 20px; }
    40% { left: 0; }
    60% { left: 0; }
    80% { left: 0; }
    100% { left: 0; }
}
@keyframes content-s {
    0%  { left: -420px; }
    20% { left: 20px; }
    40% { left: 0; }
    60% { left: 0; }
    80% { left: 0; }
    100% { left: 0; }
}

@media(max-width: 768px){
    .banner {
        height: 300px;
    }   
    .banner-legend {
        border: 300px solid transparent;
        border-left: 300px solid rgba(0, 0, 0, .7);
        border-bottom: 0;
    }
    .banner-content-txt {
        height: 90px;
    }
    .banner-content-txt h3 {
        margin: 0 0 0 10px;
    }
    .banner-content-txt p {
        margin-left: 10px;
    }
}
</style>

<script>
    define(["Vue", "vue!vue-slick"], function (Vue, slick) {
        return Vue.component("weston-banner", {
            template: template, // the variable template will be injected,
            props:['banners'],
            data: function() {
                return {
                    westonOptions: {
                        autoplay: true,
                        autoplaySpeed: 8000,
                        cssEase: 'ease',
                        dots: true,
                        infinite: true,
                        nextArrow: '.weston .next',
                        prevArrow: '.prev',
                        speed: 500
                    }
                }
            }
        });
    });
</script>