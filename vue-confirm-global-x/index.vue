<template>
    <div id="globalConfirmCont" :class="[state && animation]">
        <div class="confirm">
            <div class="tit">{{msg.title}}</div>
            <div class="text">{{msg.text}}</div>
            <div class="btnBox">
                <button @click="cancel">{{msg.btnCancel || '取消'}}</button>
                <button @click="sure">{{msg.btnSure || '确认'}}</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default{
        name: 'globalConfirm',
        data () {
          return {
              msg: {},
              animation: 'slideFade', // 默认动画
              state: false
          }
        },
        methods: {
            // 反馈
            sure () {
                this.state = false;
                this.bindSureFn();
            },
            cancel () {
                this.state = false;
                this.bindCancelFn();
            },
            // 被绑定函数
            bindSureFn () {},
            bindCancelFn () {},
            // 绑定外部执行函数
            then () {
                if (typeof arguments[0] === 'function') {
                    this.bindSureFn = arguments[0];
                }
                if (typeof arguments[1] === 'function') {
                    this.bindCancelFn = arguments[1];
                }
            }
        }
    }
</script>

<style>
    #globalConfirmCont {
        position: fixed;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.6);
        z-index: -1;
        opacity: 0;
        transition: all 0.5s ease;
        -webkit-transition: all 0.5s ease;
        -ms-transition: all 0.5s ease;
        -moz-transition: all 0.5s ease;
        -o-transition: all 0.5s ease;
    }
    #globalConfirmCont .confirm {
        position: absolute;
        left: 50%;
        top: 46%;
        transform: translate(-50%, -50%) scale(1);
        -webkit-transform: translate(-50%, -50%) scale(1);
        -ms-transform: translate(-50%, -50%) scale(1);
        -moz-transform: translate(-50%, -50%) scale(1);
        -o-transform: translate(-50%, -50%) scale(1);
        width: 400px;
        height: auto;
        background: #fff;
        border-radius: 6px;
        padding: 20px;
        transition: all 0.5s ease;
        -webkit-transition: all 0.5s ease;
        -ms-transition: all 0.5s ease;
        -moz-transition: all 0.5s ease;
        -o-transition: all 0.5s ease;
    }
    #globalConfirmCont .tit {
        font-size: 20px;
        text-align: center;
        color:#333;
    }
    #globalConfirmCont .text {
        font-size: 16px;
        text-align: center;
        padding: 16px 0 30px;
        color:#666;
        line-height: 24px;
    }
    #globalConfirmCont .btnBox {
        text-align: center;
        font-size: 0;
    }
    #globalConfirmCont .btnBox>button{
        display: inline-block;
        font-size: 16px;
        width: 30%;
        margin:0 5%;
        height: 40px;
        border-radius: 4px;
    }
    #globalConfirmCont .btnBox>button:nth-child(1){
        border:1px solid #ccc;
        color:#999;
    }
    #globalConfirmCont .btnBox>button:nth-child(2){
        background: #ff4141;
        color:#fff;
    }
    /*兼容手机*/
    @media screen and (max-width: 500px) {
        #globalConfirmCont .confirm {
            width: 80%;
        }
        #globalConfirmCont .tit {
            font-size: 0.38rem;
        }
        #globalConfirmCont .text {
            font-size: 0.28rem;
            line-height: 0.4rem;
            padding: 16px 0 20px;
        }
        #globalConfirmCont .btnBox>button{
            font-size: 0.28rem;
            width: 40%;
            margin:0 5%;
            height: 0.8rem;
        }
    }
    /*动画1*/
    #globalConfirmCont.slideFade{
        z-index: 9999;
        opacity: 1;
    }
    #globalConfirmCont.slideFade .confirm{
        top:50%;
    }
    /*动画2*/
    #globalConfirmCont.scaleFade{
        z-index: 9999;
        opacity: 1;
    }
    #globalConfirmCont.scaleFade .confirm{
        transform:translate(-50%, -50%) scale(1);
        -webkit-transform:translate(-50%, -50%) scale(1);
        -moz-transform:translate(-50%, -50%) scale(1);
        -ms-transform:translate(-50%, -50%) scale(1);
        -o-transform:translate(-50%, -50%) scale(1);
    }
</style>