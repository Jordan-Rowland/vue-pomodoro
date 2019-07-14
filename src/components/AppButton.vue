<template>
  <div>
    <button
        class="button"
        >{{ text }}</button>
  </div>
</template>

<script>
/* jshint esversion: 9 */
import { value } from 'vue-function-api';

export default {
name: 'AppButton',
props: {
  text: String,
},
setup(props) {


  return {

  };
},

};
</script>

<style scoped>
.button {
  margin: 0 15px;
  height: 3em;
  background-color: #5FBA7D;
  color: white;
  border: none;
  border-radius: 7px;
  width: 105px;
  font-weight: 800;
  box-shadow: none;
  outline: none;
}

.button:hover {
  cursor: pointer;
}
</style>
