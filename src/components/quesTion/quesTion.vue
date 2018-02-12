<style scoped lang="stylus" rel="stylesheet/stylus">
.myQ {
  margin: 42px 15%;
  display: flex;

  .left {
    // width: 100px;
    height: 100%;
    display: flex;
    font-size: 24px;
    color: #e7331b;
    flex-direction: row;

    .left_cont {
      display: flex;

      span {
        display: block;
        width: 37px;
        height: 27px;
        background: url('./jb.png') no-repeat;
        background-size: 100%;
      }

      p {
        margin: 0 30px 0 5px;
      }
    }
  }

  .content {
    width: 1024px;
    color: #000120;

    h2 {
      font-size: 26px;
      margin-bottom: 28px;
    }

    .p1 {
      // width: 100%;
      font-size: 18px;
      line-height: 30px;
    }

    .but {
      display: flex;
      font-size: 14px;
      color: #adadad;

      p {
        font-size: 14px;
        margin: 12px 12px 24px 0;
      }
    }

    .btn1 {
      width: 80px;
      height: 40px;
      background-color: #b3b3b3;
      font-size: 16px;
      color: #fff;
    }

    .fwb {
      margin-bottom: 20px;
    }

    .btn {
      margin-left: 800px;
    }

    .cg {
      display: flex;
      text-align: center;
      justify-content: center;

      .sp1 {
        width: 78px;
        height: 80px;
        display: block;
        background: url('./cg.png') no-repeat;
        background-size: 100%;
        margin-right: 11px;
      }

      .cg2 {
        display: inline-block;
        width: 37px;
        height: 27px;
        background: url('./jb.png') no-repeat;
        background-size: 100%;
      }

      .cg3 {
        color: red;
      }

      .cg4 {
        display: inline-block;
        width: 12px;
        height: 12px;
        background: url('./time.png') no-repeat;
        background-size: 100%;
      }

      .cg5 {
        color: #0099f0;
      }

      .p3 {
        margin-top: 8px;
        font-size: 14px;
        color: #878787;
      }

      h3 {
        font-size: 20px;
        color: #0098f0;
      }

      p {
        font-size: 16px;
        color: #0098f0;
        margin-right: 10px;
      }
    }

    .cg2 {
      display: flex;
      text-align: center;
      justify-content: center;

      .sp2 {
        width: 75px;
        height: 75px;
        display: block;
        background: url('./sb.png') no-repeat;
        background-size: 100%;
        margin-right: 11px;
      }

      .p3 {
        margin-top: 8px;
        font-size: 14px;
        color: #878787;
      }

      p {
        font-size: 20px;
        color: #727272;
        margin-right: 10px;
      }

      .cg4 {
        display: inline-block;
        width: 12px;
        height: 12px;
        background: url('./time.png') no-repeat;
        background-size: 100%;
      }

      .cg5 {
        color: #0099f0;
        margin-right: 10px;
      }
    }
  }

  .info {
    border-radius: 10px;
    line-height: 20px;
    padding: 10px;
    margin: 10px;
    background-color: #ffffff;
  }

  .bad {
    width: 988px;
    padding: 28px;
    background-color: #fff1f1;
    margin: 30px 0;

    .bad_t {
      display: flex;

      span {
        display: block;
        width: 23px;
        height: 23px;
        background: url('./x.png') no-repeat;
        background-size: 100%;
      }

      h2 {
        font-size: 20px;
        color: #e7331b;
        margin-left: 10px;
      }
    }

    .btn3 {
      text-align: center;
      display: flex;
      margin: 0 auto;
      color: #adadad;
    }

    .a_content {
      font-size: 18px;
      line-height: 30px;
    }

    .hideSome {
      word-break: break-all;
      display: -webkit-box;
      -webkit-line-clamp: 5;
      -webkit-box-orient: vertical;
      overflow: hidden;
    }
  }

  .ck {
    width: 988px;
    padding: 28px;
    background-color: #e9e9e9;
    margin: 30px 0;

    .ck_t {
      display: flex;

      span {
        display: block;
        width: 21px;
        height: 25px;
        background: url('./da.png') no-repeat;
        background-size: 100%;
      }

      h2 {
        font-size: 20px;
        color: #000120;
        margin-left: 10px;
      }
    }

    .btn3 {
      text-align: center;
      display: flex;
      margin: 0 auto;
      color: #adadad;
    }

    .a_content {
      font-size: 18px;
      line-height: 30px;
    }

    .hideSome {
      word-break: break-all;
      display: -webkit-box;
      -webkit-line-clamp: 5;
      -webkit-box-orient: vertical;
      overflow: hidden;
    }
  }

  .right {
    display: flex;
    align-items: center;
    margin-left: 40px;
    flex-direction: column;
    justify-content: center;

    .r1 {
      width: 58px;
      height: 58px;
      display: block;
      background: url('./wxz.png') no-repeat;
      background-size: 100%;
    }

    .r2 {
      width: 58px;
      height: 58px;
      display: block;
      background: url('./xz.png') no-repeat;
      background-size: 100%;
    }

    p {
      font-size: 16px;
      color: #3e3e3e;
      margin-top: 18px;
    }
  }
}

.fxh {
  display: flex;
  .fxh_center{
    width: 100%
    .fxh_1{
      display: flex

    }
  }
}
</style>

<template>

  <div class="myQ">
    <div class="hed"></div>
    <div class="left">
      <div class="left_cont">
        <span></span>
        <p>{{integralOrg}}</p>
      </div>
    </div>
    <div class="content">
        <h2>{{question}}</h2>
        <p class="p1">{{description}}</p>
        <div class="but">
          <p>来源:{{source}}</p>
          <p>|</p>
          <p>{{createTime}}</p>
        </div>
        <div class="fwb">
          <div class="components-container">
            <!-- <button @click="getUEContent">获取内容</button> -->
            <div class="editor-container">
              <UE :defaultMsg=defaultMsg :config=config :id=ue1 ref="ue"></UE>
            </div>
        </div>
        </div>
        <div class="btn">
         <el-button type="info" @click="disable()">不会</el-button>
         <el-button type="danger" @click="getUEContent()">提交答案</el-button>
        </div>
        <el-dialog
          :visible.sync="centerDialogVisible"
          width="504px" height="334px"
          center top="20%">
          <div class="cg">
            <span class="sp1"></span>
            <div class="cg1">
             <h3>提交回答成功</h3>
             <p>预计获得<span class="cg2"></span ><span class="cg3">232</span>收益</p>
             <p class="p3"><span class="cg4"></span><span class="cg5">{{time}}s</span>自动跳转到下一题</p>
            </div>
          </div>
          <span slot="footer" class="dialog-footer">
            <!-- <el-button @click="centerDialogVisible = false">取 消</el-button> -->
            <el-button type="primary" @click="centerDialogVisible = false">直接下一题</el-button>
          </span>
        </el-dialog>
        <el-dialog
          :visible.sync="sbVisible"
          width="474px" height="308px"
          center top="20%">
          <div class="cg2">
            <span class="sp2"></span>
            <div class="cg1">
             <p>你的回答内容为空</p>
             <p>不能进行"提交回答"</p>
             <p class="p3"><span class="cg4"></span><span class="cg5">{{time}}s</span>自动跳转当页</p>
            </div>
          </div>

        </el-dialog>
            <el-dialog
          :visible.sync="fxVisible"
          width="571px" height="571px"
          center top="20%"
          font-size="20px"
          title="分享"
         >
        <div class="fxh_center">
          <div class="fxh_1">
            <p>本次你已答题: 67  预计得到收益 <span></span> <span>232</span></p>

        </div>
          <p>辛苦了~快吧你的成绩告诉你的小伙伴吧~</p>
          <div>
            <p>分享到</p>
            <a class="jiathis_button_qzone"></a>
            <a class="jiathis_button_tsina"></a>
            <a class="jiathis_button_tqq"></a>
            <a class="jiathis_button_weixin"></a>
            <a class="jiathis_button_renren"></a>
            <a href="http://www.jiathis.com/share" class="jiathis jiathis_txt jtico jtico_jiathis" target="_blank"></a>
            <a class="jiathis_counter_style"></a>
          </div>
          <input type="text" value="">
          <p>网站分享链接<a href=""></a></p>
          <div>
            <img src="" alt="">
            <img src="" alt="">
          </div>
          <button>分享</button>
        </div>
        </el-dialog>
      <div class="bad">
        <div class="bad_t">
          <span></span>
          <h2>错误回答</h2>
        </div>
        <div :class="isTogel ? 'a_content' : 'a_content hideSome' ">
              {{reference}}
         </div>
         <el-button type="text" @click='detailTogel' class="btn3">{{buttonText}}</el-button>
      </div>
      <div class="ck">
        <div class="ck_t">
          <span></span>
          <h2>参考回答</h2>
        </div>
        <div :class="isTogel2 ? 'a_content' : 'a_content hideSome' ">
              {{reference}}
            </div>
         <el-button type="text" @click='detailTogel2' class="btn3">{{buttonText2}}</el-button>
      </div>
    </div>
    <div class="right">
      <span :class="right?'r1':'r2'" @click="com"></span>
      <p>下一题</p>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
import UE from '../../components/ue/ue.vue';
export default {
  components: { UE },
  data() {
    return {
      defaultMsg: '',
      config: {
        toolbars: [
          ['fullscreen', 'source', 'undo', 'redo', 'bold', 'italic', 'underline', 'fontborder', 'strikethrough', 'superscript', 'subscript', 'removeformat', 'formatmatch', 'autotypeset', 'blockquote', 'pasteplain', '|', 'forecolor', 'backcolor', 'insertorderedlist', 'insertunorderedlist', 'selectall', 'cleardoc'],

        ],
        // initiaFrameWidth: null,
        initialFrameHeight: 300,
        elementPathEnabled: false,
        zIndex:0
      },
      isTogel: false,
      isTogel2: false,
      buttonText: '显示全文',
      buttonText2: '显示全文',
      ue1: "ue1",
      centerDialogVisible: false,
      sbVisible: false,
      right: false,
      answerCount: '',
      anticipatedIncome: '',
      createTime: '',
      description: '',
      integralOrg: '',
      question: '',
      questionId: '',
      reference: '',
      source: '',
      time: 10,
      fxVisible: false
    }
  },
  computed: {
    // editor() {
    //   return this.$refs.myQuillEditor.quill
    // }
  },
  beforeRouteLeave (to, from, next) {
    console.log(to,from)
    // 在当前路由改变，但是该组件被复用时调用
    // 举例来说，对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候，
    // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
    // 可以访问组件实例 `this`
    next()
  },
  created() {
    // 初始化
    this.com()
    this.init()
    localStorage.setItem("question", true);
  },
  beforeRouteLeave (to, from, next) {
    // console.log(to.name)
    if(to.name!='question'){
      localStorage.removeItem('question',true)
    }
    next();
  },

  methods: {
    init: function () {
      let url = 'http://v3.jiathis.com/code/jia.js'
      let script = document.createElement('script')
      script.setAttribute('src', url)
      document.getElementsByTagName('head')[0].appendChild(script)
    },
    com() {
      this.right = !this.right
      this.$indexServer.newQuestion()
        .then((res) => {
          console.log(res)
          if (res.data.code === 200) {
            let data = res.data.data
            console.log(res.data.data)
            this.answerCount = data.answerCount
            this.anticipatedIncome = data.answerCount
            this.createTime = data.createTime
            this.description = data.description
            this.integralOrg = data.integralOrg
            this.question = data.question
            this.questionId = data.questionId
            this.reference = data.reference
            this.source = data.source
            if(this.reference.length<50) {
              this.buttonText = ''
            }


              }
        })
    },
    disable() {
      this.$indexServer.disable(this.questionId)
        .then((res) => {
          if(res.data.code === 200) {
            this.com()
          }
        })

    },
    getUEContent() {

      let content = this.$refs.ue.getPlainTxt(); // 调用子组件方法
      if (content.length > 1) {
        this.centerDialogVisible = true
        this.$refs.ue.remove()
        this.$indexServer.commit(this.questionId, content)
          .then((res) => {
          })
        // this.com()
      } else {
        this.sbVisible = true
      }

      let timer = setInterval(() => {
        this.time--;
        if (this.time <= 0) {
          this.sbVisible = false
          this.centerDialogVisible = false
          this.time = 10;
          clearInterval(timer);
          this.com()
        }
      }, 1000)

      // console.log(typeof content,+content+1)

      // this.$notify({
      //   title: '获取成功，可在控制台查看！',
      //   message: content,
      //   type: 'success'
      // });
    },
    // 显示隐藏按钮
    isShow(n) {
      this.show_a = !this.show_a
    },
    detailTogel() {
      if (this.isTogel === true) {
        this.buttonText = '显示全文'
      } else if (this.isTogel === false) {
        this.buttonText = '收起'
      }
      this.isTogel = !this.isTogel
    },
    detailTogel2() {
      if (this.isTogel2 === true) {
        this.buttonText2 = '显示全文'
      } else if (this.isTogel2 === false) {
        this.buttonText2 = '收起'
      }
      this.isTogel2 = !this.isTogel2
    },
    // onSubmit() {
    //   // 提交
    //   // this.$refs.infoForm.validate，这是表单验证
    //   this.$refs.infoForm.validate((valid) => {
    //     if (valid) {
    //       this.$post('m/add/about/us', this.infoForm).then(res => {
    //         if (res.errCode === 200) {
    //           this.$message({
    //             message: res.errMsg,
    //             type: 'success'
    //           })
    //           this.$router.push('/aboutus/aboutlist')
    //         } else {
    //           this.$message({
    //             message: res.errMsg,
    //             type: 'error'
    //           })
    //         }
    //       })
    //     }
    //   })
    // }
  }
}
</script>

