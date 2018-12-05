<template>
    <div class="RTData">
        <transition name="el-zoom-in-center">
        <div v-show="leftShow" class="left-branch">
            <div class="tit">选择支路</div>
            <div class="inputBox">
                <i class="icon-ss"></i>
                <input placeholder="请输入支路名称" type="text" id="key" value="" class="empty"/><br/>
            </div>
            <!--<div class="zTreeDemoBackground left">-->
            <ul id="treeDemo" class="ztree"></ul>
            <!--</div>-->
            <div class="butt">
                <div class="tit">已选支路</div>
                <ul>
                    <li><i :class="option == 0?'icon-not':'icon-yes'"></i><span>2AH103-馈线-</span></li>
                    <li><i :class="option == 1?'icon-not':'icon-yes'"></i><span>2AH103-馈线-</span></li>
                    <li><i :class="option == 2?'icon-not':'icon-yes'"></i><span>2AH103-馈线-</span></li>
                </ul>
            </div>
        </div>
        </transition>
        <div class="main">
            <div @click="leftShow=!leftShow" class="btn">支 路 选 择</div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "ShiShiShuJu",
        data() {
            return {
                option:'2',
                leftShow:true
            }
        },
        mounted() {
            var setting = {
                check: {
                    enable: true,

                },
                view: {
                    nameIsHTML: true, //允许name支持html
                    selectedMulti: false
                },
                edit: {
                    enable: false,
                    editNameSelectAll: false
                },
                data: {
                    simpleData: {
                        enable: true
                    }
                }
            };

            var zNodes = [
                {
                    id: 1,
                    pId: 0,
                    name: "随意勾选 1",
                    open: true,
                    // iconSkin: "icon01"
                },
                {
                    id: 11,
                    pId: 1,
                    name: "随意勾选 1-1",
                    open: true,
                    // iconSkin: "icon01"
                },
                {
                    id: 111,
                    pId: 11,
                    name: "随意勾选 1-1-1"
                },
                {
                    id: 112,
                    pId: 11,
                    name: "随意勾选 1-1-2"
                },
                {
                    id: 12,
                    pId: 1,
                    name: "随意勾选 1-2",
                    open: true,
                    // iconSkin: "icon01"
                },
                {
                    id: 121,
                    pId: 12,
                    name: "随意勾选 1-2-1"},
                {
                    id: 122,
                    pId: 12,
                    name: "随意勾选 1-2-2"
                },
                {
                    id: 2,
                    pId: 0,
                    name: "随意勾选 2",
                    checked: true,
                    open: true,
                    // iconSkin: "icon01"
                },
                {
                    id: 21,
                    pId: 2,
                    name: "随意勾选 2-1"
                },
                {
                    id: 22,
                    pId: 2,
                    name: "随意勾选 2-2",
                    open: true,
                    // iconSkin: "icon01"
                },
                {
                    id: 221,
                    pId: 22,
                    name: "随意勾选 2-2-1",
                    // checked: true,
                },
                {
                    id: 222,
                    pId: 22,
                    name: "随意勾选 2-2-2"
                },
                {
                    id: 23,
                    pId: 2,
                    name: "随意勾选 2-3"
                }
            ];

            var code;

            function setCheck() {
                var zTree = $.fn.zTree.getZTreeObj("treeDemo"),
                    py = $("#py").attr("checked") ? "p" : "",
                    sy = $("#sy").attr("checked") ? "s" : "",
                    pn = $("#pn").attr("checked") ? "p" : "",
                    sn = $("#sn").attr("checked") ? "s" : "",
                    type = {"Y": py + sy, "N": pn + sn};
                zTree.setting.check.chkboxType = type;
                showCode('setting.check.chkboxType = { "Y" : "' + type.Y + '", "N" : "' + type.N + '" };');
            }

            function showCode(str) {
                if (!code) code = $("#code");
                code.empty();
                code.append("<li>" + str + "</li>");
            }


            $.fn.zTree.init($("#treeDemo"), setting, zNodes);
            fuzzySearch('treeDemo', '#key', null, true); //初始化模糊搜索方法
            setCheck();
            $("#py").bind("change", setCheck);
            $("#sy").bind("change", setCheck);
            $("#pn").bind("change", setCheck);
            $("#sn").bind("change", setCheck);

        }

    }
</script>

<style>
    .ztree li span.button.ico_open,.ztree li span.button.ico_close {
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
    .ztree li span.button.ico_docu{
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
    .ztree li span.node_name{
        margin-left: 4px;
        font-size:12px;
        font-family:HiraginoSansGB-W3;
        font-weight:normal;
        color:rgba(254,254,254,1);
    }

    .ztree li span.button.chk.checkbox_false_full, .ztree li span.button.chk.checkbox_false_full_focus {
        width: 16px;
        height: 16px;
        background: url("../../assets/PeiDianJianCe/icon_wxz.png") no-repeat;
        background-position: 0 0;
    }
    .ztree li span.button.chk.checkbox_false_part, .ztree li span.button.chk.checkbox_false_part_focus, .ztree li span.button.chk.checkbox_true_full, .ztree li span.button.chk.checkbox_true_full_focus, .ztree li span.button.chk.checkbox_true_part, .ztree li span.button.chk.checkbox_true_part_focus{
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




</style>


<style lang="scss" scoped>
    .RTData {
        width: 100%;
        height: 100%;

        position: relative;
        display: flex;
        flex-wrap: nowrap;
        justify-content: space-between;

        .left-branch {
            width: 301px;
            height: 894px;
            box-sizing: border-box;
            margin-bottom: 40px;
            /*float: left;*/
            /*margin-right: 24px;*/
            position: relative;
            border: 1px solid red;

            background: #0A3E6E;
            border: 1px solid #1A8EA0;
            /*box-shadow:0px 0px 9px 0px rgba(1,16,31,1), 0px 0px 30px 0px rgba(42,244,255,0.84);*/
            /*opacity:0.51;*/
            box-shadow: 0px 3px 9px 0px #01101f, 0px 3px 30px 2px #1A8EA0 inset;
            border-radius: 3px;
            padding: 14px 13px;
            .inputBox{
                position: relative;
                .icon-ss{
                    display: inline-block;
                    position: absolute;
                    right: 15px;
                    bottom: 6px;
                    float: right;
                    width: 14px;
                    height: 14px;
                    background: url("../../assets/PeiDianJianCe/icon_ss（1）.png") no-repeat;
                    z-index: 5;
                }
            }
            .empty{
                width:223px;
                height:28px;
                border:1px solid rgba(45,243,255,1);
                border-radius:14px;
                background-color: #0A3E6E;
                margin-top: 20px;
                padding: 0 14px;
                box-sizing: border-box;
                position: relative;
                &:before{
                    content: '';

                }
            }
            .ztree{
                margin-top: 20px;
            }

            .tit {
                font-size: 18px;
                font-family: 'HiraginoSansGB-W3';
                font-weight: bold;
                /*font-weight: 500;*/
                color: rgba(254, 254, 255, 1);
            }
            .butt{
                width: 100%;
                position: absolute;
                bottom: 0;
                left: 0;
                box-sizing: border-box;
                padding: 9px 12px;
                border-top: 1px solid #1A9BB8;
                ul{
                    list-style: none;
                    margin-top: 5px;
                    li{
                        line-height: 30px;
                        span{
                            font-size:12px;
                            font-family:HiraginoSansGB-W3;
                            font-weight:normal;
                            color:rgba(254,254,254,1);
                            margin-left: 12px;
                        }
                    }
                }
            }
            .icon-not{
                width: 12px;
                height: 12px;
                display: inline-block;
                background: url("../../assets/PeiDianJianCe/组 97.png") no-repeat;
            }
            .icon-yes{
                width: 12px;
                height: 12px;
                display: inline-block;
                background: url("../../assets/PeiDianJianCe/椭圆 884.png") no-repeat;
            }


        }
        .main {
            width: 100%;
            height: 894px;
            /*float: left;*/
            margin-left: 24px;
            border: 1px solid #00ff00;
            position: relative;
            .btn{
                position: absolute;
                left: -25px;
                top: 0;
                width:21px;
                height:90px;
                text-align: center;
                /*line-height: 9px;*/
                box-sizing: border-box;
                padding: 12px 0;
                background:rgba(32,155,185,1);
                border:1px solid rgba(0,229,255,1);
                font-size:12px;
                font-family:HiraginoSansGB-W3;
                font-weight:bold;
                color:rgba(254,254,255,1);
            }
        }
    }
</style>
