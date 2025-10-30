<!-- src/components/ProjectsSection.vue -->
<script setup lang="ts">
import { ref, computed } from 'vue'

type RecordItem = {
  name: string
  units: string
  addr: string
}

const indoor: RecordItem[] = [
  {
    name: '시흥유통상가',
    units: '3,501세대 / 37동',
    addr: '서울특별시 금천구 시흥대로 97 (시흥유통센터)',
  },
  { name: '상계주공17단지', units: '1,980세대 / 11동', addr: '서울특별시 도봉구 덕릉로66길 17' },
  {
    name: '고덕롯데캐슬 베네루체아파트',
    units: '1,859세대 / 20동',
    addr: '서울시 강동구 상암로79길 88(상일동)',
  },
  { name: '광명하안주공9단지', units: '1,818세대 / 15동', addr: '경기도 광명시 하안로364' },
  {
    name: '금천롯데캐슬골드파크1차',
    units: '1,743세대 / 11동',
    addr: '서울특별시 금천구 벚꽃로 40',
  },
  {
    name: '햇빛마을20단지주공',
    units: '1,713세대 / 17동',
    addr: '경기도 고양시 덕양구 충장로152번길 39',
  },
  { name: '하안주공8단지아파트', units: '1,680세대 / 21동', addr: '경기도 광명시 하안로 237, 1층' },
  { name: '갈산주공1단지', units: '1,650세대 / 9동', addr: '인천광역시 부평구 굴포로 81-1' },
  {
    name: '보라매sk뷰아파트',
    units: '1,546세대 / 18동',
    addr: '서울특별시 영등포구 여의대방로35가길 19(신길동)',
  },
  {
    name: '마곡앰밸리9단지',
    units: '1,529세대 / 19동',
    addr: '서울특별시 강서구 공항대로 103(마곡동)',
  },
]

const tree: RecordItem[] = [
  { name: '상계주공17단지', units: '1,980세대 / 11동', addr: '서울특별시 도봉구 덕릉로66길 17' },
  {
    name: '고덕롯데캐슬 베네루체아파트',
    units: '1,859세대 / 20동',
    addr: '서울시 강동구 상암로79길 88(상일동)',
  },
  { name: '광명하안주공9단지', units: '1,818세대 / 15동', addr: '경기도 광명시 하안로364' },
  {
    name: '햇빛마을20단지주공',
    units: '1,713세대 / 17동',
    addr: '경기도 고양시 덕양구 충장로152번길 39',
  },
  { name: '하안주공8단지아파트', units: '1,680세대 / 21동', addr: '경기도 광명시 하안로 237, 1층' },
  {
    name: '보라매sk뷰아파트',
    units: '1,546세대 / 18동',
    addr: '서울특별시 영등포구 여의대방로35가길 19(신길동)',
  },
  {
    name: '마곡앰밸리9단지',
    units: '1,529세대 / 19동',
    addr: '서울특별시 강서구 공항대로 103(마곡동)',
  },
  { name: '검단SK뷰', units: '530세대 / 8동', addr: '인천광역시 서구 독정로 17' },
  { name: '당산2가현대', units: '783세대 / 7동', addr: '서울 영등포구 당산로 95' },
  { name: '예천군 삼강주막마을', units: '-', addr: '경북 예천군 풍양면 삼강리길 91' },
]

const tank: RecordItem[] = [
  { name: 'DMC센트레빌', units: '473세대 / 7동', addr: '서울시 서대문구 거북골로 120' },
  {
    name: 'e편한세상금정역에코센트럴아파트',
    units: '677세대 / 8동',
    addr: '경기도 군포시 금산로 47',
  },
  { name: '고척 산업용품종합상가', units: '3,404세대 / 2동', addr: '서울시 구로구 중앙로3길 50' },
  { name: '시흥동 삼익아파트', units: '786세대 / 13동', addr: '서울시 금천구 독산로50길 89' },
  { name: '구로 럭키아파트', units: '427세대 / 2동', addr: '서울시 구로구 도림로 107' },
  { name: '고척 서울가든아파트', units: '715세대 / 5동', addr: '서울시 구로구 중앙로5길 62' },
  {
    name: '경북도청호반베르디움1차아파트',
    units: '830세대 / 13동',
    addr: '경북 예천군 행복로 215',
  },
  {
    name: '김포수기마을3단지힐스테이트아파트',
    units: '203세대 / 7동',
    addr: '경기도 김포시 고촌읍 수기로39-13',
  },
  { name: '독산한신아파트', units: '1,000세대 / 13동', addr: '서울시 금천구 한내로 62' },
  { name: '검단모아미래도엘리트아파트', units: '658세대 / 7동', addr: '인천 서구 서로3로 50' },
]

// 현재 탭
const activeTab = ref<'indoor' | 'tree' | 'tank'>('indoor')

// 탭별 현재 페이지
const pageByTab = ref({
  indoor: 1,
  tree: 1,
  tank: 1,
})

const PAGE_SIZE = 5

const currentList = computed(() => {
  if (activeTab.value === 'indoor') return indoor
  if (activeTab.value === 'tree') return tree
  return tank
})

const currentPage = computed({
  get: () => pageByTab.value[activeTab.value],
  set: (val: number) => {
    pageByTab.value[activeTab.value] = val
  },
})

const totalPages = computed(() => Math.ceil(currentList.value.length / PAGE_SIZE))

const pagedList = computed(() => {
  const start = (currentPage.value - 1) * PAGE_SIZE
  return currentList.value.slice(start, start + PAGE_SIZE)
})

const changeTab = (tab: 'indoor' | 'tree' | 'tank') => {
  activeTab.value = tab
  // 탭 바꿀 때 해당 탭 페이지 1로
  if (!pageByTab.value[tab]) {
    pageByTab.value[tab] = 1
  } else {
    pageByTab.value[tab] = 1
  }
}

const goPage = (p: number) => {
  if (p < 1 || p > totalPages.value) return
  currentPage.value = p
}
</script>

<template>
  <section id="projects" class="section bg-slate-50/60">
    <div class="container-x">
      <h2 class="text-2xl md:text-3xl font-semibold tracking-tight">회사실적</h2>
      <p class="text-slate-500 mt-2">주요 단지/건물 위생관리 이력</p>

      <!-- 탭 -->
      <div class="flex gap-2 mt-6 mb-4">
        <button
          class="px-4 py-2 rounded-lg text-sm font-medium"
          :class="
            activeTab === 'indoor' ? 'bg-blue-600 text-white' : 'bg-white border text-slate-700'
          "
          @click="changeTab('indoor')"
        >
          실내소독
        </button>
        <button
          class="px-4 py-2 rounded-lg text-sm font-medium"
          :class="
            activeTab === 'tree' ? 'bg-blue-600 text-white' : 'bg-white border text-slate-700'
          "
          @click="changeTab('tree')"
        >
          수목소독
        </button>
        <button
          class="px-4 py-2 rounded-lg text-sm font-medium"
          :class="
            activeTab === 'tank' ? 'bg-blue-600 text-white' : 'bg-white border text-slate-700'
          "
          @click="changeTab('tank')"
        >
          저수조청소
        </button>
      </div>

      <!-- 테이블 -->
      <div class="card-soft overflow-hidden">
        <table class="w-full text-left text-sm">
          <thead class="bg-slate-100/60 text-slate-700">
            <tr>
              <th class="py-3 px-4">현장명</th>
              <th class="py-3 px-4">세대/규모</th>
              <th class="py-3 px-4">주소</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in pagedList" :key="item.name" class="border-t border-slate-100/70">
              <td class="py-3.5 px-4 font-medium text-slate-900">{{ item.name }}</td>
              <td class="py-3.5 px-4 text-slate-700">{{ item.units }}</td>
              <td class="py-3.5 px-4 text-slate-500">{{ item.addr }}</td>
            </tr>
          </tbody>
        </table>
      </div>

      <!-- 페이지네이션 -->
      <div class="mt-4 flex items-center justify-between gap-4">
        <p class="text-xs text-slate-500">{{ currentPage }} / {{ totalPages }} 페이지</p>
        <div class="flex gap-2">
          <button
            class="px-3 py-1 rounded border text-sm"
            :class="currentPage === 1 ? 'opacity-40 cursor-not-allowed' : 'hover:bg-slate-100'"
            @click="goPage(currentPage - 1)"
            :disabled="currentPage === 1"
          >
            이전
          </button>
          <button
            v-for="p in totalPages"
            :key="p"
            class="px-3 py-1 rounded text-sm"
            :class="
              p === currentPage ? 'bg-blue-600 text-white' : 'bg-white border hover:bg-slate-100'
            "
            @click="goPage(p)"
          >
            {{ p }}
          </button>
          <button
            class="px-3 py-1 rounded border text-sm"
            :class="
              currentPage === totalPages ? 'opacity-40 cursor-not-allowed' : 'hover:bg-slate-100'
            "
            @click="goPage(currentPage + 1)"
            :disabled="currentPage === totalPages"
          >
            다음
          </button>
        </div>
      </div>
    </div>
  </section>
</template>
