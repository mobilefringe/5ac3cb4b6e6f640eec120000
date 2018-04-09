<template>
    <div v-if="dataLoaded">
        <div class="feature_menu_wrapper">
            <ul class="feature_menu_list">
                <li class="feature_menu_item">
                    <i class="fa fa-home" aria-hidden="true"></i>
                    <div class="slider">
                        <p>home</p>
                    </div>
                </li>
                <li class="feature_menu_item">
                    <i class="fa fa-file" aria-hidden="true"></i>
                    <div class="slider">
                        <p>files</p>
                    </div>
                </li>
                <li class="feature_menu_item">
                    <i class="fa fa-download" aria-hidden="true"></i>
                    <div class="slider">
                        <p>downloads</p>
                    </div>
                </li>
                <li class="feature_menu_item">
                    <i class="fa fa-envelope" aria-hidden="true"></i>
                    <div class="slider">
                        <p>notifications</p>
                    </div>
                </li>
                <li class="feature_menu_item">
                    <i class="fa fa-cog" aria-hidden="true"></i>
                    <div class="slider">
                        <p>settings</p>
                    </div>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
    define(["Vue"], function (Vue) {
        return Vue.component("feature-menu", {
            template: template, // the variable template will be injected,
            data: function () {
                return {
                    dataLoaded: false,
                };
            },
            created () {
                // this.loadData().then(response => {
                    this.dataLoaded = true;
                // });
            },
            // methods: {
            //     loadData: async function() {
            //         try {
            //             let results = await Promise.all([this.$store.dispatch('LOAD_PAGE_DATA', {url: "http://billingsbridge.mallmaverick.com/api/v3/billings/social.json"})]);
            //             return results;
            //         } catch (e) {
            //             console.log("Error loading data: " + e.message);
            //         }
            //     }
            // }
        });
    });
</script>