<template>
  <div class="problem-item">
    <h2>{{sequenceNumber}}.{{problem.title}}</h2>
    <div class="text-wrapper">
      <textarea class="text"
                v-model="answer"
                :disabled="disable"
                placeholder="请输入您的答案"
      ></textarea>
    </div>
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
        answer: ''
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
    .text-wrapper
      .text
        outline none
        border none
        background-color #f2f2f2
        width 100%
        height 1.5rem
        resize none
        box-sizing border-box
        padding 0.15rem 0.15rem .1rem
        border-radius 4px
        font-size .12rem
        line-height .2rem
        margin-bottom .1rem
</style>
