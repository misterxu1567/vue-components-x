<script src="../../vueTest/src/tpls/vue-test-toast/toast.js"></script>
<template>
    <div :class="{'toast':status}" :style="{animation: ani}">{{text}}</div>
</template>

<script>
    export default{
        name: 'toast',
        data (){
            return {
                status: false,
                text: '',
                duration: null,
                type: '',
            }
        },
        computed: {
            ani () {
                return this.status ? `${this.type}Frame ${this.duration}ms ease` : '';
            }
        },
        mounted () {
        }
    }
</script>

<style>
    .toast {
        position: fixed;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
        -webkit-transform: translate(-50%, -50%);
        -moz-transform: translate(-50%, -50%);
        -ms-transform: translate(-50%, -50%);
        padding: 0 20px;
        box-sizing: border-box;
        overflow: hidden;
        height: 40px;
        line-height: 40px;
        border-radius: 4px;
        font-size: 14px;
        min-width: 160px;
        background: rgba(0, 0, 0, 0.6);
        color: #fff;
        box-shadow: 0 0 12px rgba(0, 0, 0, 0.2);
        text-align: center;
        z-index: 9999;
    }
    /*展开动画*/
    @keyframes spreadFrame {
        0% {
            height: 0px;
        }
        5% {
            height: 40px;
        }
        95% {
            height: 40px;
        }
        100% {
            height: 0px;
        }
    }

    @-moz-keyframes spreadFrame {
        0% {
            height: 0px;
        }
        5% {
            height: 40px;
        }
        95% {
            height: 40px;
        }
        100% {
            height: 0px;
        }
    }

    @-webkit-keyframes spreadFrame {
        0% {
            height: 0px;
        }
        5% {
            height: 40px;
        }
        95% {
            height: 40px;
        }
        100% {
            height: 0px;
        }
    }
    @-ms-keyframes spreadFrame {
        0% {
            height: 0px;
        }
        5% {
            height: 40px;
        }
        95% {
            height: 40px;
        }
        100% {
            height: 0px;
        }
    }

    /*渐隐动画*/
    @keyframes fadeFrame {
        0% {
            display: block;
            opacity: 0;
        }
        8% {
            opacity: 1;
        }
        92% {
            opacity: 1;
        }
        100% {
            display: block;
            opacity: 0;
        }
    }
    @-webkit-keyframes fadeFrame {
        0% {
            display: block;
            opacity: 0;
        }
        8% {
            opacity: 1;
        }
        92% {
            opacity: 1;
        }
        100% {
            display: block;
            opacity: 0;
        }
    }
    @-ms-keyframes fadeFrame {
        0% {
            display: block;
            opacity: 0;
        }
        8% {
            opacity: 1;
        }
        92% {
            opacity: 1;
        }
        100% {
            display: block;
            opacity: 0;
        }
    }
    @-moz-keyframes fadeFrame {
        0% {
            display: block;
            opacity: 0;
        }
        8% {
            opacity: 1;
        }
        92% {
            opacity: 1;
        }
        100% {
            display: block;
            opacity: 0;
        }
    }
    /*从上渐隐*/
    @keyframes upFadeFrame {
        0% {
            display: block;
            top:46%;
            opacity: 0;
        }
        10% {
            top:50%;
            opacity: 1;
        }
        90% {
            top:50%;
            opacity: 1;
        }
        100% {
            display: block;
            top:46%;
            opacity: 0;
        }
    }
    @-webkit-keyframes upFadeFrame {
        0% {
            display: block;
            top:46%;
            opacity: 0;
        }
        10% {
            top:50%;
            opacity: 1;
        }
        90% {
            top:50%;
            opacity: 1;
        }
        100% {
            display: block;
            top:46%;
            opacity: 0;
        }
    }
    @-ms-keyframes upFadeFrame {
        0% {
            display: block;
            top:46%;
            opacity: 0;
        }
        10% {
            top:50%;
            opacity: 1;
        }
        90% {
            top:50%;
            opacity: 1;
        }
        100% {
            display: block;
            top:46%;
            opacity: 0;
        }
    }
    @-moz-keyframes upFadeFrame {
        0% {
            display: block;
            top:46%;
            opacity: 0;
        }
        10% {
            top:50%;
            opacity: 1;
        }
        90% {
            top:50%;
            opacity: 1;
        }
        100% {
            display: block;
            top:46%;
            opacity: 0;
        }
    }

</style>