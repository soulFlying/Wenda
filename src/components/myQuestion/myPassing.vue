<template>
  <el-main>
    <!--审核通过-->
  <div class='passingCheck'>
    <div class='a_lists'  v-for='(item,index) in lists'>
      <!--展开头部-->
      <h1 class='q_title textBig' @click='isShow(index)' v-show='show_a & index === activeIndex'>
        <div class='gainGold' v-show='show_a'>获得：<em class='goldBig'></em><a>{{item.integralGain}}</a></div>问题:{{item.question}}<span
        class='q_static'>审核成功</span><i class='el-icon-minus up'></i></h1>
      <!--关闭头部-->
      <h1 class='q_title overHiden' @click='isHide(index)' v-show='index !== activeIndex || !show_a'>问题:{{item.question}}<i class='el-icon-plus down'></i></h1>
      <!--展开内容-->
      <el-collapse-transition>
        <div v-show='show_a & index === activeIndex'>
          <p class='a_descript'>{{item.description}}</p>
          <div class='income'>悬赏积分：<em class=gold></em><a class=goldNum>{{item.integralOrg}}</a>
            <div class='source'>来源：{{item.source}}<span>|</span>{{year(item.createTime)}}</div>
          </div>
          <div class='myAnswer'>
            <h2 class='a_top'><i class='lamp'></i>我的回答<a class='corrected' v-show="item.isModify==1">{{error(item.isModify)}}</a><span class='a_times'>{{item.createTime}}</span>
            </h2>
            <div :class="isTogel ? 'a_content' : 'a_content hideSome' " v-html='item.answer'></div>
            <el-button type="text" @click='detailTogel(index)' v-show='hasTogel & index === activeIndex'>{{buttonText}}</el-button>
          </div>
        </div>
      </el-collapse-transition>
    </div>
  </div>
    <!--分页-->
    <div class="block" v-show='paginationHide'>
      <el-pagination layout="prev, pager, next" :total='listsSize' :page-size='pageSize'
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
        buttonText: '显示全文',          //按钮
        buttonTextB: '显示全文',
        buttonTextC: '显示全文',
        showIndex: 0,
        show_a: false,                  //展开头部是否隐藏
        isTogel: false,                //是否隐藏全文
        togelIndex: '',               //被点击按钮index
        lists: '',                   //列表数据
        pageNum: 1,                  //获取数据页
        pageSize: 20,               //每页显示的总数
        currentPage: 1,            //当前页
        activeIndex:'',           //被展开列表index
        hasTogel: false,         //按钮是否隐藏
        listsSize: 0,           //列表总条数
        paginationHide:false   //分页器是否隐藏
      }
    },
    beforeRouteEnter (to, from, next) {
      next(vm => {
        vm.getDetail(vm.pageNum)  //获取列表数据
      })
    },
    mounted () {
      // 初始化
    },
    methods: {
      //时间处理（时间戳转化为日期格式）
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
      //年月日的处理
      year (yy) {
       return yy.split(' ')[0];
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
      //展开列表
      isHide (index) {
        var _this = this
        _this.activeIndex = index
        _this.show_a = true
        _this.isTogel = true
        _this.buttonText = '显示全文'
        var arr = document.getElementsByClassName('a_lists')
        _this.$nextTick(function () {
          var hh = arr[index].getElementsByClassName('a_content')[0].offsetHeight;
          if (hh > 150) {
            _this.isTogel = false
            _this.hasTogel = true
          }
          else {
            _this.hasTogel = false
            _this.isTogel = true
          }
        })
      },
      //全文显示按钮
      detailTogel (n) {
        this.togelIndex = n
        this.isTogel = !this.isTogel
        if (this.isTogel === true && this.togelIndex === n) {
          this.buttonText = '收起'
        } else if (this.isTogel === false  && this.togelIndex === n) {
          this.buttonText = '显示全文'
        }
      },
      //获取列表数据
      getDetail (n) {
        var _this = this
        this.$indexServer.auditSuccess(n,_this.pageSize)
          .then((res)=>{
            if(res.data.code == 200){
              _this.lists = res.data.data
              _this.listsSize = res.data.total
              if (_this.listsSize > 0) {
                _this.paginationHide = true
              }
              else {
                _this.paginationHide = false
              }
            } else if (res.data.code == 400) {
              _this.open7('登录超时，请重新登录！')
            }else if (res.data.code == 40011) {
              _this.open7('账号被冻结，请联系管理员！')
            }
          })
      },
      // 分页器
      handleSizeChange: function (size) {
        this.pagesize = size;
      },
      //当前页
      handleCurrentChange: function(currentPage){
        this.currentPage = currentPage;
        this.pageNum = this.currentPage;
        this.getDetail(this.pageNum)
      },
      //错误提示弹框
      open7(str) {
        var _this = this
        _this.$message({
          showClose: true,
          message: str,
          type: 'warning',
          duration:2000,
          onClose: function () {
            _this.$router.push({
              path: '/Login'
            })
          }
        });
      },
      //平台纠错
      error(x){
          if (x == 0) {

          }
          else if (x == 1) {
              return '平台纠错'
          }
      }
    }
  }
</script>
<style scoped lang="stylus" rel="stylesheet/stylus"></style>
