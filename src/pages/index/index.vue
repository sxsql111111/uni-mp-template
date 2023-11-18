<template>
  <View class="viewport">
    <!-- 自定义导航栏 -->
    <CustomNavbar></CustomNavbar>
    <!-- 滚动容器 -->
    <wSwiper :list="bannerList"></wSwiper>
    <!-- 商品分类 -->
    <CateGoryPanel :list="categoryList"></CateGoryPanel>
    <!-- 热门推荐 -->
    <HotPannel :list="hotList"></HotPannel>
    <!-- 猜你喜欢 -->
    <Guess></Guess>
  </View>
</template>

<script lang="ts" setup>
// @ts-ignore
import CustomNavbar from './Components/CustomNavbar'
// @ts-ignore
import CateGoryPanel from './components/CategoryPanel'
// @ts-ignore
import HotPannel from './Components/HotPannel.vue'
// 获取轮播图
const bannerList = ref<BannerItem[]>([])
const getHomeBannerData = async () => {
  const res = await getHomeBannerAPI()
  bannerList.value = res.result
}

//获取分类数据
const categoryList = ref<CategoryItem[]>([])
const getHomeCategoryData = async () => {
  const res = await getHomeCategoryAPI()
  categoryList.value = res.result
}

//获取热门推荐数据
const hotList = ref([])
const getHomeHotData = async () => {
  const res = await getHomeHotAPI()
  hotList.value = res.result
}

onLoad(async () => {
  await Promise.all([getHomeBannerData(), getHomeCategoryData(), getHomeBannerData()])
  await getHomeBannerData()
})
</script>
<style lang="scss" scoped></style>
