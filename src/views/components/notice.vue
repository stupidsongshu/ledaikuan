 <template>
    <div class="swiper-container notice-swiper-container">
        <div class="swiper-wrapper">
            <div class="swiper-slide phone-item" v-for="(user, index) in list" :key="index">
                {{user.phone}}成功借款{{user.amount}}元用于{{user.purpose}}消费
            </div>
        </div>
    </div>
</template>

<script type="text/ecmascript-6">
  import Swiper from 'swiper'
  import 'swiper/dist/css/swiper.css'

  export default {
    data() {
      return {
        phonePrefixArr: [134, 135, 136, 137, 138, 139, 147, 148, 150, 151, 152, 157, 158, 159, 172, 178, 182, 183, 184, 187, 188, 198, 130, 131, 132, 145, 146, 155, 156, 166, 171, 175, 176, 185, 186, 133, 149, 153, 173, 174, 177, 180, 181, 189, 199, 170],
        loanPurpose: ['装修', '婚庆', '旅游', '教育', '租房', '汽车周边', '电子数码产品', '医疗', '家用电器', '家具家居'],
        list: [],
        phoneArray: [],
        ammountArray: [],
        phoneArr: []
      }
    },
    mounted() {
        this.swiperInit()
    },
    created() {
      /*
        三大运营商最新号段 合作版
        移动号段:
          134 135 136 137 138 139 147 148 150 151 152 157 158 159 172 178 182 183 184 187 188 198
        联通号段:
          130 131 132 145 146 155 156 166 171 175 176 185 186
        电信号段:
          133 149 153 173 174 177 180 181 189 199
        虚拟运营商:
          170
      */
      // const LOAN_LIMIT_MIN = 500
      // const LOAN_LIMIT_MAX = 20000

      // let prefixArr = [134, 135, 136, 137, 138, 139, 147, 148, 150, 151, 152, 157, 158, 159, 172, 178, 182, 183, 184, 187, 188, 198, 130, 131, 132, 145, 146, 155, 156, 166, 171, 175, 176, 185, 186, 133, 149, 153, 173, 174, 177, 180, 181, 189, 199, 170]
      // let loanNuArr = [500, 1000, 2000, 3000, 4000, 5000, 6000, 8000, 10000, 12000, 15000, 18000, 20000]
      // // 生成手机号
      // let generateNumber = function() {
      //   // 前3位
      //   let prefix = prefixArr[parseInt(Math.random() * prefixArr.length)]
      //   // 后4位
      //   let postfix = (() => {
      //     let tmp = (parseInt(Math.random() * 10000)).toString()
      //     while (tmp.length < 4) {
      //       tmp = '0' + tmp
      //     }
      //     return tmp
      //   })()
      //   return prefix + '****' + postfix
      // }
      // // 贷款额度
      // let generateAmount = () => {
      //   // var tmp = parseInt(Math.random() * ((LOAN_LIMIT_MAX - LOAN_LIMIT_MIN) / 100 + 1))
      //
      //   // var tmp = parseInt(Math.random() * (LOAN_LIMIT_MAX / LOAN_LIMIT_MIN) + 1)
      //   // return tmp * 500 + LOAN_LIMIT_MIN
      //
      //   return loanNuArr[parseInt(Math.random() * loanNuArr.length)]
      // }
      //
      // for (var i = 0; i < 15; i++) {
      //   this.phoneArr.push({
      //     id: i,
      //     number: generateNumber(),
      //     amount: generateAmount()
      //   })
      // }

      // 生成50个手机号码
      for (var i = 0; i < 50; i++) {
        var prefixNo = Math.floor(Math.random() * 46)
        var last1 = Math.floor(Math.random() * 10)
        var last2 = Math.floor(Math.random() * 10)
        var last3 = Math.floor(Math.random() * 10)
        var last4 = Math.floor(Math.random() * 10)
        var phone = this.phonePrefixArr[prefixNo] + '****' + last1 + last2 + last3 + last4
        var amount = Math.round((Math.random() * 10) + 1) * 1500

        var purpose = this.loanPurpose[Math.floor(Math.random() * this.loanPurpose.length)]

        this.list.push({phone: phone,amount: amount,purpose: purpose})
      }
    },
    methods: {
        swiperInit() {
            let swiper = new Swiper('.notice-swiper-container', {
                direction: 'vertical',
                autoplay: {
                    delay: 3000,
                    disableOnInteraction: false
                },
                loop: true,
        
                // 如果需要分页器
                pagination: {
                    el: '.swiper-pagination',
                    clickable: true,
                },

                // 如果需要前进后退按钮
                // navigation: {
                //   nextEl: '.swiper-button-next',
                //   prevEl: '.swiper-button-prev',
                // },

                // 如果需要滚动条
                // scrollbar: {
                //   el: '.swiper-scrollbar',
                // },
            })

            swiper.allowTouchMove = false;
        }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .notice-wrapper
    width: 100%
    height: 24px
    bottom: -24px
    background-color #fdfce7
    .notice
      display: flex
      width: 100%
      height: 100%
      padding-left: 10px
      background-color: rgba(255, 255, 255, .4)
      .icon
        width: 14px
        height: 100%
        background: url('../../assets/img/icon_horn.png') no-repeat center;
        background-size: 14px 14px
      .swiper-container
        margin-left: 4px
        .phone-item
          display: flex
          align-items: center
          color: #333
          font-size: 12px
</style>
