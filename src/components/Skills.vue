<template>
  <div class="hello">
    <div class="holder">
      <form @submit.prevent="addSkill">
        <input type="text" placeholder="Enter a skill you have..." v-model="skill" v-validate="'min:4'" name="skill"/>
        
        <transition name="alert-in" enter-active-class="animated flipInX" leave-active-class="animated flipOutX">
          <p class="alert" v-if="errors.has('skill')">{{ errors.first('skill') }}</p>
        </transition>

      </form>

      <!-- <ul>
        <transition-group name="list" enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown">
          <li v-for="(data, index) in skills" :key='index'>
            {{ data.skill }}
            <i class="fa fa-minus-circle" v-on:click="remove(index)"></i>
          </li>
        </transition-group>
      </ul> -->

      <ul>
        <draggable v-model="skills">
          <transition-group name="list" enter-active-class="animated bounceInUp">
            <li v-for="(data, index) in skills" :key='index'>
              <i class="fa fa-bars" style="float: left; margin-right: 20px;"></i>
              {{ data.skill }}
              <i class="fa fa-minus-circle" style="float: right" v-on:click="remove(index)"></i>
            </li>
          </transition-group>
        </draggable>
      </ul>

      <p>These are some skills that you possess.</p>
    </div>
  </div>
</template>

<script>
import draggable from 'vuedraggable';

export default {
  components: {
    draggable
  },
  name: 'Skills',
  data() {
    return {
      skill: '',
      skills: [
        { skill: "Angular"},
        { skill: "React"} 
      ],
    }
  },
  methods: {
    addSkill() {
      this.$validator.validateAll().then( res => {
        if (res) {
          this.skills.push({skill: this.skill});
          this.skill = '';
        } else {
          /* eslint-disable no-console */
          console.log("Not valid");
          /* eslint-enable no-console */
        }
      })
    },
    remove(id) {
      this.skills.splice(id, 1);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<!-- Can also do: src="./Skills.css" -->
<style scoped>
@import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";
@import "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css";

.holder {
  background: #fff
}

ul {
  margin: 0;
  padding: 0;
  list-style-type: none;
}

ul li {
  padding: 20px;
  font-size: 1.3em;
  background-color: #E0EDF4;
  border-left: 5px solid #3EB3F6;
  margin-bottom: 2px;
  color: #3E5252;
}

p {
  text-align: center;
  padding: 30px 0;
  color: gray;
}

.container {
  box-shadow: 0px 0px 40px lightgray;
}

input {
  width: calc(100% - 40px);
  border: 0;
  padding: 20px;
  font-size: 1.3em;
  background-color: #323333;
  color: #687f7f;
}

.alert {
  background: #fdf2ce;
  font-weight: bold;
  padding: 5px;
  margin: 0px;
}

i {
  
  cursor: pointer;
}



/* .alert-in-enter-active {
  animation: bounce-in .5s;
}

.alert-in-leave-active {
  animation: bounce-in .5s reverse;
}

@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.05);
  }
  100% {
    transform: scale(1);
  }
} */



</style>
