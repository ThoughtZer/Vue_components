<template>
  <div class="wrapper">
    <h2 v-html="problem.title"></h2>
    <div v-if="problem.type===1">
      <label class="el-radio" v-for="(option,index) in problem.items">
        <span class="el_input" :class="isChecked(option.id)">
          <span class="el_input_inner"></span>
          <input type="radio" class="radio_original" :value="option.id" v-model="answer">
        </span>
        <span class="el_label" v-html="option.text"></span>
      </label>
    </div>
    <div v-if="problem.type===2">
      <label class="el-radio" v-for="(option,index) in problem.items">
        <span class="el_input" :class="isChecked(option.id)">
          <span class="el_checkbox__inner"></span>
          <input type="checkbox" class="checkbox_original" :value="option.id" v-model="answer">
        </span>
        <span class="el_label" v-html="option.text"></span>
      </label>
    </div>
  </div>
</template>

<script type='text/ecmascript-6'>
  export default {
    props: {
      problem: {
        type: Object,
        default: () => {
          return {}
        }
      }
    },
    data() {
      return {
        answer: []
      }
    },
    methods: {
      isChecked(id) {
        if (!this.answer) {
          return
        }
        if (this.problem.type === 1) {
          if (this.answer === id) {
            return 'is-checked'
          } else {
            return ''
          }
        }
        if (this.problem.type === 2) {
          if (this.answer.indexOf(id) > -1) {
            return 'is-checked'
          } else {
            return ''
          }
        }
      }
    },
    watch: {
      answer(newAnswer) {
        // 向外提交本题目的用户选项和id，便于调用组件的统计
        this.$emit('answerOption', {
          'answer': newAnswer,
          'id': this.problem.id
        })
      }
    }
  }
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">
  .wrapper
    .el-radio
      color: #1f2d3d;
      cursor: pointer;
      white-space: nowrap;
      position: relative;
      display: inline-block;
      .el_input
        display inline-block
        white-space: nowrap;
        cursor: pointer;
        outline: 0;
        line-height: 1;
        vertical-align: middle;
        &.is-checked
          .el_input_inner
            border-color: #20a0ff;
            background: #20a0ff;
            &::after
              transform: translate(-50%, -50%) scale(1);
          .el_checkbox__inner
            background-color: #20a0ff;
            border-color: #0190fe;
            &::after
              transform: rotate(45deg) scaleY(1);
        .el_input_inner
          display inline-block
          border: 1px solid #bfcbd9;
          width: 18px;
          height: 18px;
          border-radius: 50%;
          cursor: pointer;
          box-sizing: border-box;
          position: relative
          &::after
            width: 6px;
            height: 6px;
            border-radius: 50%;
            background-color: #fff;
            content: "";
            position: absolute;
            left: 50%;
            top: 50%;
            -ms-transform: translate(-50%, -50%) scale(0);
            transform: translate(-50%, -50%) scale(0);
            transition: transform .15s cubic-bezier(.71, -.46, .88, .6);
        .radio_original
          opacity: 0;
          outline: 0;
          position: absolute;
          z-index: -1;
          top: 0;
          left: 0;
          right: 0;
          bottom: 0;
          margin: 0;
        .el_checkbox__inner
          display: inline-block;
          position: relative;
          border: 1px solid #bfcbd9;
          border-radius: 4px;
          box-sizing: border-box;
          width: 18px;
          height: 18px;
          background-color: #fff;
          z-index: 1;
          transition: border-color .25s cubic-bezier(.71, -.46, .29, 1.46), background-color .25s cubic-bezier(.71, -.46, .29, 1.46);
          &::after
            box-sizing: content-box;
            content: "";
            border: 2px solid #fff;
            border-left: 0;
            border-top: 0;
            height: 8px;
            left: 5px;
            position: absolute;
            top: 1px;
            -ms-transform: rotate(45deg) scaleY(0);
            transform: rotate(45deg) scaleY(0);
            width: 4px;
            transition: transform .15s cubic-bezier(.71, -.46, .88, .6) .05s;
            -ms-transform-origin: center;
            transform-origin: center;
        .checkbox_original
          opacity: 0;
          outline: 0;
          position: absolute;
          margin: 0;
          width: 0;
          height: 0;
          left: -999px;
      .el_label
        font-size: 14px;
        padding-left: 5px;

</style>
