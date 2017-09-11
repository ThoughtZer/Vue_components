<template>
  <div class="pagination-wrapper">
    <ul class="pagination">
      <li v-show="current !== 1" @click="goto(1)"><a>首页</a></li>
      <li v-show="current !== 1" @click="goto(current,'decrease')"><a>上一页</a></li>
      <li v-for="index in pages" @click="goto(index)" :class="{'active':current == index}" :key="index">
        <a>{{index}}</a>
      </li>
      <li v-show="allpage != current && allpage !== 0 " @click=" goto(current,'add')"><a>下一页</a></li>
      <li v-show="allpage != current && allpage !== 0 " @click="goto(allpage)"><a>尾页</a></li>
    </ul>
  </div>
</template>

<script type='text/ecmascript-6'>
  export default {
    props: {
      showItem: {
        type: Number,
        default: 5,
      },
      allpage: {
        type: Number,
        default: 15,
      }
    },
    data: function () {
      return {
        current: 1
      }
    },
    computed: {
      pages: function () {
        let pag = [];
        let center = Math.floor(this.showItem / 2) + 1;
        if (this.current < center) {
          let i = Math.min(this.showItem, this.allpage);
          while (i) {
            pag.unshift(i--);
          }
        } else {
          let middle = this.current - Math.floor(this.showItem / 2);//从哪里开始
          let i = this.showItem;
          if (middle > (this.allpage - this.showItem / 2)) {
            middle = (this.allpage - this.showItem /2) + 1;
          }
          while (i--) {
            pag.push(middle++);
          }
        }
        return pag
      }
    },
    methods: {
      goto: function (index, type) {
        if (type === 'decrease') {
          this.current--;
        } else if (type === 'add') {
          this.current++;
        } else {
          this.current = index;
        }
        this.$emit('currentPage', this.current);//向外部提交当前页码。由外部请求数据,保证子组件的'干净'
      }
    }
  }
</script>

<style scoped>

  li {
    list-style: none;
  }

  a {
    text-decoration: none;
  }

  .pagination {
    position: relative;

  }

  .pagination li {
    display: inline-block;
    margin: 0 5px;
  }

  .pagination li a {
    padding: .5rem 1rem;
    display: inline-block;
    border: 1px solid #ddd;
    background: #fff;
    cursor: pointer;
    color: #0E90D2;
  }

  .pagination li a:hover {
    background: #eee;
  }

  .pagination li.active a {
    background: #0E90D2;
    color: #fff;
  }
</style>
