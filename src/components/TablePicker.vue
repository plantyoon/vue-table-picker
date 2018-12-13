<template>
  <div class="select-grid">
    <div class="row-by-col">
      <div class="grid-by-number"
        @click.stop="toggle">{{ current_column + ' x ' + current_row }}</div>
      <div class="grid-row-col"
        :class="{ visible }"
        @click="setCurrentIndex">
        <div class="grid-row"
          v-for="r_index in rows"
          :key="`grid-row-${ r_index }`">
          <div class="grid-column"
            v-for="c_index in columns"
            :key="`grid-column-${ c_index }`"
            :class="{ fill: current_column >= c_index && current_row >= r_index }"
            @mouseenter="checkCurrentIndex(c_index, r_index)">
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const mComp = (v, m) => Math.max(m, v);

export default {
  props: {
    columns: {
      type: Number,
      default: 2
    },
    rows: {
      type: Number,
      default: 2
    },
    minColumns: {
      type: Number,
      default: 1
    },
    minRows: {
      type: Number,
      default: 1
    },
    minSize: {
      type: Number,
      default: 1,
    },
    x: {
      type: Number,
      default: 0
    },
    y: {
      type: Number,
      default: 0
    },
    value: {
      type: Number,
      default: 0
    },
  },
  mounted() {
    this.$emit('mounted', this);
  },
  data() {
    return {
      current_index: 0,
      current_column: this.x,
      current_row: this.y,
      visible: false,
    }
  },
  methods: {
    init() {
      this.current_column = this.x;
      this.current_row = this.y;
    },
    checkCurrentIndex(x, y) {
      if (x * y < this.minSize) return;
      this.current_column = mComp(x, this.min_columns);
      this.current_row = mComp(y, this.min_rows);
    },
    setCurrentIndex() {
      this.visible = false;
      const x = this.current_column;
      const y = this.current_row;
      this.$emit('change', { x, y });
    },
    toggle() {
      this.visible = !this.visible; 
      this.init();
    }
  }
}
</script>

<style lang="scss">
.select-grid {
  cursor: pointer;
  display: inline-block;
  margin-top: 10px;

  .row-by-col {
    display: inline-block;
    font-size: 14px;
    line-height: 14px;
    text-align: center;
    border: 1px solid #ccc;
    border-radius: 2px;

    &:hover {
      background-color: darken(white, 2);
    }
  }
}
.grid-row-col {
  display: none;
  z-index: 5;
  line-height: 0;
  padding: 5px;
  background: #e5e5e5;
  position: absolute;
  transform: translate(65px, -30px);
}
.grid-row-col:before{
  content: '';
  position: absolute;
  width: 13px;
  height: 13px;
  background-color: #e5e5e5;
  display: inline-block;
  transform: translate(-50%, 70%) rotate(45deg);
  top: 0;
  margin: 0 auto;
  left: 0;
}
.grid-column {
  position: relative;
  display: inline-block;
  border: 1px solid #ccc;
  background: white;
  margin: 2px;
  width: 11px;
  height: 11px;

  &.fill {
    background: rgb(38, 172, 206);
    border: 1px solid rgb(24, 152, 202);
  }
}
.visible {
  display: inline-block;
}
</style>

