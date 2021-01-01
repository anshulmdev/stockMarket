<template>
    <div class="...">
      <div v-if="loading">
      <link rel="stylesheet" href="https://pagecdn.io/lib/font-awesome/5.10.0-11/css/all.min.css" integrity="sha256-p9TTWD+813MlLaxMXMbTA7wN/ArzGyW/L7c5+KkjOkM=" crossorigin="anonymous">

<div class="w-full h-full fixed block top-0 left-0 bg-white opacity-75 z-50">
  <span class="text-green-500 opacity-75 top-1/2 my-0 mx-auto block relative w-0 h-0" style="
    top: 50%;
">
    <i class="fas fa-circle-notch fa-spin fa-5x"></i>
  </span></div>
</div>
        <div class="flex flex-col">
  <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
      <div class="pt-6 mb-10 text-base leading-10 font-bold sm:text-lg sm:leading-7">
        Market Today
        </div>
    <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
      <div class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg">
        <table class="min-w-full divide-y divide-gray-200">
          <thead class="bg-gray-50">
            <tr>
              <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                Symbol
              </th>
              <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                Close
              </th>
              <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                Change in Price
              </th>
              <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                Time Stamp
              </th>
              <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                Difference
              </th>
              <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                Reload
              </th>
            </tr>
          </thead>
          <tbody class="bg-white divide-y divide-gray-200">
              <template v-for="(menuGroup, index) in test">
            
            <tr :key="index">
              <td class="px-6 py-4 whitespace-nowrap">
                <div class="text-sm text-gray-900">{{menuGroup.symbol.replace('.NS','')}}</div>
              </td>
              <td class="px-6 py-4 whitespace-nowrap">
                <div class="text-sm text-gray-900">{{menuGroup.close}}</div>
              </td>
              <td class="px-6 py-4 whitespace-nowrap">
                <div class="text-sm text-gray-900">{{menuGroup.priceChangeInPercent}} %</div>
              </td>
              <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                {{menuGroup.modifiedTs}}
              </td>
              <td class="px-6 py-4 whitespace-nowrap">
                <span v-if="parseInt(menuGroup.priceChange)<0" class="px-4 inline-flex text-sm leading-5 font-semibold rounded-full bg-red-200 text-red-800">
                  {{menuGroup.priceChange}}
                </span>
                <span v-else class="px-4 inline-flex text-sm leading-5 font-semibold rounded-full bg-green-200 text-green-800">
                  {{menuGroup.priceChange}}
                </span>
              </td>
              <td class="px-6 py-4 whitespace-nowrap text-center text-sm font-medium">
                <a href="#" class="text-indigo-600 hover:text-indigo-900" @click="run(menuGroup.symbol)">Update</a>
              </td>
            </tr>
        </template>

            <!-- More rows... -->
          </tbody>
        </table>
      </div>
    </div>
  </div>
</div>
    </div>
</template>

<script>
export default {
  data () {
    return{
      data: ["NIFTY_50.NS", "SUZLON.NS","CENTURYPLY.NS","DHANBANK.NS", "V2RETAIL.NS","3IINFOTECH.NS","IDFCFIRSTB.NS", "JPINFRATEC.NS", "PVR.NS"],
      loading: true,
      test: []}
  },
  mounted () {
    this.data.forEach((e)=>{
      this.run(e)
    })
  },
  methods:{
    async run(script) {
      const response = await fetch(`https://stock-info.p.rapidapi.com/v1/equity/${script}`, {
	"method": "GET",
	"headers": {
		"x-rapidapi-key": "5c79db1482mshc23d72d7d215583p10d22ejsn8444584dfad5",
		"x-rapidapi-host": "stock-info.p.rapidapi.com"
	}
})
const dataEntry = await response.json();
this.test.push(dataEntry)
this.loading = false
    }
  }
}
</script>