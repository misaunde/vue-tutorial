<template>
  <div class="hello">
    <div class="holder">
      <form @submit.prevent="addSkill">
        <input type="text" placeholder="Enter a skill you have..." v-model="skill" v-validate="'min:4'" name="skill"/>
        
        <transition name="alert-in" enter-active-class="animated flipInX" leave-active-class="animated flipOutX">
          <p class="alert" v-if="errors.has('skill')">{{ errors.first('skill') }}</p>
        </transition>

      </form>

      <ul>
        <draggable v-model="skills">
          <transition-group name="list" enter-active-class="animated bounceInUp">
            <skill-list-element v-for="(data, index) in skills" :key="index" :element="data" :index="index" :onRemove="remove"></skill-list-element>
          </transition-group>
        </draggable>
      </ul>

      <p>These are some skills that you possess.</p>
    </div>
  </div>
</template>

<script>
import Draggable from 'vuedraggable';
import SkillListElement from './Skill.vue';

export default {
  components: {
    Draggable,
    SkillListElement
  },
  name: 'Skills',
  data() {
    return {
      skill: '',
      skills: [
        { skill: "Angular" },
        { skill: "React" } 
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
      console.log("id?: ", id)
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
