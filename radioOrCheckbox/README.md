# radioOrCheckbox

> A Vue component
```
传入
    problem    问题
    也可以调用组件的时候使用v-for，传入单一问题
    问题的数据类型：
        {
          id: 1,                          // 问题ID
          type: 1,                        // 问题类型 1:单选 2:多选
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
        },
```
```
监听
    answerOption  参数是当前选择的答案（根据参数，请求数据）
    调用组件获取用户选项的两个方法
    ```javascript
      answer(userAnswer) {
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
    ```
```
