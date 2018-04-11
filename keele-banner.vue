<template>
    <section class="slides"> 
        <section class="slides-nav">
            <nav class="slides-nav__nav">
                <button class="slides-nav__prev js-prev">Prev</button>
                <button class="slides-nav__next js-next">Next</button>
            </nav>
        </section>
        <section class="slide" v-for="banner in banners" v-if="banners">
            <div class="slide__content">
                <figure class="slide__figure">
                    <div class="slide__img" v-bind:style="{ backgroundImage: 'url(' + banner.image_url + ')' }"></div>
                </figure>
                <header class="slide__header">
                    <h2 class="slide__title">
                        <span class="title-line">
                            <span>Click, Key</span>
                        </span>
                        <span class="title-line">
                            <span>Or Scroll Fool</span>
                        </span>
                    </h2>
                </header>
            </div>
        </section>
    </section>
</template>

<style>

</style>

<script>
    define(["Vue", "jquery", "slice"], function (Vue, $, slice) {
        return Vue.component("keele-banner", {
            template: template, // the variable template will be injected,
            props:['banners'],
            data: function() {
                return {
                    
                }
            },
            created(){
                SliceSlider.init();    
            }
        });
    });
</script>