<template>
    <div class="Inquire">
        <div class="filtrate-box">
            <div class="bg"></div>
            <div class="title"><h3>筛选条件</h3></div>
            <div @click="filtrateShow=!filtrateShow"
                 :class="{'shift-knob-t':filtrateShow,'shift-knob-b':!filtrateShow}"></div>
            <el-collapse-transition>
                <div v-show="filtrateShow" class="filtrate-show">
                    <div class="item-row">
                        <el-radio class="choice" v-model="radio" label="1">电</el-radio>
                        <el-radio class="choice" v-model="radio" label="2">水</el-radio>
                        <el-radio class="choice" v-model="radio" label="3">冷热</el-radio>
                        <el-radio class="choice" v-model="radio" label="4">压缩空气</el-radio>
                    </div>
                    <div class="item-row item2">
                        <div class="more-box">
                            <el-checkbox v-model="checked1">支路:</el-checkbox>
                            <el-select class="select" v-model="select1" placeholder="请选择支路">
                                <el-option
                                        v-for="item in options"
                                        :key="item.value"
                                        :label="item.label"
                                        :value="item.value">
                                </el-option>
                            </el-select>
                        </div>
                        <div class="more-box">
                            <el-checkbox class="ml92" v-model="checked2">分项:</el-checkbox>
                            <el-select class="select" v-model="select2" placeholder="请选择分项">
                                <el-option
                                        v-for="item in options"
                                        :key="item.value"
                                        :label="item.label"
                                        :value="item.value">
                                </el-option>
                            </el-select>
                        </div>
                        <div v-show="sw" class="item-show more-box">
                            <el-checkbox class="ml92" v-model="checked3">部门:</el-checkbox>
                            <el-select class="select" v-model="select3" placeholder="请选择部门">
                                <el-option
                                        v-for="item in options"
                                        :key="item.value"
                                        :label="item.label"
                                        :value="item.value">
                                </el-option>
                            </el-select>
                        </div>
                        <div v-show="sw" class="item-show more-box">
                            <el-checkbox class="ml92" v-model="checked4">位置:</el-checkbox>
                            <el-select class="select" v-model="select4" placeholder="请选择位置">
                                <el-option
                                        v-for="item in options"
                                        :key="item.value"
                                        :label="item.label"
                                        :value="item.value">
                                </el-option>
                            </el-select>
                        </div>


                        <div @click="sw=!sw" class="no-off more-box">
                            <i :class="{'icon-left':sw,'icon-right':!sw}"></i>
                            <span v-show="sw">收缩</span>
                            <span v-show="!sw">更多</span>
                        </div>
                    </div>
                    <div class="item-row">
                        <span class="date-select">时间选择</span>
                        <el-date-picker
                                v-model="value6"
                                type="daterange"
                                range-separator="—"
                                start-placeholder="开始日期"
                                end-placeholder="结束日期">
                        </el-date-picker>

                        <div class="days-box">
                        <span class="days-tit date-select">
                            <i class="el-icon-search"></i>
                            快捷查询:
                        </span>
                            <div class="days-btn">
                                <span @click="days=0" :class="{cur:days==0}">前1天</span>
                                <span @click="days=1" :class="{cur:days==1}">前3天</span>
                                <span @click="days=2" :class="{cur:days==2}">前7天</span>
                                <span @click="days=3" :class="{cur:days==3}">前1月</span>
                            </div>
                        </div>
                    </div>

                    <div class="btns-box">
                        <div @click="btns=0" :class="{'btn-item':true,cur:btns==0}">查询</div>
                        <div @click="btns=1" :class="{'btn-item':true,cur:btns==1}">重置</div>
                        <div @click="btns=2" :class="{'btn-item':true,cur:btns==2}">查询</div>
                    </div>

                </div>
            </el-collapse-transition>

        </div>

        <!--能耗-->
        <div class="consumption-box">
            <div class="consumption-item">
                <div class="head">
                    <i class="icon-nh"></i>
                    hakdjsfnaldsf
                </div>
                <div class="electricity">
                    <span class="ele-tit">用电量</span>
                    <span class="num">1066.56</span>
                    <span class="unit">kWh</span>
                </div>
            </div>
        </div>
        <!--能耗-->

    </div>
</template>

<script>
    export default {
        name: "inquire",
        data() {
            return {
                radio: '1',
                filtrateShow: true,
                days: 2,
                btns: 0,
                checked1: true,
                checked2: false,
                checked3: false,
                checked4: false,
                select1: '',
                select2: '',
                select3: '',
                select4: '',
                sw: true,
                value6: '',
                options: [{
                    value: '选项1',
                    label: '黄金糕'
                }, {
                    value: '选项2',
                    label: '双皮奶'
                }, {
                    value: '选项3',
                    label: '蚵仔煎'
                }, {
                    value: '选项4',
                    label: '龙须面'
                }, {
                    value: '选项5',
                    label: '北京烤鸭'
                }],
            }
        }
    }
</script>
<style>
    .Inquire .el-radio__input.is-checked .el-radio__inner {
        background: url("../../assets/NengHaoChaXun/icon_xz.png") no-repeat;

    }

    .Inquire .el-radio__inner {
        border: 0;
        /*border-radius: 100%;*/
        width: 16px;
        height: 16px;
        /*background-color: #3496AE;*/
        cursor: pointer;
        -webkit-box-sizing: border-box;
        box-sizing: border-box;
        background: url("../../assets/NengHaoChaXun/icon_wxz.png") no-repeat;
        /*border:1px solid rgba(146, 226, 234, 1);*/
        /*box-shadow:0px 3px 18px 0px rgba(52,150,174,1);*/
    }

    .Inquire .el-radio__inner::after {
        background: none;
    }

    .Inquire .el-radio__input.is-checked + .el-radio__label {
        color: rgba(223, 253, 255, 1);
    }

    .Inquire .el-radio__label {
        font-size: 14px;
        padding-left: 5px;
        /*font-size:14px;*/
        font-family: HiraginoSansGB-W3;
        font-weight: bold;
        color: rgba(223, 253, 255, 1);
    }

    .Inquire .el-checkbox__input.is-checked .el-checkbox__inner, .el-checkbox__input.is-indeterminate .el-checkbox__inner {
        background-color: #2DF3FF;
        border-color: #2DF3FF;
    }

    .Inquire .el-checkbox__input.is-checked + .el-checkbox__label {
        color: #DFFDFF;
    }

    .Inquire .el-checkbox__inner::after {
        -webkit-box-sizing: content-box;
        box-sizing: content-box;
        content: "";
        border: 2px solid #185488;
        border-left: 0;
        border-top: 0;
        height: 7px;
        left: 4px;
        position: absolute;
        top: 1px;
        -webkit-transform: rotate(45deg) scaleY(0);
        -ms-transform: rotate(45deg) scaleY(0);
        transform: rotate(45deg) scaleY(0);
        width: 3px;
        -webkit-transition: -webkit-transform .15s ease-in .05s;
        transition: -webkit-transform .15s ease-in .05s;
        -o-transition: transform .15s ease-in .05s;
        transition: transform .15s ease-in .05s;
        transition: transform .15s ease-in .05s, -webkit-transform .15s ease-in .05s;
        transition: transform .15s ease-in .05s, -webkit-transform .15s ease-in .05s;
        -webkit-transform-origin: center;
        -ms-transform-origin: center;
        transform-origin: center;
    }

    .Inquire .el-checkbox__label {
        display: inline-block;
        padding-left: 10px;
        line-height: 19px;
        font-size: 14px;
        color: #DFFDFF;
    }

    .Inquire .el-input--small .item2 .el-input__inner {
        height: 28px;
        line-height: 28px;
    }

    .Inquire .item2 .el-input__inner {
        -webkit-appearance: none;
        background-color: #174B7B;
        background-image: none;
        border-radius: 2px;
        border: 1px solid #2DF3FF;
        -webkit-box-sizing: border-box;
        box-sizing: border-box;
        color: #BECDDE;
        display: inline-block;
        font-size: inherit;
        height: 40px;
        line-height: 40px;
        outline: 0;
        padding: 0 15px;
        -webkit-transition: border-color .2s cubic-bezier(.645, .045, .355, 1);
        -o-transition: border-color .2s cubic-bezier(.645, .045, .355, 1);
        transition: border-color .2s cubic-bezier(.645, .045, .355, 1);
        width: 100%;
    }

    .Inquire .el-select:hover {
        border-color: #2DF3FF;
    }

    .Inquire .el-select .el-input__inner:focus {
        border-color: #2DF3FF;
    }

    .Inquire .el-select .el-input .el-select__caret {
        color: #2DF3FF;
        font-size: 15px;
        font-weight: 600;
        -webkit-transition: -webkit-transform .3s;
        transition: -webkit-transform .3s;
        -o-transition: transform .3s;
        transition: transform .3s;
        transition: transform .3s, -webkit-transform .3s;
        transition: transform .3s, -webkit-transform .3s;
        -webkit-transform: rotateZ(180deg);
        -ms-transform: rotate(180deg);
        transform: rotateZ(180deg);
        cursor: pointer;
    }

    .Inquire .el-range-editor--small.el-input__inner {
        background: #174B7B;
        border: 0 solid #2DF3FF;
    }

    .Inquire .el-range-editor--small .el-range-input {
        width: 220px;
        border: 1px solid #2DF3FF;
        background: #174B7B;
        color: #DBFDFF;
    }

    .Inquire .el-date-editor .el-range__icon {
        color: #2DF3FF;
    }

    .Inquire .el-date-editor--daterange.el-input, .el-date-editor--daterange.el-input__inner, .el-date-editor--timerange.el-input, .el-date-editor--timerange.el-input__inner {
        width: 542px;
    }

    .Inquire .el-range-editor--small .el-range-separator {
        line-height: 24px;
        font-size: 13px;
        color: #2DF3FF;
    }
</style>
<style lang="scss" scoped>
    .Inquire {
        width: 100%;
        height: 100%;
        position: relative;

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
            padding: 15px 20px;
            background-color: #0B3F6F;
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
                h3 {
                    font-size: 16px;
                    font-family: HiraginoSansGB-W3;
                    font-weight: bold;
                    color: rgba(254, 254, 255, 1);
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
                .item-row {
                    height: 60px;
                    width: 100%;
                    background-color: #174B7B;
                    display: flex;
                    align-items: center;
                    border-bottom: 2px solid #0B3F6F;
                    box-sizing: border-box;
                    padding: 0 10px;
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
                .btns-box {
                    width: 100%;
                    display: flex;
                    justify-content: flex-end;
                    margin-top: 17px;
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

    }
</style>
