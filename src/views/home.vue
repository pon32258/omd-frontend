<template>
  <z-view>
    จํานวนปริมาณนํ้าที่สามารถใช้ได้จากเขื่อนทั้งหมด
    <br />
    <h1>{{ sum_percent_qUse }}</h1>
  </z-view>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      sum_percent_qUse: 0
    };
  },
  methods: {
    getPercentUse() {
      axios
        .get("http://localhost:3000/getWater?date=2019-08-27")
        .then(res => {
          if (res.length === 0) {
            this.sum_percent_qUse = 0;
            console.log(this.sum_percent_qUse);
          } else {
            this.sum_percent_qUse = res.sum_all.sum_PERCENT_QUse;
          }
        })
        .catch(err => {
          console.log(err);
          this.sum_percent_qUse = 0;
        });
    }
  },
  mounted() {
    this.getPercentUse();
  }
};
</script>
