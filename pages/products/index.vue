<template>
  <div class="px-4 md:px-8 py-8 pt-12 flex flex-col bg-blue-1 relative">
    <div class="linkWrap absolute text-gray-700 text-sm" style="top: 20px;">
      <nuxt-link to="/" class="link mr-1">
        首頁
      </nuxt-link>
      >
      <nuxt-link :to="$route.path" class="link mx-1">
        尋找販時者
      </nuxt-link>
    </div>
    <div
      class="search border-b border-gray-600 w-full lg:px-3
      py-4 pb-6 text-gray-700  font-huninn">
      <div
        class="search__header flex items-start justify-center
        flex-wrap sm:justify-start lg:flex-no-wrap">
        <div
          class="relative mb-4 w-full xs:w-3/4 sm:w-1/2 lg:w-1/3 xs:mr-4">
          <input
            type="text"
            class="w-full py-3 h-12 border border-gray-600 pl-6
            focus:outline-none tracking-wider shadow hover:border-gray-700 font-medium"
            style="border-radius: 25px;"
            placeholder="請輸入關鍵字"
            v-model="search"
            @keypress.enter="searchProduct">
          <button
            class="w-6 h-6 absolute top-0 bottom-0 m-auto icon_search focus:outline-none"
            style="right: 20px;"
            @click="searchProduct" />
        </div>
        <div class="relative inline-block w-full xs:w-3/4 sm:w-40 mb-4 xs:mr-4">
          <select
            style="border-radius: 25px;"
            class="block appearance-none w-full bg-white border h-12
            border-gray-600 hover:border-gray-700 px-4 py-3 pl-16
            shadow leading-tight focus:outline-none focus:shadow-outline font-medium
            cursor-pointer"
            v-model="location">
            <option :value="null">
              地點
            </option>
            <option value="keelung">
              基隆市
            </option>
            <option value="taipei">
              台北市
            </option>
            <option value="newTaipei">
              新北市
            </option>
            <option value="taoyuan">
              桃園縣
            </option>
            <option value="hsinchuCity">
              新竹市
            </option>
            <option value="hsinchuCountry">
              新竹縣
            </option>
            <option value="miaoli">
              苗栗縣
            </option>
            <option value="taichung">
              台中市
            </option>
            <option value="changhua">
              彰化縣
            </option>
            <option value="nantou">
              南投縣
            </option>
            <option value="yunlin">
              雲林縣
            </option>
            <option value="chiayiCity">
              嘉義市
            </option>
            <option value="chiayiCountry">
              嘉義縣
            </option>
            <option value="tainan">
              台南市
            </option>
            <option value="kaohsiung">
              高雄市
            </option>
            <option value="pingtung">
              屏東縣
            </option>
            <option value="taitung">
              台東縣
            </option>
            <option value="hualien">
              花蓮縣
            </option>
            <option value="yilan">
              宜蘭縣
            </option>
            <option value="penghu">
              澎湖縣
            </option>
            <option value="kinmen">
              金門縣
            </option>
            <option value="lienchiang">
              連江縣
            </option>
          </select>
          <div
            class="pointer-events-none absolute inset-y-0 flex items-center px-2 text-gray-700"
            style="right: 5px;">
            <svg class="fill-current h-6 w-6" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
              <path
                d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z" />
            </svg>
          </div>
          <i
            class="icon_location absolute h-6 w-6 m-auto top-0 bottom-0 pointer-events-none"
            style="left: 20px;" />
        </div>
        <div class="relative inline-block w-full xs:w-3/4 sm:w-48 xs:mr-4 mb-4">
          <select
            style="border-radius: 25px; padding-left: 3.8rem;"
            class="block appearance-none w-full bg-white h-12
            border border-gray-600 hover:border-gray-700 py-3
            shadow leading-tight focus:outline-none focus:shadow-outline font-medium
            cursor-pointer"
            v-model="priceSelect">
            <option :value="null">
              價格
            </option>
            <option value="100">
              100 以下
            </option>
            <option value="100T250">
              100 ~ 250
            </option>
            <option value="250T500">
              250 ~ 500
            </option>
            <option value="500T1000">
              500 ~ 1000
            </option>
            <option value="T1000">
              1000 以上
            </option>
          </select>
          <div
            class="pointer-events-none absolute inset-y-0 flex items-center px-2 text-gray-700"
            style="right: 5px;">
            <svg class="fill-current h-6 w-6" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
              <path
                d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z" />
            </svg>
          </div>
          <i
            class="icon_coin absolute h-6 w-6 m-auto top-0 bottom-0 pointer-events-none"
            style="left: 20px;" />
        </div>
        <label
          class="py-1 bg-white pr-6 relative border border-gray-600
          focus:outline-none h-12 hover:border-gray-700 shadow pl-12
          cursor-pointer w-full xs:w-3/4 sm:w-auto xs:mr-4"
          style="border-radius: 25px;"
          :class="{'bg-blue-2 text-white' : isIdentify}"
          for="identify">
          <h3 class="font-medium tracking-widest">
            認證徽章
          </h3>
          <p style="font-size: 8px; transform: translateY(-2px);">
            完成雙認證的販時者
          </p>
          <i
            class="icon_identify h-6 w-6 absolute top-0 bottom-0 m-auto"
            style="left: 13px;" />
          <input type="checkbox" name="identify" class="hidden" v-model="isIdentify" id="identify">
        </label>
      </div>

      <div class="search__tagWrap mt-6 lg:mt-4 flex flex-wrap px-2 xs:px-4">
        <button
          @click="selectTag('entrepreneurship')"
          :class="tagDisplay('entrepreneurship')">
          創業 / 副業
        </button>
        <button
          @click="selectTag('marking')"
          :class="tagDisplay('marking')">
          行銷
        </button>
        <button
          @click="selectTag('chat')"
          :class="tagDisplay('chat')">
          聊天
        </button>
        <button
          @click="selectTag('music')"
          :class="tagDisplay('music')">
          音樂 / 樂器
        </button>
        <button
          @click="selectTag('businessCommunication')"
          :class="tagDisplay('businessCommunication')">
          職場溝通 / 諮詢
        </button>
        <button
          @click="selectTag('cook')"
          :class="tagDisplay('cook')">
          料理
        </button>
        <button
          @click="selectTag('picture')"
          :class="tagDisplay('picture')">
          攝影
        </button>
        <button
          @click="selectTag('lifePlan')"
          :class="tagDisplay('lifePlan')">
          人生規劃
        </button>
        <button
          @click="selectTag('divination')"
          :class="tagDisplay('divination')">
          占卜
        </button>
        <button
          @click="selectTag('love')"
          :class="tagDisplay('love')">
          戀愛諮詢
        </button>
        <button
          @click="selectTag('diet')"
          :class="tagDisplay('diet')">
          飲食調理 / 減肥
        </button>
        <button
          @click="selectTag('makeup')"
          :class="tagDisplay('makeup')">
          化妝 / 保養
        </button>
        <button
          @click="selectTag('family')"
          :class="tagDisplay('family')">
          家庭 / 教育
        </button>
        <button
          @click="selectTag('sport')"
          :class="tagDisplay('sport')">
          健身 / 運動
        </button>
        <button
          @click="selectTag('animation')"
          :class="tagDisplay('animation')">
          動畫製作
        </button>
        <button
          @click="selectTag('other')"
          :class="tagDisplay('other')">
          其他
        </button>
        <button @click="selectTag('all')" class="toolBtn">
          全部
        </button>
        <button @click="tags = []" class="toolBtn">
          清除
        </button>
      </div>
      <ul
        class="search__typeWrap flex mt-2 text-gray-800 text-sm font-medium pl-2
        xs:pl-4 select-none
        flex items-center font-sans flex-wrap">
        <li style="line-height: 3rem;">
          <h3 class="text-base tracking-wider mr-6">
            接受類型
          </h3>
        </li>
        <li class="mr-4">
          <input class="hidden" type="checkbox" id="meeting" value="meeting" v-model="types">
          <label
            class="inline-block h-4 w-4 border border-gray-600 rounded-sm"
            style="transform: translate(-2px, 2px);"
            for="meeting" />
          <label for="meeting">面談</label>
        </li>
        <li class="mr-4">
          <input class="hidden" type="checkbox" id="video" value="video" v-model="types">
          <label
            class="inline-block h-4 w-4 border border-gray-600 rounded-sm"
            style="transform: translate(-2px, 2px);"
            for="video" />
          <label for="video">視訊</label>
        </li>
        <li class="mr-4">
          <input class="hidden" type="checkbox" id="phone" value="phone" v-model="types">
          <label
            class="inline-block h-4 w-4 border border-gray-600 rounded-sm"
            style="transform: translate(-2px, 2px);"
            for="phone" />
          <label for="phone">電話</label>
        </li>
        <li>
          <input class="hidden" type="checkbox" id="chat" value="chat" v-model="types">
          <label
            class="inline-block h-4 w-4 border border-gray-600 rounded-sm"
            style="transform: translate(-2px, 2px);"
            for="chat" />
          <label for="chat">聊天室
          </label>
        </li>
      </ul>
    </div>

    <div class="main sm:pt-0 pt-4">
      <div
        class="main__header h-16 flex sm:items-center ml-2 xs:ml-4 text-gray-800 md:px-12
        text-sm flex-col sm:flex-row items-start">
        <h4 class="font-medium text-base mb-2 sm:mb-0">
          搜尋結果
        </h4>
        <div class="sm:ml-auto flex items-center">
          <h4 class="mr-10 font-medium text-base">
            排序方式
          </h4>
          <button
            :class="{'text-blue-2 hover:text-blue-3' : sort.name === 'createTime'}"
            @click="sortBy('createTime')"
            class="mr-4 xs:mr-8 hover:text-gray-900 hover:font-medium focus:outline-none">
            最新
          </button>
          <button
            :class="{'text-blue-2 hover:text-blue-3' : sort.name === 'hot'}"
            @click="sortBy('hot')"
            class="mr-4 xs:mr-8 hover:text-gray-900 hover:font-medium focus:outline-none">
            熱門
          </button>
          <button
            :class="{'text-blue-2 hover:text-blue-3' : sort.name === 'price'}"
            @click="sortBy('price')"
            class="mr-4 xs:mr-8 hover:text-gray-900 hover:font-medium focus:outline-none">
            價格
          </button>
          <button
            :class="{'text-blue-2 hover:text-blue-3': !sort.isAsc}"
            @click="sortBy(null, true)"
            class="hover:text-gray-900 hover:font-medium focus:outline-none text-lg">
            ⇅
          </button>
        </div>
      </div>

      <card :products="filterProducts" />
    </div>
  </div>
</template>

<script>
import card from '~/components/card.vue';

export default {
  name: 'Products',
  head() {
    return {
      title: '尋找販時 | 時飯機',
    };
  },
  components: {
    card,
  },
  async asyncData({ $axios }) {
    const { data } = await $axios.get('/api/products');
    return { products: data.products };
  },
  layout: 'front',
  data() {
    return {
      products: '',
      priceSelect: null,
      search: '',
      location: null,
      isIdentify: false,
      tags: [],
      types: [],
      sort: {
        name: 'createTime',
        isAsc: false,
      },
    };
  },
  mounted() {
    if (this.$route.query.category) {
      this.tags.push(this.$route.query.category);
    }
  },
  methods: {
    selectTag(tagName) {
      if (tagName === 'all') {
        this.tags = ['entrepreneurship', 'love', 'diet', 'marking',
          'chat', 'music', 'businessCommunication', 'cook', 'picture',
          'lifePlan', 'divination', 'other', 'animation', 'sport',
          'family', 'makeup'];
        return;
      }
      if (!this.tags.includes(tagName)) {
        this.tags.push(tagName);
      } else {
        this.tags.splice(this.tags.indexOf(tagName), 1);
      }
    },
    sortBy(sortName, isAsc) {
      if (sortName) {
        this.sort.name = this.sort.name === sortName ? '' : sortName;
        this.sort.isAsc = true;
      }
      if (isAsc) {
        this.sort.isAsc = this.sort.isAsc !== true;
      }
    },
    async searchProduct() {
      let api = `/api/products?search=${this.search}`;
      if (this.search === '') {
        api = '/api/products';
      }
      const { data } = await this.$axios.get(api);
      this.products = data.products;
    },
  },
  computed: {
    filterProducts() {
      const tagFilterArr = this.products.filter((item) => {
        if (this.tags.includes('all') || this.tags.includes(item.category) || !this.tags.length) {
          return item;
        }
        return false;
      });

      const typeFilterArr = tagFilterArr.filter((item) => {
        const result = item.type.some((typeName) => this.types.includes(typeName));
        if (!this.types.length || result) {
          return item;
        }
        return false;
      });

      const priceArr = typeFilterArr.filter((item) => {
        if (!this.priceSelect) {
          return item;
        }
        const [min] = this.priceSelect.split('T');
        const max = this.priceSelect.split('T')[1];
        if (min && max) {
          return +item.price < +max
          && +item.price >= +min;
        }
        if (!max) {
          return +item.price < +min;
        }
        if (!min) {
          return +item.price >= +max;
        }
        return item;
      });

      const locationArr = priceArr.filter((item) => {
        if (!this.location) {
          return item;
        }
        return this.location === item.meetingPlace;
      });
      const identifyArr = locationArr.filter((item) => {
        if (!this.isIdentify) {
          return item;
        }
        return this.isIdentify === item.identified;
      });
      const myProductsArr = identifyArr.filter((item) => {
        if (this.$route.query.myProducts) {
          return item.userId === this.$store.state.userInfo.userId;
        }
        return item;
      });

      const sortArr = myProductsArr.sort((a, b) => {
        if (this.sort.name === 'hot') {
          return;
        }
        if (this.sort.name === 'createTime') {
          return this.sort.isAsc ? new Date(a[this.sort.name]) - new Date(b[this.sort.name])
            : new Date(b[this.sort.name]) - new Date(a[this.sort.name]);
        }
        return this.sort.isAsc ? a[this.sort.name] - b[this.sort.name]
          : b[this.sort.name] - a[this.sort.name];
      });

      return sortArr;
    },
    tagDisplay() {
      return (tagName) => {
        if (this.tags.includes(tagName) || this.tags.includes('all')) {
          return 'activeTag';
        }
      };
    },
  },
};
</script>

<style scoped lang="scss">
.search__tagWrap button{
  @apply py-1 px-3 bg-gray-600 text-white rounded-lg mr-3 mb-3
  font-medium tracking-wide text-sm shadow cursor-pointer select-none;
  &:hover{
    @apply bg-gray-700;
  }
  &:focus{
    @apply outline-none;
  }
  &.toolBtn{
    @apply bg-teal-500;
  }
}
.activeTag.activeTag{
  @apply bg-blue-3;
  &:hover{
    @apply bg-blue-2;
  }
}
.search__typeWrap{
  input[type="checkbox"]:checked + label {
    @apply bg-blue-2;
  }
  label{
    @apply cursor-pointer;
  }
}
.search__tagWrap input[type="checkbox"]:checked ~ label{
  @apply bg-blue-3;
}
.icon_location{
  background: url('~assets/icon_product_location.svg') center center / contain no-repeat;
}
.icon_search{
  background: url('~assets/icon_search_searchbar.svg') center center / contain no-repeat;
}
.icon_coin{
  background: url('~assets/icon_header_point.svg') center center / contain no-repeat;
}
.icon_identify{
  background: url('~assets/icon_product_proved.svg') center center / contain no-repeat;
}
.item__title{
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  display: -webkit-box;
  overflow: hidden;
  word-break: break-all;
  min-height: 54px
}
.link:hover{
  border-bottom: 1px solid gray;
}
.linkWrap{
  left: 60px;
}
@media (max-width: 767px) {
  .linkWrap{
    left: 10%;
  }
}
</style>
