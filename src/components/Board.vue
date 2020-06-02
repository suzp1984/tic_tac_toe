<template>
  <div class="board">
    <div class="board-edge clearfix">
      <div class="board-bondary">
        <div class="board-body">
          <div class="board-row">
            <square :content="tics[0]" @click.native="OnClicked(0)" />
            <square :content="tics[1]" @click.native="OnClicked(1)" />
            <square :content="tics[2]" @click.native="OnClicked(2)" />
          </div>
          <div class="board-row">
            <square :content="tics[3]" @click.native="OnClicked(3)" />
            <square :content="tics[4]" @click.native="OnClicked(4)" />
            <square :content="tics[5]" @click.native="OnClicked(5)" />
          </div>
          <div class="board-row">
            <square :content="tics[6]" @click.native="OnClicked(6)" />
            <square :content="tics[7]" @click.native="OnClicked(7)" />
            <square :content="tics[8]" @click.native="OnClicked(8)" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Square from "./Square.vue";

export default {
  name: "GameBoard",
  props: {
    tics: Array,
    OnHandleClick: Function
  },
  components: {
    Square
  },
  methods: {
    OnClicked(i) {
      this.OnHandleClick(i);
    }
  }
};
</script>

<style scoped>
</style>

<style scoped>
.board-row {
  clear: both;
  display: table;
}
.board-bondary {
  position: relative;
  float: left;
  left: 50%;
}
.board-body {
  position: relative;
  left: -50%;
}

.clearfix::after {
  content: "";
  display: block;
  height: 0;
  clear: both;
  visibility: hidden;
}
</style>