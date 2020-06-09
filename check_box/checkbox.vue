<template>
  <div>
    <div class="check_box_item" v-for="i in listCopy" @change="change(i)">
      <input
        type="checkbox"
        class="input_check center"
        :disabled="disabled"
        :checked="i.checked"
        :id="i.value"
      />
      <label :class="['center',disabled?'disabled': '']" :for="i.value">{{ i.label }}</label>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      listCopy:[...this.list]
    }
  },
  props: {
    selectArr: {
      type: Array,
      default: () => []
    },
    disabled: {
      type: Boolean,
      default: false
    },
    list: {
      type: Array,
      default: () => []
    }
  },
  mounted() {
    this.init()
  },
  methods: {
    change(i) {
      i.checked = !i.checked
      let arr = []
      this.listCopy.map(i => {
        if (i.checked) {
          arr.push(i.value)
        }
      })
      console.log(arr,'点击checkbox框改变 已选数组')
      this.$emit('change', arr)
    },
    init() {
      this.listCopy.length > 0 && this.listCopy.map(i => (i.checked = false))
      if (this.selectArr.length > 0 && this.listCopy.length > 0) {
        this.selectArr.map(i => {
          this.listCopy.map(j => {
            if (i === j.value) {
              j.checked = true
            }
          })
        })
      }
      this.listCopy = [...this.listCopy]
    }
  },
  watch: {
    selectArr: {
      handler: function(newVal) {
        console.log('监听')
        this.init()
      },
      deep: true
    }
  }
}
</script>
<style lang="stylus" scoped>
.check_box_item {
  margin-left: 10px;
  display: inline-block;
  .center {
    display: inline-block;
    vertical-align: middle;
  }

  .center.disabled {
    color: #c0c4cc;
  }
}

input[type=checkbox]:disabled {
  color: #c0c4cc;
  opacity: 0.5;
}

input[type=checkbox] {
  width: 20px;
  height: 20px;
  -webkit-appearance: none;
  background-color: transparent;
  border: 0;
  outline: 0 !important;
  color: #d8d8d8;
  position: relative;
}

input[type=checkbox]:before {
  content: '';
  display: block;
  width: 20px;
  height: 20px;
  border: 2px solid #ddd;
  background-color: #fff;
  box-sizing: border-box;
  border-radius: 3px;
  position: absolute;
  transition: all 0.3s ease;
}

input[type=checkbox]:checked:before {
  content: '';
  display: block;
  width: 20px;
  height: 20px;
  border: 2px solid #D2A47E;
  background-color: #D2A47E;
  box-sizing: border-box;
  border-radius: 3px;
  position: absolute;
}

input[type=checkbox]:checked:after {
  content: '';
  display: block;
  width: 8px;
  height: 15px;
  border-left: 2px solid #fff;
  border-top: 2px solid #fff;
  border-radius: 0.06rem;
  box-sizing: border-box;
  position: absolute;
  transform: rotate(-135deg) translate(-70%, 25%);
}
</style>

