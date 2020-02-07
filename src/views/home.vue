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
      sum_percent_qUse: 0,
      date: ""
    };
  },
  methods: {
    getWaterPercentUse(date) {
      let url = `http://localhost:3000`;
      axios
        .get(`${url}/getWater?date=${date}`)
        .then(res => {
          console.log(res.data);
          if (res.length === 0) {
            this.sum_percent_qUse = 0;
            console.log(this.sum_percent_qUse);
          } else {
            this.sum_percent_qUse = res.data.sum_all.sum_PERCENT_QUse;
          }
        })
        .catch(err => {
          console.log(err);
          this.sum_percent_qUse = 0;
        });
    },
    formatDate(date) {
      var d = new Date(date),
        month = "" + (d.getMonth() + 1),
        day = "" + d.getDate(),
        year = d.getFullYear();

      if (month.length < 2) month = "0" + month;
      if (day.length < 2) day = "0" + day;

      return [year, month, day].join("-");
    }
  },
  mounted() {
    this.date = this.formatDate(new Date().toLocaleDateString());
    this.getWaterPercentUse(this.date);
  }
};
</script>
