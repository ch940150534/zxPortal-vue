<template>
  <div id="myHeader">
    <nav class="navbar navbar-static-top" :style="{'left':-scroll+'px'}">
      <div class="container">
        <a class="navbar-brand" :href="baseUrl+'/'"></a>
        <ul class="navbar-list">
          <li class="col" v-for="(item,index) in navlist" :key="index">
            <a :href="(item.url.startsWith('/'))?baseUrl+item.url:item.url" :class="{'selected':selected==index}">{{item.name}}</a>
          </li>
          <li class="col col-input v-outter-table">
            <form method="GET" :action="baseUrl+'/s'" class="v-table-cell">
              <input type="hidden" value="article" name="m">
              <el-input id="js-input-search" placeholder="搜索" name="k">
                <el-button id="js-btn-search" slot="append" icon="el-icon-search" native-type="submit"></el-button>
              </el-input>
            </form>
          </li>
          <li class="col navbar-translate">
            <span><a @click.prevent="setCookieLanguage('en')">En</a></span>
            <span>/</span>
            <span><a @click.prevent="setCookieLanguage('zh-CN')">中</a></span>
          </li>
        </ul>
      </div>
    </nav>
  </div>
</template>

<script>
  export default {
    name: 'myHeader',
    props: ['selected'],
    data () {
      return {
        scroll: '',
        navlist: [
          {
            url: '/',
            name: '首页'
          },
          {
            url: '/article-solve-1.html',
            name: '解决方案'
          },
          {
            url: 'http://d.zxzx119.com/',
            name: '企业名录'
          },
          {
            url: '//app.zxzx119.com/',
            name: '教育培训'
          },
          {
            url: 'http://e.zxzx119.com/',
            name: '第三方审图'
          },
          {
            url: '/article-encyclop-1.html',
            name: '中消百科'
          },
          {
            url: '/119',
            name: '紧急呼叫119'
          }
        ]
      }
    },
    methods: {
      fixedScrollX () {
        this.scroll = document.documentElement.scrollLeft || document.body.scrollLeft
      },
      setCookieLanguage (type) {
        var d = new Date()
        d.setHours(d.getHours() + (1)) // 保存一个小时
        document.cookie = 'lang=' + type + '; expires=' + d.toGMTString()
        window.location.reload()
      }

    },
    mounted: function () {
      window.addEventListener('scroll', this.fixedScrollX)
    }
  }
</script>

<style lang="scss">
  #myHeader {
    $header-bgcolor: #c41335;
    & + * {
      margin-top: 75px;
    }
    .el-input .el-input__inner {
      border-radius: 20px 0 0 20px;
    }
    .el-input .el-input-group__append {
      border-radius: 0 20px 20px 0;
    }
    li {
      list-style: none;
    }
    .container {
      margin-right: auto;
      margin-left: auto;
    }
    .navbar {
      position: fixed;
      top: 0;
      margin-bottom: 20px;
      background-color: $header-bgcolor;
      height: 75px;
      background-size: 100%;
      min-width: 1200px;
      width: 100%;
    }
    .navbar-static-top {
      z-index: 99999;
      border-width: 0 0 1px;
    }
    .navbar-brand {
      float: left;
      margin: 10px 35px 0 0;
      width: 100px;
      height: 85px;
      background-image: url("../images/logo.png");
      background-size: 100%;
      background-repeat: no-repeat;
    }
    .navbar-list {
      overflow: hidden;
    }
    .col {
      //height: px;
      float: left;
      line-height: 80px;
      text-align: center;
      font-size: 18px;
      & > a {
        display: block;
        height: 75px;
        padding: 0 15px;
        color: #fff;
      }
      & > a:hover {
        color: #ddd;
      }
    }
    .selected {
      background-color: #82051d;
    }
    .col-input {
      height: 75px;
      .el-input-group {
        display: table; //inline-table使元素产生5个额外空白像素
        button {
          margin: -13px -20px; // 解决IE中icon不剧中问题
        }
      }
      form {
        height: 45px;
      }
      margin: {
        left: 65px;
        right: 8px;
      }
    ;
      width: 175px;
    }
    .navbar-translate {
      color: #fff;
      font-size: 14px;
      line-height: 95px;
      a {
        color: #fff;
      }
      a:hover {
        text-decoration: underline;
      }
    }
  }
</style>
