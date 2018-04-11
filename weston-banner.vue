<template>
    <div id="slider" class="banners">
        <div class="prev"></div>
        <slick ref="slick" :options="westonOptions">
			<div class="" v-for="banner in banners" v-if="banners">
				<div class="slider">
                    <div class="banner-legend"></div> 
                    <div class="banner-content"> 
                        <div class="banner-content-txt"> 
                            <h3> Your title </h3> 
                            <p> Your description </p> 
                        </div> 
                    </div> 
                    <div class="images"> 
                        <img :src="banner.image_url"> 
                    </div> 
                </div> 
			</div>
		</slick>
		<div class="next"></div>
    </div>      
</template>

<style>
/* Slider */
#slider {
    width: 100%;
    height: 500px;
    position: relative;
    overflow: hidden;
}
.slides {
    width: 100%;
    height: 400%;
    position: relative;
    -webkit-animation: slide 30s infinite;
    -moz-animation: slide 30s infinite;
    animation: slide 30s infinite;
}
.slider {
    width: 100%;
    height: 25%;
    position: relative;
    z-index: 1;
    overflow: hidden;
}

/* Legend */
.banner-legend {
    position: absolute;
    bottom: 0;
    border: 796px solid transparent;
    border-left: 796px solid rgba(0, 0, 0, .7);
    border-bottom: 0;
}

/* Contents */
.banner-content{
    width: 100%;
    height: 100%;
    max-height: 500px;
    position: absolute;
    overflow: hidden;
}
.banner-content-txt{
    width: 400px;
    height: 150px;
    position: absolute;
    bottom: 0;
    /*-webkit-animation:content-s 7.5s infinite;*/
    /*-moz-animation:content-s 7.5s infinite;*/
    /*animation: content-s 7.5s once;*/
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
/* Switch */
/*.switch{*/
/*    width:120px;*/
/*    height:10px;*/
/*    position:absolute;*/
/*    bottom:50px;*/
/*    z-index:99;*/
/*    left:30px;*/
/*}*/
/*.switch > ul{*/
/*  list-style:none;*/
/*}*/
/*.switch > ul > li{*/
/*  width:10px;*/
/*  height:10px;*/
/*  border-radius:50%;*/
/*  background:#333;*/
/*  float:left;*/
/*  margin-right:5px;*/
/*  cursor:pointer;*/
/*}*/
/*.switch ul{*/
/*  overflow:hidden;*/
/*}*/
/*.slick-slide.slick-active .banner-content-txt {*/
/*  width:100%;*/
/*  height:100%;*/
/*  border-radius:50%;*/
/*  background:#f39c12;*/
/*  position:relative;*/
/*  -webkit-animation:on 30s infinite;*/
/*  -moz-animation:on 30s infinite;*/
/*  animation:on 30s infinite;*/
/*}*/

/* Animation */
@-webkit-keyframes slide{
  0%,100%{
    margin-top:0%;
  }
  21%{
    margin-top:0%;
  }
  25%{
    margin-top:-500px;
  }
  46%{
    margin-top:-500px;
  }
  50%{
    margin-top:-1000px;
  }
  71%{
    margin-top:-1000px;
  }
  75%{
    margin-top:-1500px;
  }
  96%{
    margin-top:-1500px;
  }
}
@-moz-keyframes slide{
  0%,100%{
    margin-top:0%;
  }
  21%{
    margin-top:0%;
  }
  25%{
    margin-top:-500px;
  }
  46%{
    margin-top:-500px;
  }
  50%{
    margin-top:-1000px;
  }
  71%{
    margin-top:-1000px;
  }
  75%{
    margin-top:-1500px;
  }
  96%{
    margin-top:-1500px;
  }
}
@keyframes slide{
  0%,100%{
    margin-top:0%;
  }
  21%{
    margin-top:0%;
  }
  25%{
    margin-top:-500px;
  }
  46%{
    margin-top:-500px;
  }
  50%{
    margin-top:-1000px;
  }
  71%{
    margin-top:-1000px;
  }
  75%{
    margin-top:-1500px;
  }
  96%{
    margin-top:-1500px;
  }
}

/*@-webkit-keyframes content-s {*/
/*    0% { left: -420px; }*/
/*    10% { left: 0px; }*/
/*    30% {left:0px;}*/
/*    40% {left:0px;}*/
/*    50% {left:0px;}*/
/*    60% {left:0px;}*/
/*    70% {left:0;}*/
/*    80% {left:-420px;}*/
/*    90% {left:-420px;}*/
/*    100% {left:-420px;}*/
/*}*/
/*@-moz-keyframes content-s{*/
/*    0% {left:-420px;}*/
/*    10% {left:0px;}*/
/*    30% {left:0px;}*/
/*    40% {left:0px;}*/
/*    50% {left:0px;}*/
/*    60% {left:0px;}*/
/*    70%{left:0;}*/
/*    80%{left:-420px;}*/
/*    90%{left:-420px;}*/
/*    100%{left:-420px;}*/
/*}*/
@keyframes content-s{
    0%  { left: -420px; }
    20% { left: 20px; }
    /*15% { left: 0; }*/
    /*30% { left: 0; }*/
    40% { left: 0; }
    /*50% { left: 0; }*/
    60% { left: 0; }
    /*70% { left: 0; }*/
    80% { left: 0; }
    /*90% { left: 0; }*/
    100% { left: 0; }
}

@-webkit-keyframes on{
  0%,100%{
    margin-left:0%;
  }
  21%{
    margin-left:0%;
  }
  25%{
    margin-left:15px;
  }
  46%{
    margin-left:15px;
  }
  50%{
    margin-left:30px;
  }
  71%{
    margin-left:30px;
  }
  75%{
    margin-left:45px;
  }
  96%{
    margin-left:45px;
  }
}

@-moz-keyframes on{
  0%,100%{
    margin-left:0%;
  }
  21%{
    margin-left:0%;
  }
  25%{
    margin-left:15px;
  }
  46%{
    margin-left:15px;
  }
  50%{
    margin-left:30px;
  }
  71%{
    margin-left:30px;
  }
  75%{
    margin-left:45px;
  }
  96%{
    margin-left:45px;
  }
}

@keyframes on{
  0%,100%{
    margin-left:0%;
  }
  21%{
    margin-left:0%;
  }
  25%{
    margin-left:15px;
  }
  46%{
    margin-left:15px;
  }
  50%{
    margin-left:30px;
  }
  71%{
    margin-left:30px;
  }
  75%{
    margin-left:45px;
  }
  96%{
    margin-left:45px;
  }
}
</style>

<script>
    define(["Vue", "vue!vue-slick"], function (Vue, slick) {
        return Vue.component("weston-banner", {
            template: template, // the variable template will be injected,
            data: function() {
                return {
                    dataLoaded: false,
                    banners: [
                        { "image_url": "http://nikolaywerner.ru/files/2017-02/-nwf9500.jpg" },
                        { "image_url": "http://nikolaywerner.ru/files/2017-02/-nwf9506.jpg" },
                        { "image_url": "http://nikolaywerner.ru/files/2017-02/-nwf9449.jpg" },
                        { "image_url": "http://nikolaywerner.ru/files/2017-02/-nwf9541.jpg" }
                    ],
                    westonOptions: {
                        arrows: true,
                        autoplay: true,
                        // autoplaySpeed: 6000,
                        cssEase: 'ease',
                        dots: true,
                        infinite: true,
                        nextArrow: '.next',
                        prevArrow: '.prev',
                        slidesToShow: 1,
                    }
                }
            },
            created(){
                // this.loadData().then(response => {
                //   this.dataLoaded = true;
                // });
            },
            computed: {
                
            },
            methods: {
                // loadData: async function() {
                //     try {
                //         let results = await Promise.all([this.$store.dispatch("getData", "repos")]);
                //         return results;
                //     } catch (e) {
                //         console.log("Error loading data: " + e.message);
                //     }
                // }
            }
        });
    });
</script>