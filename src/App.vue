<script setup lang="ts">
import { ref, reactive } from 'vue'

type State = {
  count: number
  active: boolean
}

const initialState: State = {
  count: 0,
  active: false,
}

const initStateFunc = () => ( {...initialState})

let stateReactive = reactive<State>({
  ...initialState
})

let stateRef = ref<State>(initStateFunc())

function resetReactiveState() {
  // 2 ways for reactive to reset, each item or whole state using Object.assign
  
  // reactive does not require .value
  stateReactive.active = false
  stateReactive.count = 0

  // reset whole state in reactive, cannot directly reassign like ref
  // Object.assign(stateReactive, initialState)
}

function resetRefState() {
  // 2 ways for ref to reset, each item or whole state using an init state function
  // that destructs the initial state


  // when using refs individual items must use .value
  // stateRef.value.active = false
  // stateRef.value.count = 0

  // reset whole state in ref
  stateRef.value = initStateFunc()
}

</script>

<template>
  <div class="foo">
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

      <v-btn class="mr-2" @click="stateReactive.count++">Increment stateReactive</v-btn>
      <v-switch class="mr-2" v-model="stateReactive.active" color="green" label="reactive" />

      <v-btn @click="resetReactiveState">Reset stateReactive</v-btn>
   
      <div>state 1: {{ stateReactive }}</div>
  
      <v-divider class="my-4"></v-divider>

      <v-btn @click="stateRef.count++">Increment stateRef</v-btn>
      <v-switch v-model="stateRef.active" color="blue" label="stateRef" />
      <v-btn @click="resetRefState">Reset stateRef</v-btn>
      <div>stateRef: {{ stateRef }}</div>
    </div>
</template>

<style scoped>
.foo {
  text-align: center;
}

.bar {
  display: flex;
  justify-content: center;
  flex-direction: column;
  margin-top: 2rem;

}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

</style>
