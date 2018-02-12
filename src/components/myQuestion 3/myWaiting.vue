<template>
  <el-main>
    <div class='waitCheck'>
      <div class='a_lists' v-for='(item,index) in lists' ref='lists'>
        <h1 class='q_title textBig' @click='isShow(index)' v-show='show_a & index === activeIndex'>{{item.question}}<span
          class='q_static'>待审核</span><i class='el-icon-minus up'></i></h1>
        <h1 class='q_title overHiden' @click='isHide(index)' v-show='index !== activeIndex || !show_a'>{{item.question}}<i class='el-icon-plus down'></i></h1>
        <el-collapse-transition>
          <div v-show='show_a & index === activeIndex'>
            <p class='a_descript'>{{item.description}}</p>
            <div class='income'>悬赏积分<em class=gold></em><a class=goldNum>{{item.integralOrg}}</a>
              <div class='source'>来源：{{source (item.source)}}<span>|</span>{{year(item.createTime)}}</div>
            </div>
            <div class='myAnswer'>
              <h2 class='a_top'><i class='lamp'></i>我的回答<span class='a_times'>{{getLocalTime(item.createTime)}}</span></h2>
              <div :class="isTogel ? 'a_content' : 'a_content hideSome' ">{{item.answer}}</div>
              <el-button type="text" @click='detailTogel(index)'>{{buttonText}}</el-button>
            </div>
          </div>
        </el-collapse-transition>
      </div>
    </div>
    <!--分页-->
    <div class="block">
      <el-pagination layout="prev, pager, next" :total=lists.length :page-size='pageSize'
                     @current-change="handleCurrentChange" :current-page='currentPage'
                     @size-change="handleSizeChange"></el-pagination>
    </div>
  </el-main>
</template>

<script>
  export default {
    data () {
      return {
        activeNames: ['1'],
        buttonText: '显示全文',
        buttonTextB: '显示全文',
        buttonTextC: '显示全文',
        showIndex: 0,
        show_a: false,
        isTogel: false,
        togelIndex: '',
        lists: '',
        pageNum:1,
        pageSize: 20,
        currentPage: 1,
        activeIndex:'',
      }
    },
    mounted () {
      // 初始化
      var _this = this
      _this.getDetail()
      /*_this.isFold()*/
    },
    methods: {
      //时间处理
      add0(m){
        return m<10?'0'+m:m
      },
      getLocalTime(nS) {
        var time = new Date(nS);
        var y = time.getFullYear();
        var m = time.getMonth()+1;
        var d = time.getDate();
        var h = time.getHours();
        var mm = time.getMinutes();
        var s = time.getSeconds();
        return y+'-'+this.add0(m)+'-'+this.add0(d)+' '+this.add0(h)+':'+this.add0(mm)+':'+this.add0(s);
      },
      year (yy) {
        this.getLocalTime(yy).slice(' ')[0];
      },
      //source来源
      source (n) {
        if (n===0) {
          return '百度知道'
        }
        else if(n===1){
          return '马蜂窝'
        }
        else if(n===2){
          return '携程问答'
        }
        else if(n===3){
          return '途牛问答'
        }
        else if(n===4){
          return '后台录入'
        }
      },
      // 显示隐藏按钮
      isShow (index) {
        this.activeIndex = index
        this.show_a = false
      },
      isHide (index) {
        this.activeIndex = index
        this.show_a = true
      },
      detailTogel (n) {
        this.togelIndex = n
        if (this.isTogel === true && this.togelIndex === n) {
          this.buttonText = '显示全文'
        } else if (this.isTogel === false  && this.togelIndex === n) {
          this.buttonText = '收起'
        }
        this.isTogel = !this.isTogel
      },
      getDetail () {
          var _this = this
        this.$indexServer.nonChecked(_this.pageNum,_this.pageSize)
          .then((res)=>{
            if(res.data.code == 200){
              _this.lists = res.data.data.list
            }
            _this.isFold()
          })
      },
      //判断显示全文按钮是否隐藏
      isFold () {
        var _this = this
        _this.$nextTick(function () {
          var arr = document.getElementsByClassName('a_lists')
          for(var i=0;i<arr.length;i++){
            console.log(arr[i].getElementsByClassName('a_content'));
            console.log(arr[i].getElementsByClassName('a_content').style.height);
          }
        })
      },
      // 分页器
      handleSizeChange: function (size) {
       /* this.pagesize = size;*/
      },
      handleCurrentChange: function(currentPage){
        this.currentPage = currentPage;
        console.log(this.currentPage);
        this.pageNum = this.currentPage;
        this.getDetail()
      }
    },
    components: {}
  }
</script>
<style scoped lang="stylus" rel="stylesheet/stylus"></style>
