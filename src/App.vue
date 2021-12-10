<template>
  <div class="info-wrapper">
    <div class="info-main">
      <h1>{{ year }}/{{ month }}</h1>
      <div class="move-month">
        <button @click="moveBeforeMonth">＜</button>
        <button @click="moveNextMonth">＞</button>
      </div>
    </div>
  </div>
  <div class="calender-wrapper">
    <div class="calender-main">
      <Cell :type="cell.type" :date="cell.date" v-for="(cell,index) in DateArray" :key="index"/>

    </div>

  </div>
</template>

<script>

import Cell from "@/components/Cell";

export default {
  name: 'App',
  components: {Cell},
  data() {
    return {
      year: null,
      month: null,
    }
  },
  created() {
    const now = new Date()
    this.year = now.getFullYear()
    this.month = now.getMonth() + 1
  },
  computed: {
    DateArray: function () {
      const TargetDate = new Date(this.year, this.month - 1, 1)
      console.log(TargetDate)
      const day = TargetDate.getDay()


      let Result = this.getDefaultDate()
      const BeforeMonthMaxDate = this.calcDate("Before")
      for (let i = 0; i < day; i++) {
        Result.push({
          type: "blank",
          date: BeforeMonthMaxDate - i
        })
      }
      const ThisMonthMaxDate = this.calcDate("This")
      for (let n = 0; n < ThisMonthMaxDate; n++) {
        Result.push({
          type: "month",
          date: n + 1
        })
      }

      const AfterMonthCount = 7 - (Result.length % 7)

      for (let a = 0; a < AfterMonthCount; a++) {
        Result.push({
          type: "blank",
          date: a + 1
        })
      }

      return Result
    }
  },
  methods: {
    getDefaultDate() {
      return [
        {
          type: "default",
          date: "日"
        },
        {
          type: "default",
          date: "月"
        },
        {
          type: "default",
          date: "火"
        },
        {
          type: "default",
          date: "水"
        },
        {
          type: "default",
          date: "木"
        },
        {
          type: "default",
          date: "金"
        },
        {
          type: "default",
          date: "土"
        }
      ]
    },
    moveBeforeMonth() {
      if (this.month === 1) {
        this.month = 12
        this.year--;
      } else {
        this.month--
      }
    },
    moveNextMonth() {
      if (this.month === 12) {
        this.month = 1
        this.year++
      } else {
        this.month++
      }
    },
    calcDate(Type) {
      let M
      if (Type === "Before") {
        M = this.month - 1
        if (M === 0) {
          M = 12
        }
      } else if (Type === "After") {
        M = this.month % 12 - 1
      } else {
        M = this.month
      }
      switch (M) {
        case 1:
        case 3:
        case 5:
        case 7:
        case 8:
        case 10:
        case 12:
          return 31
        case 2:
          if (this.year / 4 !== 0) {
            return 28
          }
          return 29
        case 4:
        case 6:
        case 9:
        case 11:
          return 30
      }
    }
  }
}
</script>

<style>
.calender-wrapper {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.info-wrapper{
  width: 100%;
  display: flex;
  justify-content: center;
}

.calender-main  {
  width: 840px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: flex-start;
}
.info-main{
  width: 840px;
  display: flex;
}

.move-month {
  display: flex;
}

.move-month > button {
  background: none;
  outline: none;
  border: none;
  font-size: 36px;
  padding: 20px;
}

</style>
