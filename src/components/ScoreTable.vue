<template>
  <div class="list">
    <div class="list__year">
      Year:
      <span :class="{'-finish' : year == 2020}">{{year}}</span>
    </div>
    <div class="list__item" v-for="(item,index) in filteredList" :key="index">
      <div class="list__item__title">{{item.name}}</div>
      <div class="list__item__bar" :style="calcWidth(item.rate)"></div>
      <div class="list__item__logo" :is="`logo-${item.name}`"></div>
      <div class="list__item__rate">{{withDot(item.rate)}} $</div>
    </div>
    <div class="list__more" @click="moreLess()">{{this.limit == 7 ? 'More' : 'Less'}}</div>
  </div>
</template>

<script>
export default {
  name: "ScoreTable",
  props: {
    isStart: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      year: 1996,
      limit: 7,
      list: [],
    };
  },
  computed: {
    total: function () {
      return this.list.map((item) => item.rate).reduce((sum, x) => sum + x);
    },
    filteredList: function () {
      // eslint-disable-next-line vue/no-side-effects-in-computed-properties
      return this.list
        .sort((a, b) => b.rate - a.rate)
        .filter((item, index) => index < this.limit);
    },
  },
  created() {
    this.init();
  },
  watch: {
    isStart: function (val) {
      if (val) {
        this.begening();
        this.t = setInterval(() => {
          this.year++;
          if (this.year == 2020) clearInterval(this.t);
        }, 1000);
      }

      if (!val) {
        this.year = 1996;
        this.init();
        clearInterval(this.t);
      }
    },
  },
  methods: {
    init: function () {
      this.list = [
        {
          name: "Amazon",
          color: "#333",
          rate: 1282514,
        },
        {
          name: "Microsoft",
          color: "#333",
          rate: 655212,
        },
        {
          name: "Apple",
          color: "#333",
          rate: 545221,
        },
        {
          name: "Facebook",
          color: "#333",
          rate: 125445,
        },
        {
          name: "Alibaba",
          color: "#333",
          rate: 352214,
        },
        {
          name: "Tencent",
          color: "#333",
          rate: 375421,
        },
        {
          name: "Visa",
          color: "#333",
          rate: 323662,
        },
        {
          name: "Nestle",
          color: "#333",
          rate: 12003,
        },
        {
          name: "Toyota",
          color: "#333",
          rate: 339885,
        },
        {
          name: "Samsung",
          color: "#333",
          rate: 322022,
        },
        {
          name: "Verizon",
          color: "#333",
          rate: 420000,
        },
        {
          name: "Intel",
          color: "#333",
          rate: 130020,
        },
        {
          name: "Sony",
          color: "#333",
          rate: 123325,
        },
        {
          name: "Faraday",
          color: "#333",
          rate: 100,
        },
      ];
    },
    calcWidth: function (rate) {
      let _rate = (100 / (this.total / rate)) * 2;
      return `width: ${_rate}%`;
    },
    withDot: function (rate) {
      let parts = rate.toString().split(".");
      parts[0] = parts[0].replace(/\B(?=(\d{3})+(?!\d))/g, ".");
      return parts.join(",");
    },
    begening: function () {
      let vm = this;

      vm.list.forEach((item) => {
        this.b = setInterval(() => {
          let avr = null;
          if (this.year == 2020) return clearInterval(this.b);

          if (item.name == "Faraday") {
            avr = 9999;
          } else if (item.name == "Facebook") {
            avr = 6666;
          } else if (item.name == "Intel") {
            avr = 4444;
          } else {
            avr = 1111;
          }
          let _random = Math.floor(Math.random() * avr) + 1;
          item.rate += _random;
        }, 100);
      });
    },
    moreLess: function () {
      if (this.limit == 7) return (this.limit = this.list.length - 1);
      if (this.limit != 7) return (this.limit = 7);
    },
  },
};
</script>