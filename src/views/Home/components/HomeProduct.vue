<script setup>
import HomePanel from "./HomePanel.vue";
import { getGoodsAPI } from "@/apis/home";
import { onMounted, ref } from "vue";
import GoodsItem from './GoodsItem.vue'

//获取数据列表
const goodsProduct = ref([]);
const getGoods = async () => {
  const res = await getGoodsAPI();
  goodsProduct.value = res.result;
};

onMounted(() => getGoods());
</script>

<template>
  <div class="home-product">
    <HomePanel :title="cate.name" v-for="cate in goodsProduct" :key="cate.id">
      <div class="box">
        <RouterLink class="cover" to="/">
          <img v-img-lazy="cate.picture" />
          <strong class="label">
            <span>{{ cate.name }}馆</span>
            <span>{{ cate.saleInfo }}</span>
          </strong>
        </RouterLink>
        <ul class="goods-list">
          <li v-for="goods in cate.goods" :key="goods.id">
            <GoodsItem :goods="goods" />
          </li>
        </ul>
      </div>
    </HomePanel>
  </div>
</template>

<style scoped lang="scss">
.home-product {
  background: #fff;
  margin-top: 20px;
  .sub {
    margin-bottom: 2px;

    a {
      padding: 2px 12px;
      font-size: 16px;
      border-radius: 4px;

      &:hover {
        background: $xtxColor;
        color: #fff;
      }

      &:last-child {
        margin-right: 80px;
      }
    }
  }

  .box {
    display: flex;

    .cover {
      width: 240px;
      height: 610px;
      margin-right: 10px;
      position: relative;

      img {
        display: block;
        background-color: #fff;
        width: 100%;
        height: 100%;
        object-fit: contain;
        transition: transform 1s ease, opacity 1s ease; /* 添加过渡效果 */
      }

      img:hover {
        transform: scale(0.97); /* 缩放到97% */
        opacity: 0.8; /* 降低透明度 */
}

      .label {
        width: 188px;
        height: 66px;
        display: flex;
        font-size: 18px;
        color: #fff;
        line-height: 66px;
        font-weight: normal;
        position: absolute;
        left: 0;
        top: 50%;
        transform: translate3d(0, -50%, 0);

        span {
          height: 40px;
          font-size: 12px;
          text-align: center;

          &:first-child {
            width: 76px;
            background: rgba(0, 0, 0, 0.9);
            line-height: 40px;
          }

          &:last-child {
            flex: 1;
            background: rgba(0, 0, 0, 0.7);
            line-height: 40px;
          }
        }
      }
    }

    .goods-list {
      width: 990px;
      display: flex;
      flex-wrap: wrap;

      li {
        width: 240px;
        height: 300px;
        margin-right: 10px;
        margin-bottom: 10px;

        &:nth-last-child(-n + 4) {
          margin-bottom: 0;
        }

        &:nth-child(4n) {
          margin-right: 0;
        }
      }
    }
  }
}
</style>
