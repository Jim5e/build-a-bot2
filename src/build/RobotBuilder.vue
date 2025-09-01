<template>
  <div class="content">

    <button class="add-to-cart" @click="addtoCart()">Add to Cart</button>



    <div class="top-row">
      <div class="top part">
        <div class = "robot-name">
          {{ selectedRobot.head.title }}
          <span v-if="selectedRobot.head.onSale"
           class="sale">Sale!</span>

        </div>
        <img :src="selectedRobot.head.src" title="head"/>
        <button @click="selectPrevHead()" class="prev-selector">&#9668;</button>
        <button @click="selectNextHead()" class="next-selector">&#9658;</button>
      </div>
    </div>
    <div class="middle-row">
      <div class="left part">
        <img :src="selectedRobot.arms.src" title="left arm"/>
        <button @click="selectPrevArms()" class="prev-selector">&#9650;</button>
        <button @click="selectNextArms()" class="next-selector">&#9660;</button>
      </div>
      <div class="center part">
        <img :src="selectedRobot.torso.src" title="left arm"/>
        <button @click="selectPrevTorso()" class="prev-selector">&#9668;</button>
        <button @click="selectNextTorso()" class="next-selector">&#9658;</button>
      </div>
      <div class="right part">
        <img :src="selectedRobot.arms2.src" title="left arm"/>
        <button @click="selectPrevArms2()" class="prev-selector">&#9650;</button>
        <button @click="selectNextArms2()" class="next-selector">&#9660;</button  >
      </div>
    </div>
    <div class="bottom-row">
      <div class="bottom part">
        <img :src="selectedRobot.base.src" title="left arm"/>
        <button @click="selectPrevBase()" class="prev-selector">&#9668;</button>
        <button @click="selectNextBase()" class="next-selector">&#9658;</button>
      </div>
    </div>
    <div>
      <h1>Cart</h1>
      <table>
        <thead>
          <tr>
            <th>Robot</th>
            <th class="cost">Cost</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="robot in cart" :key="robot">
            <td>{{ robot.robot.head.title }}</td>
            <td class="cost">{{ robot.cost }}</td>
            
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script> 
import availableParts from '../data/parts';
export default {
  name: "RobotBuilder",
  data(){
    return {
      availableParts,
      selectedHeadIndex: 0,
      selectedArmsIndex: 0,
      selectedArms2Index: 0,
      selectedTorsoIndex: 0,
      selectedBaseIndex: 0,
      cart: []  
    };
  },
  computed:{
    selectedRobot(){
      return {
        head: this.availableParts.heads[this.selectedHeadIndex],
        arms: this.availableParts.arms[this.selectedArmsIndex],
        arms2: this.availableParts.arms[this.selectedArms2Index],
        torso: this.availableParts.torsos[this.selectedTorsoIndex],
        base: this.availableParts.bases[this.selectedBaseIndex]
      };
    }
  },
  methods: {
    addtoCart(){
      const robot = this.selectedRobot;
      const cost = robot.head.cost + robot.arms.cost + robot.arms2.cost + robot.torso.cost + robot.base.cost;
      this.cart.push({robot, cost});
    },
    selectNextHead(){
      this.selectedHeadIndex = (this.selectedHeadIndex + 1) % this.availableParts.heads.length;
    },
    selectNextArms(){
      this.selectedArmsIndex = (this.selectedArmsIndex + 1) % this.availableParts.arms.length;
    },
    selectNextArms2(){
      this.selectedArms2Index = (this.selectedArms2Index + 1) % this.availableParts.arms.length;
    },
    selectNextTorso(){
      this.selectedTorsoIndex = (this.selectedTorsoIndex + 1) % this.availableParts.torsos.length;
    },
    selectNextBase(){
      this.selectedBaseIndex = (this.selectedBaseIndex + 1) % this.availableParts.bases.length;
    },

    selectPrevHead(){
      this.selectedHeadIndex = (this.selectedHeadIndex - 1 + this.availableParts.heads.length) % this.availableParts.heads.length;
    },
    selectPrevArms(){
      this.selectedArmsIndex = (this.selectedArmsIndex - 1 + this.availableParts.arms.length) % this.availableParts.arms.length;
    },
    selectPrevArms2(){
      this.selectedArms2Index = (this.selectedArms2Index - 1 + this.availableParts.arms.length) % this.availableParts.arms.length;
    },
    selectPrevTorso(){
      this.selectedTorsoIndex = (this.selectedTorsoIndex - 1 + this.availableParts.torsos.length) % this.availableParts.torsos.length;
    },
    selectPrevBase(){
      this.selectedBaseIndex = (this.selectedBaseIndex - 1 + this.availableParts.bases.length) % this.availableParts.bases.length;
    }

  }
};   
</script>

<style scoped>   
.part {
  position: relative;
  width:165px;
  height:165px;
  border: 3px solid #aaa;
} 
.part img {
  width:165px;
}
.top-row {
  display:flex;
  justify-content: space-around;
}
.middle-row {
  display:flex;
  justify-content: center;
}
.bottom-row {
  display:flex;
  justify-content: space-around;
  border-top: none;
}
.head {
  border-bottom: none;
}
.left {
  border-right: none;
}
.right {
  border-left: none;
}
.left img {
  transform: rotate(-90deg);
}
.right img {
  transform: rotate(90deg);
}
.bottom {
  border-top: none;
}
.prev-selector {
  position: absolute;
  z-index:1;
  top: -3px;
  left: -28px;
  width: 25px;
  height: 171px;
}
.next-selector {
  position: absolute;
  z-index:1;
  top: -3px;
  right: -28px;
  width: 25px;
  height: 171px;
}
.center .prev-selector, .center .next-selector {
  opacity:0.8;
}
.left .prev-selector {
  top: -28px;
  left: -3px;
  width: 144px;
  height: 25px;
}
.left .next-selector {
  top: auto;
  bottom: -28px;
  left: -3px;    
  width: 144px;
  height: 25px;
}
.right .prev-selector {
  top: -28px;
  left: 24px;  
  width: 144px;
  height: 25px;
}
.right .next-selector {
  top: auto;
  bottom: -28px;
  left: 24px;    
  width: 144px;
  height: 25px;
}
.right .next-selector {
  right: -3px;
}  

.robot-name {
  position: absolute;
  top: -25px;
  text-align: center;
  width: 100%;
}

.sale {
  color: red;
}

.content{
  position: relative;
}

.add-to-cart{
  position: absolute;
  right: 30px;
  width: 220px;
  padding:30px;
  font-size: 24px;
}

td, th{
text-align: left;
padding: 8px ;
padding-right: 20px;
}
.cost{
  text-align: right;
}

</style>