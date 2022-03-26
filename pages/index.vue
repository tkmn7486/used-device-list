<template>
  <section>
    <p class="is-size-2">
      中古端末一覧
    </p>
    <b-tabs>
      <b-tab-item label="選択した機種の詳細">
        <p>{{ selected ? selected.model_name : null }}</p>
      </b-tab-item>

      <b-tab-item label="端末一覧">
        <b-table
          :data="contents"
          :columns="columns"
          :selected.sync="selected"
          focusable
        />
      </b-tab-item>
    </b-tabs>
  </section>
</template>

<script>
import axios from 'axios'
export default {
  name: 'IndexPage',
  async asyncData () {
    const { data } = await axios.get(
      // your-service-id部分は自分のサービスidに置き換えてください
      'https://used-device-list.microcms.io/api/v1/used-list-k?limit=100',
      {
        // your-api-key部分は自分のapi-keyに置き換えてください
        headers: { 'X-MICROCMS-API-KEY': 'a3ab90328c87471dab133dfd64f4098e631b' }
      }
    )
    return data
  },
  data () {
    const selected = ''

    return {
      selected: selected[0],
      columns: [
        {
          field: 'cont_id',
          label: 'ID',
          width: '100',
          numeric: true,
          searchable: true
        },
        {
          field: 'model_name',
          label: '機種名',
          searchable: true
        },
        {
          field: 'career',
          label: 'キャリア',
          searchable: true
        },
        {
          field: 'OS',
          label: 'OS',
          searchable: true
        },
        {
          field: 'rank',
          label: '商品ランク',
          searchable: true
        }
      ]
    }
  }
}
</script>

<style>
</style>
