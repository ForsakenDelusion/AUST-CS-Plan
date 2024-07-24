---
statistics: true
---


# 前言

本项目旨在为初入大学的CS新生提供引导。

本指南将会提供不同的学习路线供大家参考。由于个人能力有限，所以期待贡献者们的加入。

本指南更多的偏向于提高计科人的综合技能，而不是应试能力。请各位明确自己想要在哪方面获得提升。在后文中，可能会涉及到国外的公开课，面对全英的学习环境或许你会感到焦虑或者恐慌，但请你放松，能够流畅的阅读英文文档也是cser必备的技能。

!!! info "网站统计"
    页面总数：{{pages}}  
    总字数：{{words}}  
    代码块行数：{{codes}} 
    网站运行时间：<span id="web-time"></span>



<script>
var _hmt = _hmt || [];
(function() {
  var hm = document.createElement("script");
  hm.src = "https://hm.baidu.com/hm.js?28f18450da302a3ecb5dafd02685a81f";
  var s = document.getElementsByTagName("script")[0]; 
  s.parentNode.insertBefore(hm, s);
})();
</script>

<script>
function updateTime() {
    var date = new Date();
    var now = date.getTime();
    var startDate = new Date("2024/06/25 00:00:00");
    var start = startDate.getTime();
    var diff = now - start;
    var y, d, h, m;
    y = Math.floor(diff / (365 * 24 * 3600 * 1000));
    diff -= y * 365 * 24 * 3600 * 1000;
    d = Math.floor(diff / (24 * 3600 * 1000));
    h = Math.floor(diff / (3600 * 1000) % 24);
    m = Math.floor(diff / (60 * 1000) % 60);
    if (y == 0) {
        document.getElementById("web-time").innerHTML = d + "<span class=\"heti-spacing\"> </span>天<span class=\"heti-spacing\"> </span>" + h + "<span class=\"heti-spacing\"> </span>小时<span class=\"heti-spacing\"> </span>" + m + "<span class=\"heti-spacing\"> </span>分钟";
    } else {
        document.getElementById("web-time").innerHTML = y + "<span class=\"heti-spacing\"> </span>年<span class=\"heti-spacing\"> </span>" + d + "<span class=\"heti-spacing\"> </span>天<span class=\"heti-spacing\"> </span>" + h + "<span class=\"heti-spacing\"> </span>小时<span class=\"heti-spacing\"> </span>" + m + "<span class=\"heti-spacing\"> </span>分钟";
    }
    setTimeout(updateTime, 1000 * 60);
}
updateTime();
function toggle_statistics() {
    var statistics = document.getElementById("statistics");
    if (statistics.style.opacity == 0) {
        statistics.style.opacity = 1;
    } else {
        statistics.style.opacity = 0;
    }
}
</script>
