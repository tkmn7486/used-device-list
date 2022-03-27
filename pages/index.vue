<template>
  <section>
    <b-tabs>
      <b-tab-item label="選択した機種の詳細">
        <div class="selected-tab">
          <p class="selected-title">
            {{ selected ? selected.model_name : null }} ({{ selected ? selected.model_number : null }})
          </p>
          <div class="badges">
            <div class="rank">
              <p class="rank-cont">
                {{ selected ? selected.rank[0] : null }}
              </p>
              <label class="rank-after">ランク</label>
            </div>
            <div class="os">
              <p>{{ selected ? selected.OS[0] : null }}</p>
            </div>
          </div>
          <div class="tile is-ancestor">
            <!-- tile -->
            <div class="tile is-4 is-vertical is-parent">
              <div class="tile is-child box">
                <p class="title">
                  スペック
                </p>
                <div class="specs">
                  <p class="spec">
                    カラー：
                  </p>
                  <p class="spec">
                    容量：
                  </p>
                  <p class="spec">
                    メモリ：
                  </p>
                  <p class="spec">
                    OS最新：
                    {{ selected ? selected.max_version : null }}
                  </p>
                </div>
              </div>
              <div class="tile is-child box">
                <p class="title">
                  利用可能なアプリ
                </p>
              </div>
            </div>
            <div class="tile is-parent">
              <div class="tile is-child box">
                <div class="img-area">
                  <div class="front">
                    <img :src="selected ? selected.front_img.url : null" alt="front_img" class="device-img">
                    <p>前面</p>
                  </div>
                  <div class="back">
                    <img :src="selected ? selected.back_img.url : null" alt="back_img" class="device-img">
                    <p>背面</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
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
.selected-tab{
  text-align:center;
}

.selected-title{
  font-size:30px;
  margin-bottom:20px;
  font-weight:bold;
}

.os{
  border:solid;
  border-radius:10px;
  width:200px;
  display:inline-block;
  font-size:20px;
}

.rank{
  border:solid;
  border-radius:10px;
  width:200px;
  height:auto;
  display:inline-block;
}

.rank-cont{
  display:inline;
  font-size:20px;
}

.rank-after{
  display:inline;
}

.badges{
  margin:10px;
}

.specs{
  width:40%;
  margin:0 auto;
}

.spec{
  text-align:left;
}

.device-img{
  width:300px;
}

.front{
  display:inline-block;
  text-align:center;
  margin:10px 20px;
}

.back{
  display:inline-block;
  text-align:center;
  margin:10px 20px;
}

.title{
  font-size:20px;
}

</style>
