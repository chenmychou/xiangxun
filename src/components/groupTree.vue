<template>
 <div>
    <div class="tree3">
      <v-tree ref='tree1' :canDeleteRoot="false" :data='treeData' :draggable='false' :tpl='tplJsx' :halfcheck='true'/>
    </div>
 </div>
</template>

<script>
import icon from '@/assets/images/file.png'
import iconfile from '@/assets/images/file_package.png'
export default {
  name: 'groupTree',
  props: ['treeData','mtype'],
  data () {
    return {
    }
  },
  methods: {
    tplJsx (...args) {
      let {0: node,1: children} = args
      let titleClass = node.selected ? 'node-title node-selected' : 'node-title'
      let icon1 = (node.children && node.children.length) > 0 ? iconfile : icon;
      node.expanded = true
      return (<span>
            {<img style="vertical-align: middle;" src={icon1}/>}
            <span class={titleClass} domPropsInnerHTML={node.name} onClick={() => {
                this.doRefreshList(node.id)
            }} />
      </span>)
    },
    doRefreshList (organizeId){
        if(this.mtype == 1){
            this.$emit('searchTermList',organizeId)
        }else if(this.mtype == 2){
            this.$emit('searchOrganizeList',organizeId)
        }else if(this.mtype == 3){
            this.$emit('searchUserListData',organizeId)
        }
    }
  }
}
</script>
<style>
.tree3{
  /* float: left; */
  /* width: 30%; */
  margin-top: 0px;
  padding: 24px;
  box-sizing: border-box;
  border: 1px solid #083775;
  box-shadow:0px 0px  3px 0px #083775;
  overflow: auto;
  height: 450px;
}
.treebtn1{
  background-color: transparent;
  border: 1px solid #ccc;
  padding: 1px 3px;
  border-radius: 5px;
  margin-right: 5px;
  color: rgb(148, 147, 147);
}
.treebtn2{
  background-color: transparent;
  border: 1px solid #ccc;
  padding: 3px 5px;
  border-radius: 5px;
  margin-left: 5px;
  color: rgb(97, 97, 97);
}
.treebtn3{
  background-color: transparent;
  border: 1px solid #ccc;
  padding: 3px 5px;
  border-radius: 5px;
  margin-left: 5px;
  color: rgb(63, 63, 63);
}
.tree-search-input{
  width: 70%;
  padding: 6px 8px;
  outline: none;
  border-radius: 6px;
  border:1px solid #ccc;
}
.tree-search-btn{
  width: 25%;
  padding: 6px 8px;
  outline: none;
  border-radius: 6px;
  background-color: rgb(218, 218, 218);
  border:1px solid rgb(226, 225, 225);
  color: rgb(117, 117, 117);
}
.halo-tree li span:hover {
    background-color: transparent
}

.fade-enter-active,
.fade-leave-active {
    transition: opacity .2s
}

.fade-enter,
.fade-leave-to {
    opacity: 0
}

.halo-tree .expand-enter-active {
    transition: all 3s ease;
    height: 50px;
    overflow: hidden
}

.halo-tree .expand-leave-active {
    transition: all 3s ease;
    height: 0;
    overflow: hidden
}

.halo-tree .expand-enter,
.halo-tree .expand-leave {
    height: 0;
    opacity: 0
}

.halo-tree {
    font-size: 1rem;
    -webkit-transition: height .3s ease-in-out, padding-top .3s ease-in-out, padding-bottom .3s ease-in-out;
    transition: height .3s ease-in-out, padding-top .3s ease-in-out, padding-bottom .3s ease-in-out
}

.halo-tree ul {
    box-sizing: border-box
}

.halo-tree li,
.halo-tree ul {
    list-style-type: none;
    text-align: left
}

.halo-tree .inputCheck {
    display: inline-block;
    position: relative;
    width: 14px;
    height: 14px;
    border: 1px solid #0f76a1!important;
    border-radius: 50%!important;
    top: 4px;
    text-align: center;
    font-size: 0.875rem;
    line-height: 14px
}

.halo-tree .inputCheck.notAllNodes:before {
    content: "\2713";
    display: block;
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: #888;
    z-index: 1;
    color: #fff
}

.halo-tree .inputCheck.box-checked:after {
    content: "\2713";
    display: block;
    position: absolute;
    z-index: 1;
    width: 100%;
    text-align: center
}

.halo-tree .box-halfchecked {
    background-color: #888
}

.halo-tree .box-halfchecked:after {
    content: "\2713";
    display: block;
    position: absolute;
    z-index: 1;
    width: 100%;
    text-align: center;
    color: #fff
}

.halo-tree .check {
    display: block;
    position: absolute;
    font-size: 0.875rem;
    width: 16px;
    height: 16px;
    left: -5px;
    top: -4px;
    border: 1px solid #0f76a1!important;
    opacity: 0;
    cursor: pointer;
    -ms-filter: "progid:DXImageTransform.Microsoft.Alpha(Opacity=0)";
    filter: alpha(opacity=0);
    z-index: 2
}

.halo-tree .chkDisabled {
    background-color: #f5f5f5;
    opacity: 1;
    cursor: not-allowed
}

.halo-tree li {
    margin: 0;
    padding: 5px 5px 5px 15px;
    position: relative;
    list-style: none
}

.halo-tree li:after,
.halo-tree li:before {
    content: "";
    left: -8px;
    position: absolute;
    right: auto;
    border-width: 1px
}

.halo-tree li:before {
    border-left: 1px dashed #0f76a1!important;
    bottom: 50px;
    height: 100%;
    top: -8px;
    width: 1px
}

.halo-tree li:after {
    border-top: 1px dashed #0f76a1!important;
    height: 20px;
    top: 17px;
    width: 28px
}

.halo-tree li:last-child:before {
    height: 26px
}

.halo-tree>li.first-node:before {
    top: 17px
}

.halo-tree>li.second-node:before {
    top: 4px
}

.halo-tree>li.first-node.only-node:before {
    border-left: none!important;
}

.halo-tree>li.only-node:after {
    border-top: none!important;
}

.halo-tree>ul {
    padding-left: 0
}

.halo-tree ul {
    padding-left: 17px;
    padding-top: 10px
}

.halo-tree .tree-expand {
    display: inline-block;
    width: 14px;
    height: 14px;
    text-align: center;
    line-height: 13px;
    border: 1px solid #0f76a1!important;
    background:#0b122e!important;
    border-radius: 2px;
    font-style: normal
}

.halo-tree .tree-open {
    line-height: 13px
}

.halo-tree .tree-close:after {
    content: "+";
    color:#0f76a1;
}

.halo-tree .tree-open:after {
    content: "-";
    color:#0f76a1;
}

.halo-tree .tree-empty:after {
    content: ""
}

.halo-tree .tree-node-el {
    background: #0b122e!important;
    padding-left: 2px;
    position: relative;
    z-index: 3
}

.halo-tree li.leaf {
    padding-left: 15px
}

.halo-tree li.leaf:after {
    content: "";
    left: -7px;
    position: absolute;
    right: auto;
    border-width: 1px;
    border-top: 1px dashed #0f76a1;
    height: 20px;
    top: 17px;
    width: 25px
}

.halo-tree-search-box {
    height: 18px;
    line-height: 18px;
    outline: none;
    border: 1px solid #888;
    border-radius: 3px
}

.halo-tree-search-box:focus {
    border: 1px solid #108ee9;
    -webkit-box-shadow: 0 2px 2px rgba(16, 142, 233, .2);
    box-shadow: 0 2px 2px rgba(16, 142, 233, .2);
    -webkit-transition: border-color .15s ease-in-out, -webkit-box-shadow .15s ease-in-out;
    -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
    transition: border-color .15s ease-in-out, box-shadow .15s ease-in-out
}

.halo-tree .node-title {
    padding: 3px;
    border-radius: 3px;
    cursor: pointer;
    margin: 0 2px;
    color:#7dd7f9;
}

.halo-tree .node-title:hover {
    background-color: #2b2626!important;
}

.halo-tree .node-title-disabled {
    padding: 3px;
    border-radius: 3px;
    background-color: #f5f5f5;
    opacity: 1;
    cursor: not-allowed;
    margin: 0 2px
}

.halo-tree .node-title-disabled:hover {
    background-color: #f5f5f5
}

.halo-tree .node-selected {
    border: 1px solid #ddd;
    background-color: #2b2626!important;
}

.halo-tree .node-title.node-searched {
    border: 1px solid #ff8247
}

svg[data-v-e7743bdc] {
    height: 14px;
    width: 14px;
    overflow: visible;
    line-height: 14px
}

circle[data-v-e7743bdc] {
    fill: #1e90ff;
    fill-opacity: 0;
    -webkit-animation: opacity-data-v-e7743bdc 1.2s linear infinite;
    animation: opacity-data-v-e7743bdc 1.2s linear infinite
}

circle[data-v-e7743bdc]:nth-child(12n+1) {
    -webkit-animation-delay: -.1s;
    animation-delay: -.1s
}

circle[data-v-e7743bdc]:nth-child(12n+2) {
    -webkit-animation-delay: -.2s;
    animation-delay: -.2s
}

circle[data-v-e7743bdc]:nth-child(12n+3) {
    -webkit-animation-delay: -.3s;
    animation-delay: -.3s
}

circle[data-v-e7743bdc]:nth-child(12n+4) {
    -webkit-animation-delay: -.4s;
    animation-delay: -.4s
}

circle[data-v-e7743bdc]:nth-child(12n+5) {
    -webkit-animation-delay: -.5s;
    animation-delay: -.5s
}

circle[data-v-e7743bdc]:nth-child(12n+6) {
    -webkit-animation-delay: -.6s;
    animation-delay: -.6s
}

circle[data-v-e7743bdc]:nth-child(12n+7) {
    -webkit-animation-delay: -.7s;
    animation-delay: -.7s
}

circle[data-v-e7743bdc]:nth-child(12n+8) {
    -webkit-animation-delay: -.8s;
    animation-delay: -.8s
}

circle[data-v-e7743bdc]:nth-child(12n+9) {
    -webkit-animation-delay: -.9s;
    animation-delay: -.9s
}

circle[data-v-e7743bdc]:nth-child(12n+10) {
    -webkit-animation-delay: -1s;
    animation-delay: -1s
}

circle[data-v-e7743bdc]:nth-child(12n+11) {
    -webkit-animation-delay: -1.1s;
    animation-delay: -1.1s
}

circle[data-v-e7743bdc]:nth-child(12n+12) {
    -webkit-animation-delay: -1.2s;
    animation-delay: -1.2s
}

.g-circles--v2 circle[data-v-e7743bdc] {
    fill-opacity: 0;
    stroke-opacity: 0;
    stroke-width: 1;
    stroke: #9acd32;
    -webkit-animation-name: opacity-stroke-data-v-e7743bdc, colors-data-v-e7743bdc, colors-stroke-data-v-e7743bdc, transform-2-data-v-e7743bdc;
    animation-name: opacity-stroke-data-v-e7743bdc, colors-data-v-e7743bdc, colors-stroke-data-v-e7743bdc, transform-2-data-v-e7743bdc
}

.g-circles--v3 circle[data-v-e7743bdc] {
    fill-opacity: 1;
    -webkit-animation-name: opacity-data-v-e7743bdc, colors-data-v-e7743bdc;
    animation-name: opacity-data-v-e7743bdc, colors-data-v-e7743bdc
}

.g-circles--v4 circle[data-v-e7743bdc] {
    fill-opacity: 1;
    fill: orange;
    -webkit-transform-origin: 60px 60px;
    -ms-transform-origin: 60px 60px;
    transform-origin: 60px 60px;
    -webkit-animation-name: opacity-data-v-e7743bdc, colors-3-data-v-e7743bdc, transform-data-v-e7743bdc;
    animation-name: opacity-data-v-e7743bdc, colors-3-data-v-e7743bdc, transform-data-v-e7743bdc
}

@-webkit-keyframes opacity-data-v-e7743bdc {
    3% {
        fill-opacity: 1
    }
    75% {
        fill-opacity: 0
    }
}

@keyframes opacity-data-v-e7743bdc {
    3% {
        fill-opacity: 1
    }
    75% {
        fill-opacity: 0
    }
}

@-webkit-keyframes opacity-stroke-data-v-e7743bdc {
    10% {
        stroke-opacity: 1
    }
    85% {
        stroke-opacity: 0
    }
}

@keyframes opacity-stroke-data-v-e7743bdc {
    10% {
        stroke-opacity: 1
    }
    85% {
        stroke-opacity: 0
    }
}

@-webkit-keyframes colors-data-v-e7743bdc {
    0% {
        fill: #9acd32
    }
    10% {
        fill: gold
    }
    75% {
        fill: crimson
    }
}

@keyframes colors-data-v-e7743bdc {
    0% {
        fill: #9acd32
    }
    10% {
        fill: gold
    }
    75% {
        fill: crimson
    }
}

@-webkit-keyframes colors-stroke-data-v-e7743bdc {
    0% {
        stroke: #9acd32
    }
    10% {
        stroke: gold
    }
    75% {
        stroke: crimson
    }
}

@keyframes colors-stroke-data-v-e7743bdc {
    0% {
        stroke: #9acd32
    }
    10% {
        stroke: gold
    }
    75% {
        stroke: crimson
    }
}

@-webkit-keyframes colors-2-data-v-e7743bdc {
    0% {
        fill: #ff0
    }
    50% {
        fill: red
    }
    65% {
        fill: #ff4500
    }
    95% {
        fill: gold
    }
}

@keyframes colors-2-data-v-e7743bdc {
    0% {
        fill: #ff0
    }
    50% {
        fill: red
    }
    65% {
        fill: #ff4500
    }
    95% {
        fill: gold
    }
}

@-webkit-keyframes colors-3-data-v-e7743bdc {
    0% {
        fill: #9acd32
    }
    50% {
        fill: #40e0d0
    }
    65% {
        fill: #ff0
    }
    95% {
        fill: orange
    }
}

@keyframes colors-3-data-v-e7743bdc {
    0% {
        fill: #9acd32
    }
    50% {
        fill: #40e0d0
    }
    65% {
        fill: #ff0
    }
    95% {
        fill: orange
    }
}

@-webkit-keyframes transform-data-v-e7743bdc {
    10% {
        -webkit-transform: scale(.75);
        transform: scale(.75)
    }
}

@keyframes transform-data-v-e7743bdc {
    10% {
        -webkit-transform: scale(.75);
        transform: scale(.75)
    }
}

@-webkit-keyframes transform-2-data-v-e7743bdc {
    40% {
        -webkit-transform: scale(.85);
        transform: scale(.85)
    }
    60% {
        stroke-width: 20
    }
}

@keyframes transform-2-data-v-e7743bdc {
    40% {
        -webkit-transform: scale(.85);
        transform: scale(.85)
    }
    60% {
        stroke-width: 20
    }
}

.tree-container {
    position: relative;
    width: 90%;
    height: 36px;
    border: 1px solid #ccc;
    border-radius: 6px
}

.tag-box-container {
    position: relative;
    width: 100%;
    height: 36px;
    overflow: hidden
}

.tag-box {
    width: 2000%;
    height: 36px
}

.tree-box {
    margin-top: 3px;
    border-radius: 6px;
    border: 1px solid #ccc;
    box-shadow: 0 0 5px rgba(0, 0, 0, .4)
}

.tree-box ul {
    margin-left: 0;
    -webkit-padding-start: 10px
}

.search-input {
    width: 96%;
    height: 30px;
    box-sizing: border-box;
    margin: 5px auto 0;
    font-size: 0.875rem;
    text-indent: 1em;
    outline: none
}

.search-input,
.tag {
    border: 1px solid #ccc;
    border-radius: 6px
}

.tag {
    float: left;
    position: relative;
    min-width: 50px;
    height: 26px;
    margin: 4px;
    padding: 0 10px;
    line-height: 26px;
    text-align: center;
    background-color: #fff;
    user-select: none;
    cursor: default;
    transition: padding .3s
}

.tag .rmNode {
    display: none
}

.tag:hover {
    padding-right: 25px
}

.tag:hover>.rmNode {
    display: block !important
}

.blank {
    background-color: #fff;
    border: 0
}

.rmNode {
    position: absolute;
    right: 5px;
    top: 5px;
    width: 15px;
    height: 15px;
    line-height: 15px;
    font-size: 0.75rem;
    background-color: #b3b3b3;
    color: #ececec;
    border-radius: 50%;
    cursor: pointer
}

.fade-enter-active,
.fade-leave-active {
    transition: opacity .5s, transform .5s
}

.fade-enter,
.fade-leave-active {
    opacity: 0;
    transform: translateY(-10px)
}

</style>
