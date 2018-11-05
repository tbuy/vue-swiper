<template>
    <div class="c_scrollText" ref="scrollText" :style="{ height:height}">
        <div class="text" ref="move">
          {{ content }}
        </div>
        <div class="text" ref="moveTwo" v-show="isShowTextTwo">
          {{ content }}
        </div>
    </div>
</template>
<script type="text/ecmascript-6">

    export default {
        props: {
            //高度
            height: {
                type: String,
                default: '50px'
            },
            //内容
            content: {
                type: String,
                required: true
            },
            //滚动速度(1-5)
            speed: {
                type: Number,
                default: 5
            },
            //跟随标题距离(px)
            distance: {
                type: Number,
                default: 100
            }

        },
        data: function () {
            return {
                //是否显示跟随标题
                isShowTextTwo: false,
            }
        },
        // watch:{
        //     content(){
        //         //解决 切歌走马灯失效
        //         clearInterval(this._timer);
        //         this.isShowTextTwo = false;
        //         this.$refs.moveTwo.style.transform = undefined
        //         this.$refs.move.style.transform = undefined;
        //         this.$refs.move.style.left = 0;

        //         this.$nextTick(()=>{
        //             var _step = 0;
        //             //滚动的标题宽度
        //             var _width = this.$refs.move.offsetWidth;
        //             //外框的宽度
        //             var _outsideWidth = this.$refs.scrollText.offsetWidth;
        //             //跟随标题位置
        //             this.$refs.moveTwo.style.left = _width + this.distance + 'px';

        //             if(_width > _outsideWidth) {
        //                 //显示跟随标题
        //                 this.isShowTextTwo = true;
        //                 this._timer = setInterval(()=>{
        //                     if(_step == -_width - this.distance ) {
        //                         setTimeout(()=>{
        //                             _step = 1
        //                         }, 1000)
        //                     } else {
        //                         _step -= this.speed;
        //                         this.$refs.move.style.transform = 'translate3D('+ _step +'px, 0, 0)';
        //                         this.$refs.moveTwo.style.transform = 'translate3D('+ _step +'px, 0, 0)';
        //                     }
        //                 }, 80)
        //             }else{
        //                 this.$refs.move.style.transform = 'translate3D(-50%, 0, 0)';
        //                 this.$refs.move.style.left = '50%';
        //             }
        //         })


        //     }
        // },
        mounted: function () {
            //限制速度
            if(this.speed < 1) {
                this.speed = 1
            }else if(this.speed > 5){
                this.speed = 5
            }

            var _step = 0;
            //滚动的标题宽度
            var _width = this.$refs.move.offsetWidth;
            //外框的宽度
            var _outsideWidth = this.$refs.scrollText.offsetWidth;
            //跟随标题位置
            this.$refs.moveTwo.style.left = _width + this.distance + 'px';

            clearInterval(this._timer);

            if(_width > _outsideWidth) {
                //显示跟随标题
                this.isShowTextTwo = true;
                this._timer = setInterval(()=>{
                    if(_step == -_width - this.distance ) {
                        debugger
                        setTimeout(()=>{
                            _step = 1
                        }, 1000)
                    } else {
                        _step -= this.speed;
                        this.$refs.move.style.transform = 'translate3D('+ _step +'px, 0, 0)';
                        this.$refs.moveTwo.style.transform = 'translate3D('+ _step +'px, 0, 0)';
                    }
                }, 80)
            }else{
                this.$refs.move.style.transform = 'translate3D(-50%, 0, 0)';
                this.$refs.move.style.left = '50%';
            }
        },
        destroyed: function () {
            clearInterval(this._timer);
        }

    }
</script>
<style scoped>
    .c_scrollText {
        width: 100%;
        overflow: hidden;
        position: relative;
    }
    .text {
        position: absolute;
        white-space: nowrap;

    }

</style>
