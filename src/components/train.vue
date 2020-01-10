<template>
    <div id="app">
        <div class="container">
            <div class="train_big_box">
                <div class="train_box">
                    <div class="train_window_box">
                        <div class="train_window"></div>
                        <div class="train_window"></div>
                        <div class="train_window"></div>
                        <div class="train_window"></div>
                        <div class="train_window"></div>
                        <div class="train_window"></div>
                    </div>
                </div>
                <div class="train_box">
                    <div class="train_window_box">
                        <div class="train_window"></div>
                        <div class="train_window"></div>
                        <div class="train_window"></div>
                        <div class="train_window"></div>
                        <div class="train_window"></div>
                        <div class="train_window"></div>
                    </div>
                </div>
                <div class="train_box">
                    <div class="train_window_box">
                        <div class="train_window"></div>
                        <div class="train_window"></div>
                        <div class="train_window"></div>
                        <div class="train_window"></div>
                        <div class="train_window"></div>
                        <div class="train_window"></div>
                    </div>
                </div>
                <div class="train_box">
                    <div class="train_head">
                    <div class="train_window_box train_head_window_box">
                        <div class="train_window"></div>
                        <div class="train_window"></div>
                        <div class="train_window"></div>
                    </div>
                    </div>
                </div>
            </div><!-- train_big_box -->
            <div class="bridge_big_box" ref="bridge_big_box">
                <div class="bridge_box" ref="bridge_box_1">
                    <svg version="1.0" :style="{width:bridge.bridgeWidth}" viewBox="0 0 1000 1458" v-for="{item,index} in bridge.count" :key="index">
                        <g transform="translate(0.000000,1458.000000) scale(0.100000,-0.100000)" fill="#0b2347">
                            <path class="bridge_path"/>
                        </g>
                    </svg>
                </div>
                <div class="bridge_box" ref="bridge_box_2"></div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return {
            bridge:{
                bridgeWidth:300,
                count:'',
            },
            screenWidth: document.body.clientWidth,
        }
    },
    mounted(){
        const _this = this;
        const bridge_box_1 = this.$refs.bridge_box_1;
        const bridge_box_2 = this.$refs.bridge_box_2;
        const bridge_big_box = this.$refs.bridge_big_box;

       //场景向后
        function crossMarquee(){
            bridge_box_2.innerHTML=bridge_box_1.innerHTML;
            function Marquee(){
                bridge_box_1.offsetWidth<=bridge_big_box.scrollLeft ? bridge_big_box.scrollLeft-=bridge_box_1.offsetWidth : bridge_big_box.scrollLeft+=8;
            }
            let myMar = setInterval(Marquee,1);
            // bridge_big_box.onmouseover=function(){clearInterval(myMar);}
            // bridge_big_box.onmouseout=function(){myMar=setInterval(Marquee,speed);}
        }; 
        //对桥盒子进行填充,保证观众在大尺寸视窗情况下浏览时不会出现桥缺少情况
        function _fill_bridge(){
            let bridgeNum = Math.ceil(_this.screenWidth / _this.bridge.bridgeWidth)+1;
            for(let i = 0;i<bridgeNum;i++){
                _this.$set(_this.bridge,'count',i);
            }
        };
        const _fill_bridge_is_deal = new Promise(function(resolve,reject){
            _fill_bridge();
            resolve();
        });
        _fill_bridge_is_deal.then(function(){
            let bridgeWidthCount = _this.$refs.bridge_box_1.clientWidth;//当前桥的总宽度 
            crossMarquee();
            bridge_big_box.scrollLeft+100;
            console.log(bridgeWidthCount);
        });
    },
}
</script>

<style scoped>
.container {
    width:100vw;
    height: 100vh;
    z-index: 1;
    position: absolute;
}
.train_big_box{
    width: 100%;
    height: 35px;
    bottom: 300px;
    left:-1.5%;
    display: flex;
    position: absolute;
    animation:train_big_box 6s ease infinite alternate;
}
@keyframes train_big_box{
    0%{
        left:-1.5%;
    }
    50%{
        left:-4%;
    }
    100%{
        left:-2.5%;
    }
}
.train_box{
    width: 130px;
    height: 100%;
    background: #224779;
    margin-left:10px;
    position: relative;
    border-radius: 10px;
    box-shadow: inset 0px 1px 0 1px #f3d79b;
    transform: perspective(5px) rotateX(1deg);
}
.train_head{
    width:120px;
}
.train_head{
    width: 100%;
    height: 100%;
    background: #224779;
    content: "";
    top: 0px;
    left: 19px;
    transform: skew(25deg);
    box-shadow: inset -8px 8px 0 -7px #f3d79b;
    position: absolute;
    border-radius: 10px;
}
.train_window_box{
    height:100%;
    display: flex;
    justify-content: space-around;
    align-items: center;
    box-sizing: border-box;
    padding: 0 10px;
    transform: perspective(-5px) rotateX(-1deg);
}
.train_window{
    width: 10px;
    height: 10px;
    background:#edcd78;
    box-shadow: 0 0 7px #edcd78;
}
.train_head_window_box{
    transform: skewX(-20deg);
    justify-content: flex-end;
}
.train_head_window_box > .train_window{
    margin-left: 7px;
}
.bridge_big_box{
    width:100%;
    display: flex;
    box-sizing: border-box;
    position: absolute;
    bottom: -143px;
    overflow: hidden;
    border-top:3px solid #c6c6c6;
}
.bridge_box{
    display: flex;
}
.bridge_path{
    d:path('M0 13470 l0 -1110 53 0 c130 0 331 -35 492 -87 591 -189 1052 -687 1196 -1292 51 -213 49 96 49 -5638 l0 -5343 710 0 710 0 0 5343 c0 5734 -2 5425 49 5638 144 605 605 1103 1196 1292 436 139 901 110 1310 -82 494 -233 861 -683 986 -1210 51 -213 49 96 49 -5638 l0 -5343 705 0 705 0 0 5343 c0 5734 -2 5425 49 5638 144 605 605 1103 1196 1292 161 52 362 87 492 87 l53 0 0 1110 0 1110 -5000 0 -5000 0 0 -1110z');
}
</style>>