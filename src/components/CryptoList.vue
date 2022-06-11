<script>
export default {
  created() {
    fetch(
      "https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=250&page=1&sparkline=false"
    )
      .then((response) => response.json())
      .then((data) => (this.cryptoList = data));
  },

  data() {
    return {
      count: 0,
      cryptoList: [],
    };
  },
};
</script>

<template>
  <body class="container mx-auto my-20">
    <div class="flex flex-col">
      <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
          <div
            class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg"
          >
            <table class="min-w-full divide-y divide-gray-200">
              <thead class="bg-gray-50">
                <tr>
                  <th
                    scope="col"
                    class="px-6 py-3 text-md text-justify font-medium text-zinc-700 uppercase tracking-wider"
                  >
                    #
                  </th>
                  <th
                    scope="col"
                    class="px-6 py-3 text-md text-justify font-medium text-zinc-700 uppercase tracking-wider"
                  >
                    Name
                  </th>
                  <th
                    scope="col"
                    class="px-6 py-3 text-md text-justify font-medium text-zinc-700 uppercase tracking-wider"
                  >
                    Price
                  </th>
                  <th
                    scope="col"
                    class="px-6 py-3 text-md text-justify font-medium text-zinc-700 uppercase tracking-wider"
                  >
                    Market Cap
                  </th>
                  <th
                    scope="col"
                    class="px-6 py-3 text-md text-justify font-medium text-zinc-700 uppercase tracking-wider"
                  >
                    Volume (24h)
                  </th>
                  <th
                    scope="col"
                    class="px-6 py-3 text-md text-justify font-medium text-zinc-700 uppercase tracking-wider"
                  >
                    24h %
                  </th>
                </tr>
              </thead>
              <tbody class="bg-white divide-y divide-gray-200">
                <tr v-for="(item, index) in cryptoList" :key="index">
                  <td class="px-6 py-4 whitespace-nowrap">
                    {{ item.market_cap_rank }}
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap">
                    <div class="flex items-center">
                      <div class="flex-shrink-0 h-7 w-7">
                        <img class="rounded-full" :src="item.image" alt="" />
                      </div>
                      <div class="ml-4">
                        <div class="font-medium">
                          {{ item.name }}
                          <span class="text-sm text-gray-400">
                            ({{ item.symbol.toUpperCase() }})
                          </span>
                        </div>
                      </div>
                    </div>
                  </td>
                  <td class="text-sm px-6 py-4 whitespace-nowrap">
                    {{
                      item.current_price.toLocaleString("en-US", {
                        style: "currency",
                        currency: "USD",
                      })
                    }}
                  </td>
                  <td class="text-sm px-6 py-4 whitespace-nowrap">
                    {{
                      item.market_cap.toLocaleString("en-US", {
                        style: "currency",
                        currency: "USD",
                        minimumFractionDigits: 0,
                        maximumFractionDigits: 0,
                      })
                    }}
                  </td>
                  <td class="text-sm px-6 py-4 whitespace-nowrap">
                    {{
                      item.total_volume.toLocaleString("en-US", {
                        style: "currency",
                        currency: "USD",
                        minimumFractionDigits: 0,
                        maximumFractionDigits: 0,
                      })
                    }}
                  </td>
                  <td class="text-sm px-6 py-4 whitespace-nowrap">
                    <p
                      v-if="item.price_change_percentage_24h < 0"
                      class="flex text-red-600"
                    >
                      <svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="h-5 w-5 pt-1"
                        viewBox="0 0 20 20"
                        fill="currentColor"
                      >
                        <path
                          fill-rule="evenodd"
                          d="M14.707 10.293a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 111.414-1.414L9 12.586V5a1 1 0 012 0v7.586l2.293-2.293a1 1 0 011.414 0z"
                          clip-rule="evenodd"
                        />
                      </svg>
                      {{ item.price_change_percentage_24h }}%
                    </p>
                    <p v-else class="flex text-green-600">
                      <svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="h-5 w-5 pt-1"
                        viewBox="0 0 20 20"
                        fill="currentColor"
                      >
                        <path
                          fill-rule="evenodd"
                          d="M5.293 9.707a1 1 0 010-1.414l4-4a1 1 0 011.414 0l4 4a1 1 0 01-1.414 1.414L11 7.414V15a1 1 0 11-2 0V7.414L6.707 9.707a1 1 0 01-1.414 0z"
                          clip-rule="evenodd"
                        />
                      </svg>
                      {{ item.price_change_percentage_24h }}%
                    </p>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </body>
</template>

<style scoped>
button {
  font-weight: bold;
}
</style>
