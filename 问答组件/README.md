### 组件使用方法

传入

 - problem（问题对象）
 - sequenceNumber （问题序号）
 - disable  （可操作与否）

监听

 - answerOption （答案监听）

    ```
      问题的数据类型：
        {
          id: 1,                          // 问题ID
          type: 1,                        // 问题类型 1:单选 2:多选 3:主观
          title: '这是第一道单项选择题目',    // 题目文本
          items: [                        // 选项内容
            {
              id: 1,
              text: '选项一'
            },
            {
              id: 2,
              text: '选项二'
            },
            {
              id: 3,
              text: '选项三'
            },
            {
              id: 4,
              text: '选项四'
            }
          ]
        }
    ```

父组件监听answerOption事件

    getAnswer(userAnswer) {
        let aIndex = this._findIndex(this.user_answer, userAnswer)
        if (aIndex <= -1) {
          this.user_answer.push(userAnswer)
        } else {
          this.user_answer.splice(aIndex, 1, userAnswer)
        }
        console.log(this.user_answer)   // 最终的答案数组
      },
      _findIndex(arr, option) {
        return arr.findIndex((item) => {
          return item.id === option.id
        })
      }

最终：

  - 单选是 一个 选项id
  - 多选是 多个 选项id组成的数组
  - 主观题 一个 字符串



#### 注意

   这三个组件可合并成一个组件通过类型判断显示
