<template>
    <div v-if="dataLoaded" id="overlay">
        <div class="loading-container">
            <vue-simple-spinner size="huge" :message="property.name + 'is loading...'"></vue-simple-spinner>
        </div>
    </div>
</template>

<script>
    define(["Vue", "vuex", "vue-simple-spinner"], function (Vue, Vuex, Spinner) {
        Vue.component("vue-simple-spinner", Spinner);
        return Vue.component("loader", {
            template: template, // the variable template will be injected,
            data: function () {
                return {
                    dataLoaded: false
                };
            },
            created (){
                // this.loadData().then(response => {
                    this.dataLoaded = true;
                // });
            },
            computed: {
                ...Vuex.mapGetters([
                    'property'
                ])
            }
        });
    });
</script>