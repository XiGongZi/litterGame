<template>
  <div class="coordinate-random">
    <div class="background">
      
    </div>
  </div>
</template>
<script>
export default {
  name: 'coordinate-random',
  components: {},
  data() {
    return {
      screenInfo:[0, 0],
      safeBorder:[[],[]]
    };
  },
  props: {
    coordinateRandom: {
      type: Object,
      default() {
        return {
          radious:0,
          timeSet:{
            hide:1000
          },
          countArr:[1,1,1,1,1,1,1,1,1,1]
        };
      }
    }
  },
  computed: {},
  created() {
    // let sja = new Circle(3,2,1,1);
    // console.log(sja.y);
        // let screen_width = document.body.offsetWidth;
        // let screen_height = document.body.offsetHeight ;
  },
  mounted() {
    // 得到正确的宽高值并放入data
    this.screenInfo = [document.body.offsetWidth,document.body.offsetHeight];

  },
  watch: {
    // 这一条用来约束默认安全区域，需要从父组件传入半径
    screenInfo:function(){
      let r = this.coordinateRandom.radious;
      let x = this.screenInfo[0];
      let y = this.screenInfo[1];
      console.log([r,x,y])
      this.safeBorder =  [[r,r],[x-r,y-r]];
    }
  },
  methods: {
    // 安全策略
    /*
        组件需要接受的值
          1.r的范围 arr
          2.挡板显示的时间  num
          3.每次需要显示的数量（包含一共需要多少次） arr


        1.判断边界，是否过于贴近边界
          a.限定边界
            [[0 + r,0 + r],[screen_width - r，screen_height - r]]
        2.判断碰撞，是否过于贴近已有的圆心
          a.计算已生成的圆心和刚生成的圆心距离是否大于两者半径的和，是则安全，否则不安全需要重新生成
            GetDistance([],[])
    */
    randomCoor:function(){
      /*接受值：
          1.
      */
    },
    GetDistance:function([x1,y1],[x2,y2]){
        console.log(x2)
        console.log('x2')
        var radLat1 = x1 - x2;
        var radLat2 = y1 - y2;
        return Math.sqrt(Math.pow(radLat1,2) + Math.pow(radLat2,2));
    }
  }
};
  // function GetDistance([x1,y1],[x2,y2]){
  //       console.log(x2)
  //       console.log('x2')
  //       var radLat1 = x1 - x2;
  //       var radLat2 = y1 - y2;
  //       return Math.sqrt(Math.pow(radLat1,2) + Math.pow(radLat2,2));
  //   }
// class Circle {
//   constructor({x = 0,y = 0,r = 0,z = 0} = {}){
//     this.x = x;
//     this.y = y;
//     this.center = [x,y];
//     this.radious = r;
//     this.z = z;
//   }
//   toString() {
//     return {
//       center:[this.x,this.y],
//       radious:this.r
//     }
//   }
// }




</script>
<style lang="less" scoped>
.coordinate-random {
  height:100vh;
  width:100vw;
  .background{
    height:100%;
    background:#bde9e4;
  }

}

//  0.点击圆盘后，分十次依次出现不同数字，每次数字出现后n秒后隐藏，当用户从小到大点击正确的数字时则判断通过，否则震动手机并提示，十次后给出统计结果。
//  1.针对整个屏幕生成坐标系
//  2.每个数字定义一个圆心和半径。随机生成位置时判断是否合法，若合法则放置否则继续随机生成。。一直取完'数字后'到达3.
//  3.等待n毫秒，将‘数字’顶部的遮挡show（图片或颜色）
//  4.监听用户点击事件，每当错误点击时触发错误反馈（震动并发声），当完全按顺序点击时进入过场动画
//  5.过场动画时，清空坐标系上的数字，重新从2开始。
//  6.10次后反馈最终结果。

// 每个数字定义一个圆心和半径。随机生成位置时判断是否合法，若合法则放置否则继续随机生成。
</style>
