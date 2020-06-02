<template>
  <div class="square">{{ content }}</div>
</template>

<script>
export default {
  name: "Square",
  props: {
    content: String
  }
};
</script>

<style scoped>
.square {
  background: #fff;
  border: 2px solid #999;
  float: left;
  font-size: 48px;
  font-weight: bold;
  line-height: 68px;
  width: 68px;
  height: 68px;
  margin-right: -2px;
  margin-top: -2px;
  padding: 0;
  text-align: center;
}
</style>