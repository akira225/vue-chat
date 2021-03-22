<template>
    <div class="col-md-8 col-xl-6 chat">
        <div class="card">
            <div class="card-body msg_card_body">
                <ChatMsg v-for="message in messages" :message="message"></ChatMsg>
            </div>
            <div class="card-footer">
                <div class="input-group">
                        <textarea v-model="NewMsgContent"
                                  name="" class="form-control type_msg"
                                  placeholder="Type your message..."
                                  @keypress.enter="ProcessMsg"></textarea>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import ChatMsg from "./ChatMsg";
    export default {
        name: "ChatComponent",
        components: {ChatMsg},
        data() {
            return {
                NewMsgContent : ""
            }
        },
        methods:{
            ProcessMsg:function (event) {
                event.preventDefault()
                if(this.NewMsgContent){
                    console.log(this.NewMsgContent)
                    this.$store.state.Connection.send(JSON.stringify({Command:"NEW_MESSAGE",
                        User:this.$store.state.UserName, Msg: this.NewMsgContent}))
                    this.NewMsgContent = ""
                }
            }
        },
        computed:{
            messages(){
                return this.$store.state.messages
            }
        }
    }
</script>

<style scoped>

</style>