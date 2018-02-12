<template>
  <el-main>
    <!--审核失败-->
    <div class='setRoles'>
      <div class='a_lists' v-for='(item,index) in lists'>
        <!--展开头部-->
        <h1 class='q_title textBig' @click='isShow(index)' v-show='show_a & index === activeIndex'>
          问题:{{item.question}}<span
          class='q_static'>审核失败</span><i class='el-icon-minus up'></i></h1>
        <!--关闭头部-->
        <h1 class='q_title overHiden' @click='isHide(index,item.questionId)' v-show='index !== activeIndex || !show_a'>
          问题:{{item.question}}<i class='el-icon-plus down'></i></h1>
        <!--展开内容-->
        <el-collapse-transition>
          <div v-show='show_a & index === activeIndex'>
            <p class='a_descript'>{{listDetail.description}}</p>
            <div class='income'>悬赏积分<em class=gold></em><a class=goldNum>{{listDetail.integral}}</a>
              <div class='source'>来源：{{listDetail.source}}<span>|</span>{{listDetail.createTime}}</div>
            </div>
            <el-button type="primary" @click='reAnswer (item.questionId)' v-show='!listDetail.hideReanswer'>重新回答
            </el-button>
            <!--我的回答-->
            <div class='myAnswer'>
              <h2 class='a_top'><i class='lamp'></i>我的回答<span class='a_times'>{{myAnswers.createTime}}</span></h2>
              <div :class="isTogel ? 'a_content a_contentX' : 'a_content hideSome a_contentX' "
                   v-html='myAnswers.myAnswer'></div>
              <el-button type="text" @click='detailTogel(index,"x")' v-show='hasTogelX & index === activeIndex'>{{buttonText}}</el-button>
            </div>
            <!--错误回答-->
            <div class='myAnswer errAnswer' v-show='hasErrAnswer' v-for='(val,x) in listDetail.errorList'>
              <h2 class='a_top'><i class='lamp'></i>错误回答<span class='a_times'>{{val.createTime}}</span></h2>
              <div class="a_content a_contentY" v-html='val.errorAnwser'></div>
              <el-button type="text" class='errBtn'>显示全文</el-button>
            </div>
            <!--参考答案-->
            <div class='myAnswer keyAnswer'>
              <h2 class='a_top'><i class='lamp'></i>参考答案</h2>
              <div :class="togelC ? 'a_content a_contentZ' : 'a_content hideSome a_contentZ' "
                   v-html='listDetail.reference'></div>
              <el-button type="text" @click='detailTogel(index,"z")' v-show='hasTogelZ & index === activeIndex'>{{buttonTextC}}</el-button>
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
        buttonText: '显示全文',     //我的回答按钮
        buttonTextB: '显示全文',   //错误回答按钮
        buttonTextC: '显示全文',   //参考答案按钮
        showIndex: 0,
        show_a: false,            //展开头部是否隐藏
        isTogel: false,           //是否需要隐藏全文-我的回答
        togelIndex: '',           //被点击‘显示全文’按钮所属列表index
        togelC: false,            //是否需要隐藏全文-参考答案回答
        lists: '',                //列表-问题
        listsSize: 0,             //列表总条数
        listDetail: '',           //展开列表详情
        pageNum: 1,               //当前列表页数
        pageSize: 20,             //每页显示列表条数
        currentPage: 1,           //点击分页器获取当前页数
        activeIndex: '',          //被点击‘显示全文’按钮所属列表index
        hasTogelX: false, //隐藏我的回答
        hasTogelY: false, //隐藏错误回答
        hasTogelZ: false, //隐藏参考答案
        hasErrAnswer: false,      //是否拥有错误答案
        myAnswers: '',            //我的回答
        paginationHide:false      //是否隐藏
      }
    },
    beforeRouteEnter (to, from, next) {
      next(vm => {
        vm.getDetail(vm.pageNum)
      })
    },
    created () {
    },
    mounted () {
      // 初始化
    },
    methods: {
      // 隐藏‘展开头部’按钮
      isShow (index) {
        this.activeIndex = index
        this.show_a = false
      },
      /*展开列表*/
      isHide (index, questionId) {
        var _this = this
        _this.buttonText = '显示全文'
        _this.buttonTextB = '显示全文'
        _this.buttonTextC = '显示全文'
        let question = questionId
        /*判断是否隐藏全文*/
        _this.$indexServer.failDetailed(question)
          .then((res) => {
            if (res.data.code == 200) {
              _this.listDetail = res.data.data
              _this.myAnswers = _this.listDetail.myAnswer
              _this.show_a = true
              if (_this.listDetail.errorList) {
                _this.hasErrAnswer = true
                var n = _this.listDetail.errorList.length
                _this.$nextTick(() => {                                   //循环通过容器的高判断是否内容超过五行（错误答案，原生写法）
                  var arr = document.getElementsByClassName('a_lists')
                  var errBtns = arr[index].getElementsByClassName('errBtn')
                  var yy = arr[index].getElementsByClassName('a_contentY')
                  for (let i = 0; i < n; i++) {
                    if (yy[i].offsetHeight > 150) {
                      errBtns[i].style.display = 'block'                //超过显示‘显示全文’按钮
                      yy[i].classList.add("hideSome")
                      errBtns[i].onclick = function () {                //按钮操作全文显隐
                        if (yy[i].classList.contains('hideSome') == true) {
                          yy[i].classList.remove("hideSome")
                          this.innerHTML = '收起'
                        }
                        else {
                          yy[i].classList.add("hideSome")
                          this.innerHTML = '显示全文'
                        }
                      }
                    }
                    else {
                      errBtns[i].style.display = 'none'
                      yy[i].classList.remove("hideSome")
                    }
                  }
                })
              }
              _this.activeIndex = index                       //判断我的回答和参考答案（同上）
              _this.isTogel = true
              _this.togelC = true
              _this.$nextTick(function () {
                var arr = document.getElementsByClassName('a_lists')
                var xx = arr[index].getElementsByClassName('a_contentX')[0].offsetHeight;
                var zz = arr[index].getElementsByClassName('a_contentZ')[0].offsetHeight;
                if (xx > 150) {             //我的回答
                  _this.isTogel = false
                  _this.hasTogelX = true
                }else {
                  _this.isTogel = true
                  _this.hasTogelX = false
                }
                if (zz > 150) {             //参考答案
                  _this.togelC = false      //添加hideSome
                  _this.hasTogelZ = true
                }else {
                  _this.togelC = true
                  _this.hasTogelZ = false
                }
              })
            } else if (res.data.code == 400) {
              _this.open7('登录超时，请重新登录！')
            } else if (res.data.code == 401) {
              _this.open8('您的参数有误！')
            } else if (res.data.code == 402) {
              _this.open8('该题已下架！')
            } else if (res.data.code == 406) {
              _this.open8('该题已被别人获取！')
            }
          })
      },
//      点击按钮操作，x-我的回答，z-参考答案
      detailTogel (n, m) {
        this.togelIndex = n
        if (m === 'x') {
          this.isTogel = !this.isTogel
          if (this.isTogel === true && this.togelIndex === n) {
            this.buttonText = '收起'
          } else if (this.isTogel === false && this.togelIndex === n) {
            this.buttonText = '显示全文'
          }
          return
        } else if (m === 'z') {
          this.togelC = !this.togelC
          if (this.togelC === true && this.togelIndex === n) {
            this.buttonTextC = '收起'
          } else if (this.togelC === false && this.togelIndex === n) {
            this.buttonTextC = '显示全文'
          }
        }
        return
      },
      /*获取列表数据*/
      getDetail (n) {
        var _this = this
        _this.$indexServer.auditFailure(n, _this.pageSize)
          .then((res) => {
            if (res.data.code == 200) {
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
            } else if (res.data.code == 401) {
              _this.open8('您的参数有误！')
            } else if (res.data.code == 402) {
              _this.open8('该题已下架！')
            } else if (res.data.code == 406) {
              _this.open8('该题已被别人获取！')
            }else if (res.data.code == 40011) {
              _this.open7('账号被冻结，请联系管理员！')
            }
          })
      },
      // 重新回答
      reAnswer (id) {
        this.$router.push({name: 'question', query: {id: id}});
      },
      // 分页器
      handleSizeChange: function (size) {
        this.pagesize = size;
      },
      /*点击分页器*/
      handleCurrentChange: function (currentPage) {
        this.currentPage = currentPage;
        this.pageNum = this.currentPage;
        this.getDetail(this.pageNum)
      },
      /*错误提示弹框,并返回首页*/
      open7(str) {
        var _this = this
        _this.$message({
          showClose: true,
          message: str,
          type: 'warning',
          duration: 2000,
          onClose: function () {
            _this.$router.push({
              path: '/Login'
            })
          }
        });
      },
      /*错误提示弹框*/
      open8(n) {
        var _this = this
        _this.$message({
          showClose: true,
          message: n,
          type: 'warning',
          duration: 3000,
        });
      }
    }
  }
</script>
<style scoped lang="stylus" rel="stylesheet/stylus"></style>
