<template>
  <div class="problem-item">
    <h2>{{sequenceNumber}}.{{problem.title}}(多选)</h2>
    <label class="el-checkbox" v-for="(option,index) in problem.items">
        <span class="el_input" :class="isChecked(option.id)">
          <span class="el_checkbox__inner"></span>
          <input type="checkbox" class="checkbox_original" :value="option.id" v-model="answer" :disabled="disable">
        </span>
      <span class="el_label" v-html="option.text"></span>
    </label>
  </div>
</template>

<script type='text/ecmascript-6'>
  export default {
    props: {
      disable: {
        type: Boolean,
        default: false
      },
      sequenceNumber: {
        type: Number,
        default: 1
      },
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
        if (this.answer.indexOf(id) > -1) {
          return 'is-checked'
        } else {
          return ''
        }
      }
    },
    watch: {
      answer(newAnswer) {
        // 向外提交本题目的用户选项和id，便于调用组件的统计
        this.$emit('answerOption', {
          'answer': newAnswer,
          'id': this.problem.id,
          'type': this.problem.type
        })
      }
    }
  }
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">
  .problem-item
    background #ffffff
    padding 0 0.08rem
    h2
      margin 0
      font-size .15rem
      line-height .2rem
      color #000000
      box-sizing border-box
      position relative
      padding 0.08rem 0
      &::after
        content ' '
        position absolute
        left 0
        bottom 0
        right 0
        height 1px
        border-top 1px solid #e6e3e4
        color #e6e3e4
        transform-origin 0 0
        transform scaleY(0.5)
    .el-checkbox
      color: #1f2d3d
      cursor: pointer
      -white-space: nowrap
      position: relative
      display flex
      min-height .45rem
      line-height .45rem
      .el_input
        display inline-block
        white-space: nowrap
        cursor: pointer
        outline: 0
        line-height .45rem
        vertical-align top
        margin-right 0.05rem
        &.is-checked
          .el_checkbox__inner
            background-color: #515359
            border-color: #a9abb6
            &::after
              transform: rotate(45deg) scaleY(1)
        .el_checkbox__inner
          top -0.02rem
          display inline-block
          position relative
          border 1px solid #bfcbd9
          border-radius 4px
          box-sizing: border-box
          width: 18px
          height: 18px
          background-color: #fff
          z-index: 1
          transition: border-color .2s cubic-bezier(.71, -.46, .29, 1.46), background-color .2s cubic-bezier(.71, -.46, .29, 1.46)
          &::after
            box-sizing: content-box
            content: ""
            border: 2px solid #fff
            border-left: 0
            border-top: 0
            height: 8px
            left: 5px
            position: absolute
            top: 1px
            transform: rotate(45deg) scaleY(0)
            width: 4px
            transition: transform .15s cubic-bezier(.71, -.46, .88, .6) .05s
            transform-origin: center
        .checkbox_original
          opacity: 0
          outline: 0
          position: absolute
          margin: 0
          width: 0
          height: 0
          left: -999px
      .el_label
        box-sizing border-box
        font-size .15rem
        white-space normal
        line-height .3rem
        flex 1
</style>
