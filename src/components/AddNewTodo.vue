<template>
  <div class="addnew" @click="$emit('addnew')">
    <p>+</p>
  </div>
</template>
<script>
export default {};
</script>
<style lang="scss">
.addnew {
  cursor: pointer;
  margin: 50px;
  width: 200px;
  height: 340px;
  background-color: red;
  display: flex;
  justify-content: center;
  align-items: center;
  & p {
    font-size: 100px;
  }
}
</style>