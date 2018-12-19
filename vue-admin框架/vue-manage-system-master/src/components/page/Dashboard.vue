<template>
    <div class="Dashboard">
        <div class="bg"></div>
        <div class="index-slider">
            <el-carousel height="150px">
                <el-carousel-item v-for="item in 2" :key="item">
                    <el-row :gutter="20">
                        <el-col v-for="(d,index) in sliderData" :span="8">
                            <div class="sliderCon">
                                <div class="sbg"></div>
                                    <div class="slider-inner">
                                        <span class="water-icon  hidden-sm-and-down"></span>
                                        <div class="see-blank">
                                            <p>{{d.title}}</p>
                                            <span class="led-text">{{d.data}}</span>
                                            <small>T</small>
                                        </div>
                                        <div class="tong-huan-bi hidden-md-and-down">
                                            <p class="tongbi">
                                                <span>同比：</span>
                                                <span class="tongbi-detail">{{d.tongbi}}<small>%</small></span>
                                                
                                                <i :class="d.class1"></i>
                                            </p>
                                            <p class="huanbi">
                                                <span>环比：</span>
                                                <span class="hunabi-detail">{{d.huanbi}}<small>%</small></span>
                                                
                                                <i :class="d.class2"></i>
                                            </p>
                                        </div>
                                    </div>       
                                </div>  
                            </el-col>  
                        </el-row>
                </el-carousel-item>
              </el-carousel>
        </div>
        
        <div class="second-line">
            <el-row :gutter="20">
                <el-col :lg="12" :md="24" :sm="24" :xs="24">
                    <div class="sliderCon">
                        <div class="sbg"></div>
                        <div class="slider-inner">
                            <div class="title">
                                <h3>企业信息</h3>
                                <el-container>
                                    <el-aside width="40%" class="hidden-sm-and-down">
                                        <img src="../../assets/ShouYe/pp.jpg" alt="">
                                    </el-aside>
                                    <el-main>
                                        <div class="b-descrip">
                                            <span class="b-name">金风园区智慧楼</span>  位于北京市经济开发区博兴一路8号，总面积63889平方米，其中 1#天诚厂房建筑面积42154平方米，由2层生产
                                        </div>
                                    </el-main>
                                </el-container>    
                            </div>
                        </div>       
                    </div>  
                </el-col>  
                <el-col :lg="12" :md="24" :sm="24" :xs="24">
                    <div class="sliderCon">
                        <div class="sbg"></div>
                        <div class="slider-inner">
                            <div class="title">
                                <h3>24小时功率曲线</h3>
                                <el-container>
                                    <div id="gonglv" style="width:100%;height:100%;"></div>
                                </el-container>      
                            </div>
                        </div>       
                    </div>  
                </el-col>  
            </el-row>   
        </div>
        <div class="three-line">
                <el-row :gutter="20">
                    <el-col :lg="24" :md="24" :sm="24" :xs="24">
                        <div class="sliderCon">
                            <div class="sbg"></div>
                            <div class="slider-inner">
                                <div class="title">
                                    <h3>能耗趋势与对比</h3>
                                    <el-container>
                                       
                                    </el-container>    
                                </div>
                            </div>       
                        </div>  
                    </el-col>  
                    
                </el-row>   
            </div>
    </div>
</template>

<script>
    // import Schart from "vue-schart";
    import bus from "../common/bus";
    import Swiper from "swiper";
    import 'element-ui/lib/theme-chalk/display.css';
    var echarts = require('echarts');
    export default {
        name: "dashboard",
        data() {
            return {
                sliderData:[
                    {
                        title:'今日用水',
                        data:62.86,
                        tongbi:32.12,
                        class1:'icon-tb',
                        huanbi:12.10,
                        class2:'icon-hb'
                    },
                    {
                        title:'今月用水',
                        data:1062.86,
                        tongbi:0.13,
                        class1:'icon-tb',
                        huanbi:0.10,
                        class2:'icon-hb'
                    },
                    {
                        title:'今年用水',
                        data:20562.86,
                        tongbi:0.14,
                        class1:'icon-tb',
                        huanbi:0.10,
                        class2:'icon-hb'
                    }
                ],
                img:'../../assets/ShouYe/pp.jpg',
            };
        },
        components: {
            
        },
        computed: {
            role() {
                // return this.name === "admin" ? "超级管理员" : "普通用户";
            }
        },
      
        methods: {
            SetEchart() {
                // 基于准备好的dom，初始化echarts实例
                // var growRanking = echarts.init(document.getElementById('myChart'));

                var gonglv = document.getElementById('gonglv');
                var gonglvChart = echarts.init(gonglv);
                var one = [224, 220, 335, 188, 350, 230, 354, 261,220,231,241,351,254,123,255,154,365,234,125,421,322,122,352,421];
                var two = [124, 120, 235, 288, 250, 330, 254, 361,320,331,141,351];
                
                // 指定图表的配置项和数据


                var option = {
                    color: ['#1A9BFF', '#00E099', '#38E68D', '#CFDB48', '#66A9C9', '#00BFC7', '#99D683', '#B4C1D7', '#21834B'],
                   
                    legend: {
                        data: ['昨日曲线','今日曲线'],
                        // align: 'left',
                        x: 'center',
                        right: '4%',
                        // icon: 'rect',
                        //itemGap: 13,
                        textStyle: {
                            color: 'rgb(91,227,224)',
                            fontSize: 12
                        }
                    },
                    grid: {
                        left: '3%',
                        right: '1%',
                        bottom: '3%',
                        top: '15%',
                        containLabel: true
                    },
                    tooltip: {
                        trigger: 'axis',
                        axisPointer: {
                            lineStyle: {
                                type: 'shadow',
                                color: '#778AA8'
                            }
                        }
                    },
                    xAxis: [{
                        data: ['0', '1', '2','3','4','5', '6', '7','8','9','10','11','12','13','14','15', '16', '17','18','19','20','21','22','23'],
                        type: 'category',
                        boundaryGap: false,
                        axisLine: {
                            lineStyle: {
                                color: 'rgb(91,227,224)'//x轴坐标颜色
                            }
                        }
                    }],
                    yAxis: [
                        {
                            type: 'value',
                            name: '单位（kw）',
                            axisTick: {
                                show: false
                            },
                            axisLine: {
                                lineStyle: {
                                    color: 'rgb(223,253,255)'
                                }
                            },
                            axisLabel: {
                                margin: 10,
                                textStyle: {
                                    fontSize: 14
                                }
                            },
                            splitLine: {
                                lineStyle: {
                                    color: 'rgb(42,81,125)'
                                }
                            }
                        }
                    ],
                    series: [{
                        name: '昨日曲线',
                        type: 'line',
                        smooth: true,
                        symbolSize: 0,
                        areaStyle: {
                            normal: {
                                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                                    offset: 0,
                                    color: 'rgba(26, 155, 255, 0.9)'
                                }, {
                                    offset: 0.8,
                                    color: 'rgba(26, 155, 255, 0)'
                                }], false),
                                shadowColor: 'rgba(0, 0, 0, 0.1)',
                                shadowBlur: 10
                            }
                        },
                        data: one,
                        },
                        {
                        name: '今日曲线',
                        type: 'line',
                        smooth: true,
                        symbolSize: 0,
                        areaStyle: {
                            normal: {
                                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                                    offset: 0,
                                    color: 'rgba(0, 224, 153, 0.9)'
                                }, {
                                    offset: 0.8,
                                    color: 'rgba(0, 224, 153, 0)'
                                }], false),
                                shadowColor: 'rgba(0, 0, 0, 0.1)',
                                shadowBlur: 10
                            }
                        },
                        data: two,
                        }
                    ]
                }


                // 使用刚指定的配置项和数据显示图表。
                gonglvChart.setOption(option);
                window.onresize = function () {
                    gonglvChart.resize();
                    };
            },
        },
        mounted() {
            this.SetEchart();
        }
    };
</script>
<style>
    .second-line,.three-line{
        margin-bottom:20px;
    }
    .b-descrip{
        color:#DFFDFF;
    }
    .b-name{
        color:#2CF4F2;
    }
    .title{
        width:100%;
        padding:15px;
    }
    img{
        width:100%;
        height:95%;
    }
    .title>h3{
        padding-bottom:27px;
        color:#FEFEFF;
        text-align: left;
        width:100%;
        display: flex;
        font-size:16px;
    }
    .el-container{
        padding-left:30px;
        height:222px;
    }
    /* .title img{
        margin:0 30px;
    } */
    .cbg{
    width: 98%;
    height: 100%;
    position: absolute;
    /* top: 0;
    left: 0; */
    border: 1px solid #2af4ff;
    -webkit-box-shadow: 0px 3px 10px 0px #173050, 0px 3px 30px 0px rgba(42, 244, 255, 0.84) inset;
    box-shadow: 0px 3px 10px 0px #173050, 0px 3px 30px 0px rgba(42, 244, 255, 0.84) inset;
    opacity: 0.5;
    border-radius: 3px;
    z-index: 0;
    }


    
    .el-carousel__container{
        height:100%;
    }
    .Dashboard .swiper-pagination-bullet-active {
        background: #fff;
    }
    .sliderCon{
        position:relative;
    }
    .sbg{
        width: 100%;
        height: 100%;
        position: absolute;
        top: 0;
        left: 0;
        border: 1px solid #2af4ff;
        -webkit-box-shadow: 0px 3px 10px 0px #173050, 0px 3px 30px 0px rgba(42, 244, 255, 0.84) inset;
        box-shadow: 0px 3px 10px 0px #173050, 0px 3px 30px 0px rgba(42, 244, 255, 0.84) inset;
        opacity: 0.5;
        border-radius: 3px;
        z-index: 0;
    }
    .slider-inner{
        width:100%;
        display: flex;
        justify-content: space-around;
        position: relative;
    }
    .el-carousel__indicators{
        bottom:20px;
    }
    .water-icon{
        width:100px;
        height:104px;
        line-height:124px;
        flex-grow:0;
        position:relative;
        flex-shrink:1;
        margin-top:20px;
        margin-left:40px;
        background: url("../../assets/ShouYe/icon_water.png") no-repeat;
    }
    .see-blank{
        position:relative;
        height:100px;
        color:#E8EEEA;
        font-family:'DS-Digital';
        font-size:16px;
        margin-top:33px;
        margin-left:20px;
        flex-grow:1;
    }
    .see-blank small{
        padding-left:5%;
    }
    .see-blank>small{
        color:#2CF4F2;
        font-size: 16px;
        margin-top:15px;
    }
    .led-text{
        color:#2CF4F2;
        display: inline-block;
        font-size:30px;
        margin-top:15px;
    }
    .el-carousel{
        height:100%;
    }
    .icon-tb{
        background: url("../../assets/ShouYe/icon_tb.png") no-repeat;
        width:11px;
        height:14px;
        position:relative;
        display: inline-block;
    }
    .icon-hb{
        background: url("../../assets/ShouYe/icon_hb.png") no-repeat;
        width:11px;
        height:14px;
        position:relative;
        display: inline-block;
        vertical-align: middle;
    }
    .tong-huan-bi{
        color:#E8EEEA;
        font-size: 14px;
        margin-top:40px;
        text-align: left;
        flex-grow:1;
        /* margin-right:10%; */
    }
    .tongbi .tongbi-detail{
        color:#2FA1FF;
        width:50px;
        display: inline-block;
    }
    .tongbi{
        margin-bottom:13px;
    }
    .huanbi .hunabi-detail{
        color:#FE6134;
        width:50px;
        display: inline-block;
    }
</style>
