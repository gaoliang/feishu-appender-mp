<template>
  <scroll-view scroll-x class="container">
    <text v-if="options.trace === undefined">只能从推送消息中进入哦～</text>
    <uni-notice-bar single="true" text="注意，过长的Stack Trace 可能会被截断，仅供参考"></uni-notice-bar>
    <view>
      <text selectable="true" class="first-line">{{firstLine}}</text>
    </view>
    <br />
    <text space="ensp" selectable="true" class="other-line">{{otherLine}}</text>
  </scroll-view>
</template>

<script>
import { Base64 } from "js-base64";

import uniNoticeBar from "@dcloudio/uni-ui/lib/uni-notice-bar/uni-notice-bar.vue";
export default {
  components: { uniNoticeBar },

  onLoad: function(options) {
	this.options = options;
    let text = Base64.decode(options.trace);
    let lines = text.split("\n");
    this.firstLine = lines.shift();
	this.otherLine = lines.join("\n");
  },
  data() {
    return {
	  options: {},
      firstLine: "firstLine",
      otherLine: "otherLine"
    };
  },
  methods: {}
};
</script>

<style>
.container {
  line-height: 12px;
}
.first-line {
  font-size: 13px;
  font-family: "Courier New", Courier, monospace;
}
.other-line {
  white-space: nowrap;
  font-size: 13px;
  font-family: "Courier New", Courier, monospace;
}
</style>
