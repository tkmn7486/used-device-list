<template>
  <section class="section">
    <p class="is-size-2">
      中古端末一覧
    </p>
    <b-table
      :data="contents"
      :columns="columns">
    </b-table>
  </section>
</template>

<script>

export default {
  name: 'IndexPage',
  data () {
    return {
      columns: [
        {
          field: 'id',
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
          field: 'os',
          label: 'OS',
          searchable: true
        }
      ]
    }
  }
}
</script>

<style>
</style>
