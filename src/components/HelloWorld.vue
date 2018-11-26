<template>
<div id="content">
    <vue-waterfall-easy :imgsArr="imgsArr" @scrollReachBottom="fetchImgsData">
        <template slot-scope="props">
            <!-- props （所有imgsArr包括的内容） -->
            <div class="player_info">
                {{props.value.src}}
                <p>{{props.value.info}}</p>
                <p class="num">第{{props.index+1}}张图片</p>
            </div>
        </template>
    </vue-waterfall-easy>
</div>
</template>

<script>
import vueWaterfallEasy from 'vue-waterfall-easy'
export default {
    name: 'app',
    components: {
        vueWaterfallEasy
    },
    props: {
        gap: { // 图片间隔
            type: Number,
            default: 20
        },
        //    imgWidth: { // 指定图片的统一宽度
        //    type: Number,
        //  default: 240
        //},
        timeOut: { // 预加载事件小于500毫秒就不显示加载动画，增加用户体验
            type: Number,
            default: 500
        },
        height: {
            type: String,
            default: '100%'
        },
        //  imgsArr: { // 请求返回的图片数据，格式：[{src:'1.jpg','link':'url1' info:'自定义图片信息'},{src:'2.jpg','link':'url2',info:'自定义图片信息'}...]
        //     type: Array,
        //     required: true
        //   },
    },

    data() {
        return {
            imgsArr: [],
            fetchImgsArr: []

        }

    },

    methods: {
        initImgsArr(n, m) {
            //初始化图片数组的方法，把要加载的图片装入
            var arr = []
            for (var i = n; i < m; i++) {
                arr.push({
                    id: i,
                    src: `../static/img/${i + 1}.jpg`, //`./src/assets/img/${i + 1}.jpg`
                    link: 'https:/',
                    info: '一些图片描述文字'
                })
                //src为加载的图片的地址、link为超链接的链接地址、
                //info为自定义的图片展示信息，请根据自己的情况自行填写
            }
            return arr
        },
        fetchImgsData() { //获取新的图片数据的方法，用于页面滚动满足条件时调用
            this.imgsArr = this.imgsArr.concat(this.fetchImgsArr) //数组拼接，把下一批要加载的图片放入所有图片的数组中
        }
    },
    created() {
        this.imgsArr = this.initImgsArr(0, 10) //初始化第一次（即页面加载完毕时）要加载的图片数据
        this.fetchImgsArr = this.initImgsArr(10, 26) // 模拟每次请求的下一批新的图片的数据数据
    }

}
</script>

<style lang="scss" scoped>
#content {
    position: absolute;
    top: 32px;
    bottom: 0;
    width: 100%;
}
.player_info {
    text-align: center;
    color: #8888;
}
</style>
