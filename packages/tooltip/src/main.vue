<template>
  <div
    class="el-tooltip"
    @mouseenter="handleShowPopper"
    @mouseleave="handleClosePopper">
    <div class="el-tooltip__rel" ref="reference">
      <slot></slot>
    </div>

    <transition :name="transition">
      <div
        class="el-tooltip__popper"
        :class="['is-' + effect]"
        ref="popper"
        v-show="!disabled && showPopper">
        <slot name="content"><div v-text="content"></div></slot>
      </div>
    </transition>
  </div>
</template>

<script>
import Popper from 'main/utils/vue-popper';

export default {
  name: 'el-tooltip',

  mixins: [Popper],

  props: {
    openDelay: {
      type: Number,
      default: 0
    },
    disabled: Boolean,
    effect: {
      type: String,
      default: 'dark'
    },
    content: String,
    visibleArrow: {
      default: true
    },
    transition: {
      type: String,
      default: 'fade-in-linear'
    },
    options: {
      default() {
        return {
          boundariesPadding: 10,
          gpuAcceleration: false
        };
      }
    }
  },

  methods: {
    handleShowPopper() {
      this.timeout = setTimeout(() => {
        this.showPopper = true;
      }, this.openDelay);
    },

    handleClosePopper() {
      clearTimeout(this.timeout);
      this.showPopper = false;
    }
  }
};
</script>
