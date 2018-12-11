<template>
    <div class="RTData Inquire">
        <transition name="el-zoom-in-center">
            <div v-show="leftShow" class="left-branch">
                <div class="tit"><h3>报警分类</h3></div>
                <div class="alarm-type">
                    <ul>
                        <li>全部类型 <span>17</span></li>
                        <li class="f2">安全报警 <span>1</span></li>
                        <li class="f3">配电监控 <span>1</span></li>
                        <li class="f2">环境报警 <span>4</span></li>
                        <li class="f3">温度报警 <span>2</span></li>
                        <li class="f3">湿度报警 <span>2</span></li>
                        <li class="f2">缴费提醒 <span>12</span></li>
                        <li class="f3">预付费用户 <span>8</span></li>
                        <li class="f3">后付费用户 <span>4</span></li>
                    </ul>
                </div>
            </div>
        </transition>
        <div @click="leftShow=!leftShow" :class="{btn:true,shrinkBtn:!leftShow}">报 警 分 类</div>
        <div :class="{main:true,mainShow:leftShow}">
            <div class="filtrate-box">
                <div class="bg"></div>
                <div class="title"><h3>筛选条件</h3>

                </div>
                <!--<div @click="filtrateShow=!filtrateShow"-->
                <!--:class="{'shift-knob-t':filtrateShow,'shift-knob-b':!filtrateShow}"></div>-->
                <el-collapse-transition>
                    <div v-show="filtrateShow" class="filtrate-show">


                        <div class="item-row item-row-btns">
                            <div class="menu-left">
                                <div @click="plclCur=!plclCur" :class="{'btn-plcl':true,cur:plclCur}"></div>
                                <div class="commit">
                                    <span style="color: #FF755E">100</span>条未读，<span style="color: #48D997">234</span>条已处理
                                </div>
                            </div>
                            <div class="menu-right">
                                <div class="right-btn">
                                    <div @click="btnCur=0" :class="{'btn-all':true,cur:btnCur==0}"></div>
                                    <div @click="btnCur=1" :class="{'btn-ycl':true,cur:btnCur==1}"></div>
                                    <div @click="btnCur=2" :class="{'btn-wcl':true,cur:btnCur==2}"></div>
                                </div>
                                <div class="sort-box">
                                    <div class="select-sort">
                                        <span>默认排序</span>
                                        <i class="icon-arrow"></i>
                                    </div>
                                    <div class="pull-down">
                                        <div>默认排序</div>
                                        <div>默认排序</div>
                                        <div>自定义时间段</div>
                                        <div class="custom">
                                            <div class="time-start">
                                                <input type="text" class="input-year">
                                                <span>年</span>
                                                <input type="text" class="input-month">
                                                <span>月</span>
                                                <input type="text" class="input-day">
                                                <span>日</span>
                                            </div>
                                            <div class="to">至</div>
                                            <div class="time-end">
                                                <input type="text" class="input-year">
                                                <span>年</span>
                                                <input type="text" class="input-month">
                                                <span>月</span>
                                                <input type="text" class="input-day">
                                                <span>日</span>
                                            </div>
                                        </div>
                                        <div class="confirm">确定</div>

                                    </div>
                                </div>
                            </div>
                        </div>


                    </div>
                </el-collapse-transition>

            </div>
            <!--对比-->
            <div class="contrast">
                <el-row :gutter="24">
                    <el-col :key="index" v-for="(v,index) in lists" :xl="8" :lg="8" :md="24" :sm="24" :xs="24">
                        <div class="current-period">
                            <div :style="{background:v.color}" class="item-left">
                                <i :class="v.icon"></i>
                            </div>
                            <div class="item-right">
                                <div class="p">
                                    <span>{{ v.title }}</span>
                                    <span class="time">2018-10-26   00：46：00</span>
                                </div>

                                <div class="kwh">
                                    <span class="number">166.56</span>
                                    <span class="unit">kWh</span>
                                </div>
                            </div>
                        </div>
                    </el-col>
                </el-row>
                <el-row :gutter="24">
                    <el-col :key="index" v-for="(v,index) in lists2" :xl="8" :lg="8" :md="24" :sm="24" :xs="24">
                        <div class="current-period">
                            <div :style="{background:v.color}" class="item-left">
                                <i :class="v.icon"></i>
                            </div>
                            <div class="item-right">
                                <div class="p">
                                    <span>{{ v.title }}</span>
                                    <span class="time">2018-10-26   00：46：00</span>
                                </div>
                                <div class="kwh">
                                    <span class="number">166.56</span>
                                    <span class="unit">kWh</span>
                                </div>
                            </div>
                        </div>
                    </el-col>
                </el-row>

            </div>

            <div class="data-box">
                <div class="bg"></div>
                <div class="title"><h3>总功率因数pf</h3>
                </div>
                <div class="my-charts"></div>
            </div>


            <div class="Table">
                <div class="bg"></div>
                <div class="title"><h3>数据列表</h3>
                    <div class="head-right"><i class="icon-pdf"></i><i class="icon-excel"></i></div>
                </div>


                <template-table :data-tit="tableTitle"></template-table>
                <div class="selector">
                    <i class="icon-front"></i>
                    <i class="icon-prev"></i>
                    <div class="page-num">
                        <div class="bg"></div>
                        <input type="text" value="1">
                    </div>

                    <span class="page-all">
                        /共1页
                    </span>
                    <i class="icon-next"></i>
                    <i class="icon-last"></i>
                    <div class="count">
                        <div class="bg"></div>
                        <select>
                            <option>10</option>
                            <option>20</option>
                            <option>50</option>
                            <option>100</option>
                        </select>
                    </div>
                </div>
            </div>

        </div>
    </div>
</template>

<script>
    import TemplateTable from '../views/template-table'

    export default {
        name: "baojingguanli",
        data() {
            return {
                plclCur: false,
                btnCur: 0,
                lists: [
                    {
                        title: '最大负荷',
                        icon: 'item-icon-max',
                        color: '#00C3F4',
                    },
                    {
                        title: '最小负荷',
                        icon: 'item-icon-min',
                        color: '#2CD27D',
                    },
                    {
                        title: '平均负荷',
                        icon: 'item-icon-pjf',
                        color: '#D69B44',
                    },
                ],
                lists2: [
                    {
                        title: '日负荷率',
                        icon: 'item-icon-r',
                        color: '#656EE8',
                    },
                    {
                        title: '最低负荷率',
                        icon: 'item-icon-zdfh',
                        color: '#CFDB48',
                    },
                    {
                        title: '负荷系数',
                        icon: 'item-icon-fhxs',
                        color: '#BE6A3C',
                    }
                ],
                option: '2',
                tabTit: 0,
                radio: 2,
                leftShow: true,
                filtrateShow: true,
                btns: 0,
                no2off: true,
                value6: '',
                days: 2,
                checked5: true,
                checked6: true,
                checked7: true,
                checked8: false,
                checked9: false,
                checked10: false,
                tableTitle: {
                    title: '【 2018-09-18 00:00:00 至 2018-09-18 20:00:00 能耗数据 】',
                    titArr: [
                        {
                            prop: "id",
                            label: "日期",
                            sortable: false
                        },
                        {
                            prop: "dianliuIa",
                            label: "电流Ia",
                            sortable: false
                        },
                        {
                            prop: "dianliuIb",
                            label: "电流Ib",
                            sortable: false
                        },
                        {
                            prop: "dianliuIc",
                            label: "电流Ic",
                            sortable: false
                        },
                        {
                            prop: "zhengDianNeng",
                            label: "当前正向有功总电能",
                            sortable: false
                        },
                        {
                            prop: "cuUan",
                            label: "粗电压Uan",
                            sortable: false
                        },
                        {
                            prop: "cuUbn",
                            label: "粗电压Ubn",
                            sortable: false
                        },
                        {
                            prop: "cuUcn",
                            label: "粗电压Ucn",
                            sortable: false
                        },
                        {
                            prop: "sum",
                            label: "总有功功率W",
                            sortable: false
                        },
                    ]
                },

            }
        },
        components: {
            TemplateTable
        },
        mounted() {

        }

    }
</script>

<style>
    .ztree li span.button.ico_open, .ztree li span.button.ico_close {
        line-height: 0;
        margin: 0;
        width: 16px;
        height: 16px;
        display: inline-block;
        vertical-align: middle;
        border: 0 none;
        cursor: pointer;
        outline: none;
        background-color: transparent;
        background-repeat: no-repeat;
        background-attachment: scroll;
        background-image: url("../../assets/PeiDianJianCe/icon_wjb(1).png");
        background-position: 0 0;
        /**background-image: url(./img/zTreeStandard.gif);*/
    }

    /*icon_wj*/
    .ztree li span.button.ico_docu {
        line-height: 0;
        margin: 0;
        width: 16px;
        height: 16px;
        display: inline-block;
        vertical-align: middle;
        border: 0 none;
        cursor: pointer;
        outline: none;
        background-color: transparent;
        background-repeat: no-repeat;
        background-attachment: scroll;
        background-image: url("../../assets/PeiDianJianCe/icon_wj.png");
        background-position: 0 0;
        /**background-image: url(./img/zTreeStandard.gif);*/
    }

    .ztree li span.node_name {
        margin-left: 4px;
        font-size: 12px;
        font-family: HiraginoSansGB-W3;
        font-weight: normal;
        color: rgba(254, 254, 254, 1);
    }

    .ztree li span.button.chk.checkbox_false_full, .ztree li span.button.chk.checkbox_false_full_focus {
        width: 16px;
        height: 16px;
        background: url("../../assets/PeiDianJianCe/icon_wxz.png") no-repeat;
        background-position: 0 0;
    }

    .ztree li span.button.chk.checkbox_false_part, .ztree li span.button.chk.checkbox_false_part_focus, .ztree li span.button.chk.checkbox_true_full, .ztree li span.button.chk.checkbox_true_full_focus, .ztree li span.button.chk.checkbox_true_part, .ztree li span.button.chk.checkbox_true_part_focus {
        width: 16px;
        height: 16px;
        background: url("../../assets/PeiDianJianCe/icon_xz.png") no-repeat;
        background-position: 0 0;
    }

    .ztree li span.button.roots_open, .ztree li span.button.bottom_open, .ztree li span.button.center_open {

        background: url("../../assets/PeiDianJianCe/icon_zk.png") no-repeat;
        background-position: 0 0;
    }

    .ztree li span.button.bottom_close, .ztree li span.button.center_close, .ztree li span.button.roots_close {
        background: url("../../assets/PeiDianJianCe/icon_dj.png") no-repeat;
        background-position: 0 0;
    }

    .ztree li span.button.chk.radio_true_full, .ztree li span.button.chk.radio_true_full_focus {
        background-position: 0 0;
    }

    .ztree li span.button.radio_true_full, .ztree li span.button.radio_true_full_focus, .ztree li span.button.chk.radio_true_part, .ztree li span.button.chk.radio_true_part_focus {
        width: 16px;
        height: 16px;
        background: url("../../assets/NengHaoChaXun/icon_xz.png") no-repeat;
        background-position: 0 0;
    }

    .ztree li span.button.radio_false_full, .ztree li span.button.radio_false_full_focus, .ztree li span.button.radio_false_part, .ztree li span.button.radio_false_part_focus {
        width: 14px;
        height: 14px;
        background: url("../../assets/NengHaoChaXun/椭圆 884.png") no-repeat;
        background-position: 0 0;
    }

    .ztree li span.button.chk.radio_false_full, .ztree li span.button.chk.radio_false_full_focus, .ztree li span.button.radio_false_part, .ztree li span.button.radio_false_part_focus {
        background-position: 0 0;
        -webkit-background-size: 100% 100%;
        background-size: 100% 100%;
    }

    .ztree li span.button.chk.radio_false_part, .ztree li span.button.chk.radio_false_part_focus {
        background-position: 0 0;
    }


</style>


<style lang="scss" scoped>
    @media screen and (max-width: 1500px) {

    }

    .RTData {
        width: 100%;
        height: 100%;

        position: relative;
        display: flex;
        flex-wrap: nowrap;
        justify-content: space-between;

        .left-branch {
            width: 245px;
            height: 100%;
            min-height: 500px;
            box-sizing: border-box;
            /*margin-bottom: 40px;*/
            /*float: left;*/
            /*margin-right: 24px;*/
            position: relative;
            /*border: 1px solid red;*/

            background: #0A3E6E;
            border: 1px solid #199AB7;
            /*box-shadow:0px 0px 9px 0px rgba(1,16,31,1), 0px 0px 30px 0px rgba(42,244,255,0.84);*/
            /*opacity:0.51;*/
            box-shadow: 0px 3px 9px 0px #01101f, 0px 3px 30px 2px #1A8EA0 inset;
            border-radius: 3px;
            padding: 14px 13px;
            .alarm-type {
                width: 100%;
                margin-top: 30px;
                ul {
                    list-style: none;
                    li {
                        font-size: 12px;
                        font-family: HiraginoSansGB-W3;
                        font-weight: normal;
                        color: rgba(254, 254, 254, 1);
                        margin-bottom: 17px;
                        display: flex;
                        justify-content: space-between;
                        &.f2 {
                            position: relative;
                            margin-left: 15px;
                            span {
                                background-color: #F39800;
                            }
                        }
                        &.f2::before {
                            content: '';
                            position: absolute;
                            top: 5px;
                            left: -15px;
                            width: 5px;
                            height: 5px;
                            border: 1px solid rgba(72, 206, 230, 1);
                            border-radius: 50%;
                        }
                        &.f3 {
                            margin-left: 27px;
                            span {
                                background-color: #00A0E9;
                            }
                        }
                        span {
                            font-size: 10px;
                            font-family: HiraginoSansGB-W6;
                            font-weight: normal;
                            color: rgba(255, 255, 255, 1);
                            padding: 0 7px;
                            border-radius: 8px;
                            background-color: #FC5135;
                        }
                    }
                }
            }

            .empty {
                width: 223px;
                height: 28px;
                border: 1px solid rgba(45, 243, 255, 1);
                border-radius: 14px;
                background-color: #0A3E6E;
                margin-top: 20px;
                padding: 0 14px;
                box-sizing: border-box;
                position: relative;
                &:before {
                    content: '';

                }
            }
            .ztree {
                margin-top: 20px;
            }

            .tit {
                h3 {
                    font-size: 16px;
                    font-family: HiraginoSansGB-W3;
                    font-weight: 600;
                    color: rgba(254, 254, 255, 1);
                }

            }
            .butt {
                width: 100%;
                position: absolute;
                bottom: 0;
                left: 0;
                box-sizing: border-box;
                padding: 9px 12px;
                border-top: 1px solid #1A9BB8;
                ul {
                    list-style: none;
                    margin-top: 5px;
                    li {
                        line-height: 30px;
                        span {
                            font-size: 12px;
                            font-family: HiraginoSansGB-W3;
                            font-weight: normal;
                            color: rgba(254, 254, 254, 1);
                            margin-left: 12px;
                        }
                    }
                }
            }
            .icon-not {
                width: 12px;
                height: 12px;
                display: inline-block;
                background: url("../../assets/PeiDianJianCe/组 97.png") no-repeat;
            }
            .icon-yes {
                width: 12px;
                height: 12px;
                display: inline-block;
                background: url("../../assets/PeiDianJianCe/椭圆 884.png") no-repeat;
            }

        }
        .btn {
            cursor: pointer;
            width: 24px;
            height: 90px;
            text-align: center;
            /*line-height: 9px;*/
            box-sizing: border-box;
            padding: 12px 0;

            /*background:rgba(32,155,185,1);*/
            /*border:1px solid rgba(0,229,255,1);*/
            background: url("../../assets/PeiDianJianCe/矩形-943.png") no-repeat;
            font-size: 12px;
            font-family: HiraginoSansGB-W3;
            font-weight: bold;
            color: rgba(254, 254, 255, 1);
        }
        .shrinkBtn {
            position: absolute;
            left: -20px;
            top: 0;
        }

        .main {
            width: 100%;
            height: 100%;
            min-height: 500px;
            overflow-y: auto;
            overflow-x: hidden;

            position: relative;
            margin-left: 4px;
            .contrast {
                width: 100%;
                /*display: flex;*/
                /*flex-wrap: nowrap;*/
                /*justify-content: space-between;*/
                margin-top: 24px;
                .el-row {
                    margin-bottom: 24px;

                    &:last-child {
                        margin-bottom: 0;
                    }
                    @media screen and (max-width: 1200px) {
                        margin-bottom: 0;
                    }
                }

                /*@media screen and (min-width: 1500px) {*/
                /*&:not(:first-child) {*/
                /*margin-left: 25px;*/
                /*}*/
                /*}*/
                /*@media screen and (max-width: 1500px) {*/
                /*margin-left: 0;*/
                /*margin-top: 20px;*/
                /*}*/
                /*width: 100%;*/

                /*display: flex;*/
                /*flex-direction: column;*/
                .item-icon-hz {
                    /*line-height: 90px;*/
                    width: 43px;
                    height: 43px;
                    display: inline-block;
                    background: url("../../assets/PeiDianJianCe/icon_hz2.png") no-repeat;
                }
                .item-icon-pjf {
                    /*line-height: 90px;*/
                    width: 40px;
                    height: 37px;
                    display: inline-block;
                    background: url("../../assets/PeiDianJianCe/icon_pjf.png") no-repeat;
                }
                .item-icon-max {
                    /*line-height: 90px;*/
                    width: 59px;
                    height: 21px;
                    display: inline-block;
                    background: url("../../assets/PeiDianJianCe/max.png") no-repeat;
                }
                .item-icon-min {
                    /*line-height: 90px;*/
                    width: 60px;
                    height: 24px;
                    display: inline-block;
                    background: url("../../assets/PeiDianJianCe/mIN.png") no-repeat;
                }
                .item-icon-tb {
                    /*line-height: 90px;*/
                    width: 41px;
                    height: 34px;
                    display: inline-block;
                    background: url("../../assets/PeiDianJianCe/icon_tb.png") no-repeat;
                }
                .item-icon-r {
                    /*line-height: 90px;*/
                    width: 32px;
                    height: 41px;
                    display: inline-block;
                    background: url("../../assets/PeiDianJianCe/icon_r.png") no-repeat;
                }
                .item-icon-zdfh {
                    /*line-height: 90px;*/
                    width: 49px;
                    height: 41px;
                    display: inline-block;
                    background: url("../../assets/PeiDianJianCe/icon_zdfh.png") no-repeat;
                }
                .item-icon-fhxs {
                    /*line-height: 90px;*/
                    width: 48px;
                    height: 41px;
                    display: inline-block;
                    background: url("../../assets/PeiDianJianCe/icon_fhxs.png") no-repeat;
                }
                .current-period {
                    /*width: calc(100% - 25px);*/
                    width: 100%;
                    height: 90px;
                    box-sizing: border-box;
                    /*padding: 20px 0;*/

                    border: 1px solid rgba(42, 244, 255, 1);
                    box-shadow: 0px 0px 10px 0px rgba(23, 48, 80, 1), 0px 0px 30px 0px rgba(42, 244, 255, 0.84) inset;
                    /*opacity:0.5;*/
                    border-radius: 3px;
                    @media screen and (max-width: 1200px) {
                        margin-top: 24px;
                    }

                    .item-left {
                        width: 90px;
                        height: 90px;
                        box-sizing: border-box;
                        /*padding: ;*/
                        float: left;
                        display: flex;
                        align-items: center;
                        justify-content: center;
                        text-align: center;
                        background-color: #01A8F2;
                        border-radius: 3px 3px 0px 0px;
                        margin-top: -1px;
                        margin-left: -1px;

                    }
                    .item-right {
                        box-sizing: border-box;
                        /*padding-left: 90px;*/
                        /*box-sizing: border-box;*/
                        /*padding: 20px 0;*/
                        padding: 20px 20px 20px 110px;
                        .p {
                            font-size: 14px;
                            font-family: HiraginoSansGB-W3;
                            font-weight: normal;
                            color: rgba(223, 253, 255, 1);
                            display: flex;
                            justify-content: space-between;
                        }
                        .kwh {
                            margin-top: 6px;
                            display: flex;
                            justify-content: space-between;
                        }
                        .number {
                            font-size: 18px;
                            font-family: DigitaldreamFat;
                            font-weight: 400;
                            color: rgba(44, 244, 242, 1);
                        }
                        .unit {
                            font-size: 14px;
                            font-family: HiraginoSansGB-W3;
                            font-weight: normal;
                            color: rgba(223, 253, 255, 1);
                        }

                    }
                }
                .before {
                    width: 100%;
                    height: 90px;
                    box-sizing: border-box;
                    margin-top: 25px;
                    /*padding: 20px 0;*/

                    border: 1px solid rgba(42, 244, 255, 1);
                    box-shadow: 0px 0px 10px 0px rgba(23, 48, 80, 1), 0px 0px 30px 0px rgba(42, 244, 255, 0.84) inset;
                    /*opacity:0.5;*/
                    border-radius: 3px;
                    .item-left {
                        width: 90px;
                        height: 90px;
                        box-sizing: border-box;
                        /*padding: ;*/
                        float: left;
                        display: flex;
                        align-items: center;
                        justify-content: center;
                        text-align: center;
                        background-color: #5361DB;
                        border-radius: 3px 3px 0px 0px;
                        margin-top: -1px;
                        margin-left: -1px;
                        .item-icon-hz {
                            /*line-height: 90px;*/
                            width: 43px;
                            height: 43px;
                            display: inline-block;
                            background: url("../../assets/PeiDianJianCe/icon_hz2.png") no-repeat;
                        }
                    }
                    .item-right {
                        box-sizing: border-box;
                        /*padding-left: 90px;*/
                        /*box-sizing: border-box;*/
                        /*padding: 20px 0;*/
                        padding: 20px 20px 20px 110px;
                        p {
                            font-size: 14px;
                            font-family: HiraginoSansGB-W3;
                            font-weight: normal;
                            color: rgba(223, 253, 255, 1);
                        }
                        .kwh {
                            margin-top: 6px;
                            display: flex;
                            justify-content: space-between;
                        }
                        .number {
                            font-size: 18px;
                            font-family: DigitaldreamFat;
                            font-weight: 400;
                            color: rgba(44, 244, 242, 1);
                        }
                        .unit {
                            font-size: 14px;
                            font-family: HiraginoSansGB-W3;
                            font-weight: normal;
                            color: rgba(223, 253, 255, 1);
                        }

                    }
                }

            }

            .bg {
                width: 100%;
                height: 100%;
                position: absolute;
                top: 0;
                left: 0;
                border: 1px solid rgba(42, 244, 255, 1);
                box-shadow: 0px 3px 10px 0px rgba(23, 48, 80, 1), 0px 3px 30px 0px rgba(42, 244, 255, 0.84) inset;
                opacity: 0.5;
                border-radius: 3px;
                z-index: 0;
            }
            .filtrate-box {
                width: 100%;
                /*height: 292px;*/
                position: relative;
                box-sizing: border-box;
                padding: 15px 20px 9px 20px;
                background-color: #0B3F6F;
                .interval {
                    font-size: 14px;
                    font-family: HiraginoSansGB-W3;
                    font-weight: bold;
                    color: rgba(45, 243, 255, 1);
                }
                .fl {
                    float: left;
                }
                .icon-time {
                    width: 14px;
                    height: 15px;
                    display: inline-block;
                    background: url("../../assets/PeiDianJianCe/icon_sj.png") no-repeat;
                    margin-right: 5px;
                }
                .count {
                    width: 80px;
                    height: 28px;
                    margin-left: 12px;
                    position: relative;
                    border: 1px solid #29D1E5;
                    select {
                        border: 0px;
                        outline: none;
                        cursor: pointer;
                        position: relative;
                        z-index: 5;
                        width: 100%;
                        height: 100%;
                        background: rgba(26, 96, 134, 0);
                        font-size: 12px;
                        font-family: HiraginoSansGB-W3;
                        font-weight: bold;
                        color: rgba(219, 253, 255, 1);
                        option {
                            background-color: #0B3F6F;
                        }
                    }
                }
                .shift-knob-t {
                    width: 61px;
                    height: 20px;
                    background: url("../../assets/NengHaoChaXun/bt_zk.png") no-repeat;
                    position: absolute;
                    left: 50%;
                    bottom: -20px;
                    margin-left: -30px;
                }
                .shift-knob-b {
                    width: 61px;
                    height: 20px;
                    background: url("../../assets/NengHaoChaXun/bt_ss.png") no-repeat;
                    position: absolute;
                    left: 50%;
                    bottom: -20px;
                    margin-left: -30px;
                }
                .title {
                    /*margin-bottom: 15px;*/
                    display: flex;
                    justify-content: space-between;
                    position: relative;
                    h3 {
                        font-size: 16px;
                        font-family: HiraginoSansGB-W3;
                        font-weight: bold;
                        color: rgba(254, 254, 255, 1);
                    }
                    .updataTime {
                        display: flex;
                        justify-content: space-between;
                        align-items: center;
                        span {
                            font-size: 12px;
                            font-family: HiraginoSansGB-W3;
                            font-weight: bold;
                            color: rgba(183, 208, 210, 1);
                            margin-right: 19px;
                        }
                    }
                    .off {
                        cursor: pointer;
                        width: 40px;
                        height: 24px;
                        background: url("../../assets/PeiDianJianCe/btn_kq.png") no-repeat;
                    }
                    .no {
                        cursor: pointer;
                        width: 40px;
                        height: 24px;
                        background: url("../../assets/PeiDianJianCe/btn_gb.png") no-repeat;
                    }
                }

                .filtrate-show {
                    width: 100%;
                    display: flex;
                    position: relative;
                    flex-direction: column;
                    z-index: 5;
                    margin-top: 15px;
                    /*margin-bottom: 60px;*/
                    .item2 {
                        display: flex;
                        flex-wrap: nowrap;
                        justify-content: flex-start;

                        .more-box {
                            flex: 1;
                            display: flex;
                            flex-wrap: nowrap;
                            justify-content: flex-start;
                            align-items: center;
                        }
                    }
                    .item-row-btns {
                        display: flex;
                        justify-content: space-between;

                        .menu-left {
                            display: flex;
                            align-items: center;
                            .btn-plcl {
                                width: 111px;
                                height: 41px;
                                background: url("../../assets/PeiDianJianCe/btn_plcl-xz.png") no-repeat;
                                &.cur {
                                    background: url("../../assets/PeiDianJianCe/btn_plcl-xz1.png") no-repeat;
                                }
                            }
                            .commit {
                                font-size: 14px;
                                font-family: HiraginoSansGB-W3;
                                font-weight: normal;
                                color: #E8E8E8;
                            }
                        }
                        .menu-right {
                            display: flex;
                            flex-direction: row;
                            align-items: center;
                            .sort-box {
                                position: relative;
                                .pull-down{
                                    position: absolute;
                                    top: 28px;
                                    left: 0;
                                    width: 170px;
                                    height: 184px;
                                    background:rgba(0,17,33,.5);
                                    /*box-shadow:0px 3px 8px 1px rgba(2,28,60,0.43);*/
                                }
                            }
                            /*pull-down*/
                            .select-sort {
                                width: 170px;
                                height: 28px;
                                border: 1px solid rgba(45, 243, 255, 1);
                                border-radius: 2px;
                                box-sizing: border-box;
                                padding: 3px 12px;
                                display: flex;
                                justify-content: space-between;
                                align-items: center;
                                span {
                                    font-size: 14px;
                                    font-family: HiraginoSansGB-W3;
                                    font-weight: bold;
                                    color: rgba(190, 205, 222, 1);
                                }

                                .icon-arrow {
                                    width: 12px;
                                    height: 7px;
                                    display: inline-block;
                                    background: url("../../assets/PeiDianJianCe/形状 1054 拷贝 2.png") no-repeat;
                                    /*-webkit-background-size: ;*/
                                    background-size: 100% 100%;
                                }
                            }
                            .right-btn {
                                display: flex;
                                flex-direction: row;
                                & > div {
                                    width: 91px;
                                    height: 41px;
                                }
                                .btn-all {
                                    background: url("../../assets/PeiDianJianCe/btn_qb.png") no-repeat;
                                    &.cur {
                                        background: url("../../assets/PeiDianJianCe/btn_qb-xz.png") no-repeat;
                                    }
                                }
                                .btn-ycl {
                                    background: url("../../assets/PeiDianJianCe/btn_wcl.png") no-repeat;
                                    &.cur {
                                        background: url("../../assets/PeiDianJianCe/btn_wcl -xz.png") no-repeat;
                                    }
                                }
                                .btn-wcl {
                                    background: url("../../assets/PeiDianJianCe/btn_ycl.png") no-repeat;
                                    &.cur {
                                        background: url("../../assets/PeiDianJianCe/btn_ycl-xz.png") no-repeat;
                                    }
                                }

                            }
                        }
                    }

                    .item-row {
                        height: 60px;
                        width: 100%;
                        background-color: #174B7B;
                        display: flex;
                        align-items: center;
                        border-bottom: 2px solid #0B3F6F;
                        box-sizing: border-box;
                        padding: 0 10px;
                        .icon-lx {
                            display: inline-block;
                            width: 15px;
                            height: 11px;
                            background: url("../../assets/NengHaoChaXun/icon _fxff.png") no-repeat;
                        }
                        .icon-sj {
                            width: 14px;
                            height: 15px;
                            display: inline-block;
                            background: url("../../assets/PeiDianJianCe/icon_sj.png") no-repeat;
                            margin-right: 5px;
                        }
                        .icon-wd {
                            display: inline-block;
                            width: 16px;
                            height: 15px;
                            background: url("../../assets/NengHaoChaXun/icon_wd.png") no-repeat;
                        }
                        .checkbox-tit {
                            font-size: 14px;
                            font-family: HiraginoSansGB-W3;
                            font-weight: bold;
                            color: rgba(45, 243, 255, 1);
                            margin-left: 4px;
                            margin-right: 20px;
                        }
                        .item-input {
                            /*margin-right: 1rem;*/
                            @media screen and (min-width: 1200px) {
                                /*margin-left: 0;*/
                                /*margin-top: 15px;*/
                                margin-right: 70px;
                            }
                            span {
                                font-size: 14px;
                                font-family: HiraginoSansGB-W3;
                                font-weight: bold;
                                color: rgba(223, 253, 255, 1);
                            }
                            input {
                                background-color: #174B7B;
                                width: 200px;
                                height: 28px;
                                border: 1px solid rgba(45, 243, 255, 1);
                                border-radius: 2px;
                                box-sizing: border-box;
                                padding: 0 13px;
                            }
                        }
                        .select {
                            /*width: 220px;*/
                            margin-left: 7px;
                        }
                        .ml92 {
                            /*margin-left: 92px;*/
                        }
                        .no-off {
                            /*margin-left: 92px;*/
                            cursor: pointer;
                            .icon-left {
                                display: inline-block;
                                width: 12px;
                                height: 12px;
                                background: url("../../assets/NengHaoChaXun/icon_ss.png") no-repeat;
                            }
                            .icon-right {
                                display: inline-block;
                                width: 12px;
                                height: 12px;
                                background: url("../../assets/NengHaoChaXun/icon_gd.png") no-repeat;
                            }
                            span {
                                font-size: 12px;
                                font-family: HiraginoSansGB-W6;
                                font-weight: bold;
                                position: relative;
                                top: -1px;
                                color: rgba(45, 243, 255, 1);
                            }
                        }
                        .date-select {
                            font-size: 14px;
                            font-family: HiraginoSansGB-W3;
                            font-weight: bold;
                            color: rgba(45, 243, 255, 1);
                        }
                        .days-box {
                            display: flex;
                            flex-direction: row;
                            align-items: center;
                        }
                        .days-btn {
                            width: 288px;
                            height: 28px;
                            border: 1px solid rgba(45, 243, 255, 1);
                            opacity: 0.8;
                            margin-left: 5px;
                            border-radius: 2px;
                            display: flex;
                            span {
                                flex: 1;
                                font-size: 12px;
                                font-family: HiraginoSansGB-W3;
                                font-weight: bold;
                                color: rgba(219, 253, 255, 1);
                                text-align: center;
                                line-height: 28px;
                                cursor: pointer;
                            }
                            .cur {
                                background: linear-gradient(180deg, rgba(6, 88, 110, 1), rgba(27, 138, 168, 1));
                                border: 1px solid rgba(153, 236, 241, 1);
                                box-shadow: 0px 1px 1px 0px rgba(12, 28, 79, 0.2);
                                border-radius: 2px;
                                color: #2DF3FF;
                            }
                        }

                    }
                    .item-row-br {
                        @media screen and (max-width: 1200px) {
                            height: auto;
                            justify-content: flex-start;
                            flex-direction: column;
                            align-items: flex-start
                        }
                    }
                    .item-row-2 {
                        height: auto;
                        width: 100%;
                        padding: 13px 10px;
                        background-color: #174B7B;
                        display: block;

                        border-bottom: 2px solid #0B3F6F;
                        box-sizing: border-box;
                        /*padding: 0 10px;*/
                    }
                    .btns-box {
                        width: 100%;
                        display: flex;
                        justify-content: flex-end;
                        /*margin-top: 17px;*/
                        .btn-item {
                            width: 81px;
                            height: 41px;
                            cursor: pointer;
                            margin-right: 20px;
                            text-align: center;
                            line-height: 41px;
                            font-size: 14px;
                            font-family: HiraginoSansGB-W6;
                            font-weight: normal;
                            color: rgba(97, 213, 255, 1);
                            background: url("../../assets/NengHaoChaXun/bt_wxz.png") no-repeat;
                            -webkit-background-size: 100% 100%;
                            background-size: 100% 100%;
                        }
                        .cur {
                            background: url("../../assets/NengHaoChaXun/bt_xz.png") no-repeat;
                            -webkit-background-size: 100% 100%;
                            background-size: 100% 100%;
                        }
                    }
                }
            }
            .data-box {
                width: 100%;
                position: relative;
                height: 436px;
                margin-top: 24px;
                box-sizing: border-box;
                padding: 15px 20px;
                .title {
                    display: flex;
                    justify-content: space-between;
                    position: relative;
                    z-index: 5;
                    /*margin-bottom: 15px;*/
                    h3 {
                        font-size: 16px;
                        font-family: HiraginoSansGB-W3;
                        font-weight: bold;
                        color: rgba(254, 254, 255, 1);
                    }
                    .icon-pdf {
                        display: inline-block;
                        width: 21px;
                        height: 21px;
                        background: url("../../assets/NengHaoChaXun/pdf.png") no-repeat;
                        margin-right: 20px;
                    }
                    .icon-excel {
                        display: inline-block;
                        width: 21px;
                        height: 21px;
                        background: url("../../assets/NengHaoChaXun/excel.png") no-repeat;
                    }
                }
                .my-charts {
                    margin-top: 13px;
                    width: 100%;
                    height: 100%;
                }
                .selector {
                    position: relative;
                    z-index: 5;
                    display: flex;
                    justify-content: flex-end;
                    margin-top: 20px;
                    align-items: center;

                    .icon-front {
                        width: 10px;
                        height: 14px;
                        display: inline-block;
                        background: url("../../assets/NengHaoChaXun/icon_zz.png") no-repeat;
                    }
                    .icon-prev {
                        width: 8px;
                        height: 14px;
                        display: inline-block;
                        transform: rotate(180deg);
                        margin-left: 10px;
                        background: url("../../assets/NengHaoChaXun/箭头2.png") no-repeat;
                    }
                    .icon-next {
                        width: 8px;
                        height: 14px;
                        display: inline-block;
                        margin-left: 20px;
                        background: url("../../assets/NengHaoChaXun/箭头2.png") no-repeat;
                    }
                    .icon-last {
                        margin-left: 10px;
                        width: 10px;
                        height: 14px;
                        display: inline-block;
                        background: url("../../assets/NengHaoChaXun/icon_yy.png") no-repeat;
                    }
                    .page-num {

                        width: 38px;
                        height: 26px;
                        margin-left: 20px;
                        position: relative;
                        input {
                            position: relative;
                            z-index: 5;
                            width: 100%;
                            height: 100%;
                            background: rgba(26, 96, 134, 0);
                            border: 0px;
                            outline: none;
                            cursor: pointer;
                            font-size: 12px;
                            font-family: HiraginoSansGB-W3;
                            font-weight: bold;
                            color: rgba(45, 243, 255, 1);
                            text-align: center;
                        }
                    }
                    .page-all {
                        font-size: 12px;
                        font-family: HiraginoSansGB-W3;
                        font-weight: bold;
                        color: rgba(45, 243, 255, 1);
                        margin-left: 10px;
                    }
                    .count {
                        width: 48px;
                        height: 26px;
                        margin-left: 22px;
                        position: relative;
                        select {
                            border: 0px;
                            outline: none;
                            cursor: pointer;
                            position: relative;
                            z-index: 5;
                            width: 100%;
                            height: 100%;
                            background: rgba(26, 96, 134, 0);
                            font-size: 12px;
                            font-family: HiraginoSansGB-W3;
                            font-weight: bold;
                            color: rgba(45, 243, 255, 1);
                            option {
                                background-color: #0B3F6F;
                            }
                        }
                    }
                }
            }
            .Table {
                width: 100%;
                position: relative;
                box-sizing: border-box;
                padding: 23px 20px;
                margin-top: 25px;
                margin-bottom: 25px;
                .title {
                    display: flex;
                    justify-content: space-between;
                    position: relative;
                    z-index: 5;
                    /*margin-bottom: 15px;*/
                    h3 {
                        font-size: 16px;
                        font-family: HiraginoSansGB-W3;
                        font-weight: bold;
                        color: rgba(254, 254, 255, 1);
                    }
                    .icon-pdf {
                        display: inline-block;
                        width: 21px;
                        height: 21px;
                        background: url("../../assets/NengHaoChaXun/pdf.png") no-repeat;
                        margin-right: 20px;
                    }
                    .icon-excel {
                        display: inline-block;
                        width: 21px;
                        height: 21px;
                        background: url("../../assets/NengHaoChaXun/excel.png") no-repeat;
                    }
                }
                .table-box {
                    position: relative;
                    z-index: 5;
                    border: 1px solid #15759A;
                    /*padding-bottom: 60px;*/
                    .table-tit {
                        padding: 20px;
                        width: 100%;
                        /*letter-spacing:2px;*/
                        font-size: 14px;
                        font-family: HiraginoSansGB-W3;
                        font-weight: normal;
                        color: rgba(95, 251, 248, 1);
                        text-align: center;
                    }

                }
                .selector {
                    position: relative;
                    z-index: 5;
                    display: flex;
                    justify-content: flex-end;
                    margin-top: 20px;
                    align-items: center;

                    .icon-front {
                        width: 10px;
                        height: 14px;
                        display: inline-block;
                        background: url("../../assets/NengHaoChaXun/icon_zz.png") no-repeat;
                    }
                    .icon-prev {
                        width: 8px;
                        height: 14px;
                        display: inline-block;
                        transform: rotate(180deg);
                        margin-left: 10px;
                        background: url("../../assets/NengHaoChaXun/箭头2.png") no-repeat;
                    }
                    .icon-next {
                        width: 8px;
                        height: 14px;
                        display: inline-block;
                        margin-left: 20px;
                        background: url("../../assets/NengHaoChaXun/箭头2.png") no-repeat;
                    }
                    .icon-last {
                        margin-left: 10px;
                        width: 10px;
                        height: 14px;
                        display: inline-block;
                        background: url("../../assets/NengHaoChaXun/icon_yy.png") no-repeat;
                    }
                    .page-num {

                        width: 38px;
                        height: 26px;
                        margin-left: 20px;
                        position: relative;
                        input {
                            position: relative;
                            z-index: 5;
                            width: 100%;
                            height: 100%;
                            background: rgba(26, 96, 134, 0);
                            border: 0px;
                            outline: none;
                            cursor: pointer;
                            font-size: 12px;
                            font-family: HiraginoSansGB-W3;
                            font-weight: bold;
                            color: rgba(45, 243, 255, 1);
                            text-align: center;
                        }
                    }
                    .page-all {
                        font-size: 12px;
                        font-family: HiraginoSansGB-W3;
                        font-weight: bold;
                        color: rgba(45, 243, 255, 1);
                        margin-left: 10px;
                    }
                    .count {
                        width: 48px;
                        height: 26px;
                        margin-left: 22px;
                        position: relative;
                        select {
                            border: 0px;
                            outline: none;
                            cursor: pointer;
                            position: relative;
                            z-index: 5;
                            width: 100%;
                            height: 100%;
                            background: rgba(26, 96, 134, 0);
                            font-size: 12px;
                            font-family: HiraginoSansGB-W3;
                            font-weight: bold;
                            color: rgba(45, 243, 255, 1);
                            option {
                                background-color: #0B3F6F;
                            }
                        }
                    }
                }
            }

        }
        .mainShow {
            width: calc(100% - 273px);
        }
    }
</style>
