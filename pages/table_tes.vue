<template>
  <v-data-table
    v-model="selected"
    :headers="headers"
    :items="items"
    :single-select="singleSelect"
    item-key="title"
    show-select
    class="elevation-1"
    :loading="loading"
  >
    <template v-slot:top>
      <v-switch v-model="singleSelect" label="Single select" class="pa-3" />
      <!-- </v-switch> -->
    </template>
  </v-data-table>
</template>

<script>
export default {
  data () {
    return {
      loading: true,
      singleSelect: false,
      selected: [],
      headers: [
        { text: 'Judul', value: 'title' },
        { text: 'Harga', value: 'price' },
        { text: 'Satuan', value: 'denom' },
        { text: 'Deskripsi', value: 'desc' }
      ],
      items: []
    }
  },
  mounted () {
    this.loadData()
  },
  methods: {
    async loadData () {
      this.loading = true
      const resp = await this.$axios.get('https://sativa.now.sh/api/bo/harga/harga')
      const prices = resp.data.gtfwResult.data.prices
      console.log(prices)
      for (const item in prices) {
        this.items.push(prices[item])
      }
      this.loading = false
    }
  }
}
</script>
