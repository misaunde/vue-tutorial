<template>
    <li>
        <i class="fa fa-bars" style="float: left; margin-right: 20px;"></i>
        {{ element.skill }}
        <i class="fa fa-minus-circle" style="float: right" @click="onRemove(index)"></i>
    </li>
</template>

<script>

export default {
  props: {
    onRemove: Function,
    element: Object,
    index: Number
  }
}
</script>

<style scoped>
li {
  padding: 20px;
  font-size: 1.3em;
  background-color: #E0EDF4;
  border-left: 5px solid #3EB3F6;
  margin-bottom: 2px;
  color: #3E5252;
}

i {
  cursor: pointer;
}
</style>
