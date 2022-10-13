<template>
  <div class="card-style">
    <slot></slot>
  </div>
</template>

<style>
.card-style {
  width: 50rem;
  height: auto;
  margin: 2rem auto;
  border: 2px solid hsla(0, 2%, 20%, 0.212);
  box-shadow: 0 10px 30px hsla(0, 2%, 20%, 0.212);
  padding: 2rem 3rem;
  font-size: 20px;
}
</style>
