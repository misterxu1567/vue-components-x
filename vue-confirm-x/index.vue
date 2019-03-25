<template>
    <transition :name="animation">
        <div id="confirmContainer">
            <div class="confirm">
                <div class="tit">{{msg.title}}</div>
                <div class="text">{{msg.text}}</div>
                <div class="btnBox">
                    <button @click="feedbackFn(false)">{{msg.btnCancel || '取消'}}</button>
                    <button @click="feedbackFn(true)">{{msg.btnSure || '确认'}}</button>
                </div>
            </div>
        </div>
    </transition>
</template>

<script>
    export default{
        name: 'confirm',
        props: {
            msg:{
                type: Object,
                required: true,
                default: {
                    title: '我是标题',
                    text: '我是描述',
                    btnSure: '',
                    btnCancel: '',
                }
            },
            animation: {
                type: String,
                default: 'slide-fade'
            }
        },
        methods: {
            // 点击反馈
            feedbackFn (state) {
                this.$emit('callback', state);
            }
        }
    }
</script>

<style>
    #confirmContainer {
        position: fixed;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.6);
    }
    #confirmContainer .confirm {
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
        -webkit-transform: translate(-50%, -50%);
        -ms-transform: translate(-50%, -50%);
        -moz-transform: translate(-50%, -50%);
        width: 400px;
        height: auto;
        background: #fff;
        border-radius: 6px;
        padding: 20px;
        transform-origin: 50% 0;
        opacity: 1;
    }

    #confirmContainer .tit {
        font-size: 20px;
        text-align: center;
        color:#333;
    }
    #confirmContainer .text {
        font-size: 16px;
        text-align: center;
        padding: 16px 0 30px;
        color:#666;
        line-height: 24px;
    }
    #confirmContainer .btnBox {
        text-align: center;
        font-size: 0;
    }
    #confirmContainer .btnBox>button{
        display: inline-block;
        font-size: 16px;
        width: 30%;
        margin:0 5%;
        height: 40px;
        border-radius: 4px;
    }
    #confirmContainer .btnBox>button:nth-child(1){
        border:1px solid #ccc;
        color:#999;
    }
    #confirmContainer .btnBox>button:nth-child(2){
        background: #ff4141;
        color:#fff;
    }
    /*兼容手机*/
    @media screen and (max-width: 500px) {
        #confirmContainer .confirm {
            width: 80%;
        }
        #confirmContainer .tit {
            font-size: 0.38rem;
        }
        #confirmContainer .text {
            font-size: 0.28rem;
            line-height: 0.4rem;
            padding: 16px 0 20px;
        }
        #confirmContainer .btnBox>button{
            font-size: 0.28rem;
            width: 40%;
            margin:0 5%;
            height: 0.8rem;
        }
    }
    /*切换动画*/
    .slide-fade-enter-active {
        transition: all .5s ease;
    }
    .slide-fade-leave-active {
        transition: all .5s ease;
    }
    .slide-fade-enter, .slide-fade-leave-to
        /* .slide-fade-leave-active for below version 2.1.8 */ {
        transform: translateY(-10px);
        opacity: 0;
    }
    /**/
    .scale-fade-enter-active {
        transition: all .5s ease;
    }
    .scale-fade-leave-active {
        transition: all .5s ease;
    }
    .scale-fade-enter, .scale-fade-leave-to
        /* .slide-fade-leave-active for below version 2.1.8 */ {
        transform: scale(1.1);
        opacity: 0;
    }
</style>