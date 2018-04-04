<template>
    <!-- CHATBOT -->
    <div class="container">
        <!--Trigger the modal with a button -->
        <div id="chaticon" class="animated swing infinite" @click="showChat = !showChat"> <!-- data-toggle="modal" data-target="#chat_modal" -->
            <input id="chatbot" type="image" src="//codecloud.cdn.speedyrails.net/sites/596e75bc6e6f6473f8be0000/image/png/1501602564000/chat_icon.png" />
        </div>
        <!--Modal -->
        <div v-if="showChat" id="chat_modal" class="modal" :class="{ show_chat: showChat }"> <!-- tabindex="-1" role="dialog" aria-labelledby="chat_modalLabel" -->
            <div class="lab-modal-body modal-sm">
                <button type="button" class="close_chatbot"  @click="showChat = !showChat"> <!-- data-dismiss="modal" aria-label="Close" -->
                    <span aria-hidden="true">&times;</span>
                </button>
                <iframe id="chat_frame" :src="chatURL" width="100%" height="400px" frameBorder="0" allowfullscreen></iframe>
            </div>
        </div>
    </div>
</template>

<script>
    define(["Vue"], function (Vue) {
        return Vue.component("chatbot", {
            template: template, // the variable template will be injected,
            data: function () {
                return {
                    // dataLoaded: false,
                    showChat: false,
                    chatURL: 'http://preview-twinpines.codecloudapp.com/chat.html',
                };
            },
            created (){
                console.log(this.showChat)
                // this.loadData().then(response => {
                    // this.dataLoaded = true;
                // });
            },
            watch: {
                showChat: function() {
                    if(this.showChat == true){
                        document.body.classList.add("no_scroll");
                    } else if (this.showChat == false) {
                        document.body.classList.remove("no_scroll");
                    }
                }
            },
        });
    });
</script>