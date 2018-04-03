<template>
    <!-- CHATBOT -->
    <div class="container">
        <!--Trigger the modal with a button -->
        <div id="chaticon" class="animated swing infinite" data-toggle="modal" data-target="#chat_modal">
            <input id="chatbot" type="image" src="//codecloud.cdn.speedyrails.net/sites/596e75bc6e6f6473f8be0000/image/png/1501602564000/chat_icon.png" />
        </div>
        <!--Modal -->
        <div class="modal" id="chat_modal" tabindex="-1" role="dialog" aria-labelledby="chat_modalLabel">
            <div class="lab-modal-body modal-sm">
                <button type="button" class="close_chatbot" data-dismiss="modal" aria-label="Close">
                    <span aria-hidden="true">&times;</span>
                </button>
                <iframe id="chat_frame" src='https://emmachat.codecloudapp.com/chat' height="400px"></iframe>
            </div>
        </div>
    </div>
</template>

<script>
    define(["Vue", "vuex", ], function (Vue, Vuex, ) {
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