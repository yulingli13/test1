<template>
  <div>
    <div class="head-image">
      <h1>
        新型冠状病毒感染情况统计数据表
      </h1>
    </div>
    <select v-model="selectedCountry">
      <option value="world">全部国家</option>
      <option value="china">中国</option>
      <option value="USA">美国</option>
      <option value="japan">日本</option>
    </select>
    <table>
      <thead>
        <tr>
          <th v-for="i in table_head" :key="i">
            {{ i }}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="i in covid19.length" :key="i">
          <td>
            {{ covid19[i-1]['Country_text'] }}
          </td>
          <td>
            {{ covid19[i-1]['Last Update'] }}
          </td>
          <td>
            {{ covid19[i-1]['Total Cases_text'] }}
          </td>
          <td>
            {{ covid19[i-1]['Total Recovered_text'] }}
          </td>
          <td>
            {{ covid19[i-1]['Total Deaths_text'] }}
          </td>
          <td>
            {{ covid19[i-1]['New Cases_text'] }}
          </td>
          <td>
            {{ covid19[i-1]['New Deaths_text'] }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'CovidTable',
  data: function (){
    return {
      url: 'https://covid-19.dataflowkit.com/v1',
      covid19: [],
      table_head: ['国家', '更新时间', '累计确诊', '累计治愈', '累计死亡', '新增确诊', '新增死亡'],
      selectedCountry: 'world'
    }
  },
  watch: {
    selectedCountry: function (val) {
      let that = this;
      let url_changed;
      if (val === 'world'){
        url_changed = this.url;
        axios.get(url_changed)
            .then(function (res) {
              that.covid19 = res.data;
              console.log(that.covid19);
            })
      }
      else{
        url_changed = this.url + '/' + val;
        axios.get(url_changed)
            .then(function (res) {
              that.covid19 = [res.data];
              console.log(that.covid19);
            })
      }

    }
  },
  mounted() {
    let that = this;
    axios.get(this.url)
        .then(function (res) {
          that.covid19 = res.data;
        })
  }
}

</script>
<style>
table, td, th, tr {
  border: 1px solid black;
  border-collapse:collapse;
}
table {
  width: 100%;
}
thead {
  background: #F8FAFB;
}
th, td {
  padding-left: 5px;
  width: 200px;
}
th {
  background-color: black;
  color: #F8FAFB;
}

tr:nth-child(even) {
  background-color: #fff;
}

tr:nth-child(odd) {
  background-color: #F5F5F5;
}

select {
  width: 180px;
  height: 40px;
  padding: 10px;
  margin-bottom: 20px;
}
.head-image {
  height: 100px;
  background-image: url('../assets/covid.png');
  background-repeat: repeat-x;
  margin-bottom: 20px;
}
.head-image h1 {
  line-height: 100px;
  color: yellow;
}
</style>