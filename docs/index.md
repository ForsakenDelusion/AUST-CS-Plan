---
statistics: true
---


# 前言

本项目旨在为初入大学的CS新生提供引导。

本指南将会提供不同的学习路线供大家参考。由于个人能力有限，所以期待贡献者们的加入。

本指南更多的偏向于提高计科人的综合技能，而不是应试能力。请各位明确自己想要什么。在后文中，可能会涉及到国外的公开课，面对全英的学习环境或许你会感到焦虑或者恐慌，但请你放松，能够流畅的阅读英文文档也是cser必备的技能。当然，本指南也包括着很多中文课程以及资料，这些课程大部分来源于B站，这部分课程通常来自不同的机构，每一类课程通常都有不同年份的版本，所以这里只会笼统的提供几个主流机构的系统课，希望大家挑选适合自己的课程去学习。

## 初入计算机

我相信大部分选择计算机专业的同学们，可能对未来的方向没有特别的清晰。一部分同学可能抱着喜欢科技，数码产品的念头就选择了计算机专业，另一部分可能是因为听说计算机前途好所以选择计算机专业。但是通常的情况是读完大一就彻底变成“老油条”，忘记了当初为什么要选择计算机，甚至在了解到计算机就业有多“卷”之后后悔来读计算机。所以我也会提供我所有的认知来帮助大家规划自己的路线。

>以下内容选自csdiy: 如果你刚刚进入大学校园或者还在低年级，并且就读的是计算机方向或者想要转到计算机方向，那么你很幸运，因为学习是你的本业，你可以有充足的时间和自由来学习自己感兴趣的东西，不会有工作的压力和生活的琐碎，不必过于纠结“学了有没有用”，“能不能找到工作”这类功利的想法。那么该如何安排自己的学业呢？我觉得首要的一点就是要打破在高中形成的“按部就班”式的被动学习。作为一个小镇做题家，我深知国内大部分高中会把大家一天当中的每一分钟都安排得满满当当，你只需要被动地跟着课表按部就班地完成一个个既定的任务。只要足够认真，结果都不会太差。但步入大学的校门，自由度一下子变大了许多。首先所有的课外时间基本都由你自由支配，没有人为你整理知识点，总结提纲，考试也不像高中那般模式化。如果你还抱着高中那种“乖学生”的心态，老老实实按部就班，结果未必如你所愿。因为专业培养方案未必就是合理，老师的教学未必就会负责，认真出席课堂未必就能听懂，甚至考试内容未必就和讲的有关系。

首先我们可以把大学分为三个阶段：

第一阶段是大一大二，在这个阶段你有大把的时间可以学习，因为这个时候你没有升学或者就业的压力，你可以自由的选择你感兴趣的方向进行学习。在这个阶段，我们可以先培养对计算机的认知与兴趣，并打好基础。这里的基础不是指学好课堂上的课程就好了，在课程之外我们仍然有很多能力需要培养！我认为这才是国内非计算机强校最缺失的一部分，请移步到[“CS基础-先修部分”](https://aust-cs-plan.forsakendelusion.online/计算机科学学习路线/计算机基础/工具/)进行阅读.

第二阶段是大三到大四上，一般这个时候我们就会面临着考研或者就业的压力，如果你现在处于这个阶段，那么我建议不要花太多经历在公开课上，考研的同学认真学习。准备就业的同学面向就业学习，多做项目或者参加开源，如果你充分的利用第一阶段的时间进行学习的话，我相信你在就业上也是有相当的竞争力。

第三个阶段是大四下，~~因为我还没经历过所以也没有太多认知~~。

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
