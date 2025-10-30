<script setup lang="ts">
import { onBeforeUnmount, ref, watch } from 'vue'
const treeImages = Object.values(
  import.meta.glob('@/assets/img/수목소독/*.jpg', { eager: true, import: 'default' }),
) as string[]
const indoorImages = Object.values(
  import.meta.glob('@/assets/img/실내소독/*.jpg', { eager: true, import: 'default' }),
) as string[]
const tankImages = Object.values(
  import.meta.glob('@/assets/img/저수조청소/*.jpg', { eager: true, import: 'default' }),
) as string[]

// 서비스 데이터: 각각 여러 장의 이미지
const services = [
  {
    id: 'tree',
    icon: '🌳',
    title: '수목소독',
    desc: '계절별 병해충 방제, 영양관리',
    images: treeImages,
  },
  {
    id: 'indoor',
    icon: '🏢',
    title: '실내소독',
    desc: '공동주택/상가/빌딩 위생 소독',
    images: indoorImages,
  },
  {
    id: 'tank',
    icon: '🚰',
    title: '저수조 청소',
    desc: '위생기준에 맞춘 세척·살균',
    images: tankImages,
  },
]
const open = ref(false)
const selected = ref<(typeof services)[number] | null>(null)

const show = (item: (typeof services)[number]) => {
  selected.value = item
  open.value = true
}
const close = () => {
  open.value = false
  // selected는 닫힐 때 살짝 늦게 지워도 됨
  setTimeout(() => (selected.value = null), 200)
}

// ✅ 모달 열릴 때 body 스크롤 잠그기
const originalOverflow = ref<string>('')

watch(open, (value) => {
  if (value) {
    originalOverflow.value = document.body.style.overflow
    document.body.style.overflow = 'hidden'
  } else {
    document.body.style.overflow = originalOverflow.value || ''
  }
})

// 혹시 컴포넌트가 사라질 때 열려 있었으면 원복
onBeforeUnmount(() => {
  document.body.style.overflow = originalOverflow.value || ''
})
</script>

<template>
  <section id="services" class="section">
    <div class="container-x">
      <div class="flex items-center justify-between gap-4">
        <div>
          <h2 class="text-2xl md:text-3xl font-semibold tracking-tight">사업종목</h2>
          <p class="text-slate-500 mt-2">수목소독 · 실내소독 · 저수조 청소</p>
        </div>
      </div>

      <div class="mt-10 grid gap-6 md:grid-cols-3">
        <article
          v-for="svc in services"
          :key="svc.id"
          class="card-soft p-6 hover:-translate-y-1 hover:shadow-md transition cursor-pointer"
          @click="show(svc)"
        >
          <div class="text-3xl mb-3">{{ svc.icon }}</div>
          <h3 class="text-lg font-semibold">{{ svc.title }}</h3>
          <p class="text-sm text-slate-600 mt-2">{{ svc.desc }}</p>
          <p class="text-xs text-blue-500 mt-4 inline-flex items-center gap-1">갤러리 보기 →</p>
        </article>
      </div>
    </div>

    <!-- 모달 -->
    <transition name="fade">
      <div
        v-if="open"
        class="fixed inset-0 z-[999] flex items-center justify-center bg-black/50 backdrop-blur-sm px-4"
        @click.self="close"
      >
        <div
          class="relative w-full max-w-5xl max-h-[90vh] overflow-y-auto rounded-2xl bg-white shadow-2xl"
        >
          <!-- 헤더 -->
          <div
            class="sticky top-0 z-10 flex items-center justify-between px-6 py-4 border-b border-slate-200 bg-slate-50/90 backdrop-blur"
          >
            <div>
              <h3 class="text-base font-semibold text-slate-900">{{ selected?.title }}</h3>
              <p class="text-xs text-slate-500">{{ selected?.desc }}</p>
            </div>
            <button
              class="inline-flex items-center justify-center w-8 h-8 rounded-full border border-slate-200 bg-white text-slate-500 hover:text-slate-900"
              @click="close"
            >
              ✕
            </button>
          </div>

          <!-- 이미지 그리드 -->
          <div class="p-6 grid gap-4 sm:grid-cols-2 md:grid-cols-3">
            <div
              v-for="(img, index) in selected?.images"
              :key="index"
              class="rounded-xl overflow-hidden border border-slate-200 bg-slate-50 hover:shadow-md transition"
            >
              <img
                :src="img"
                :alt="selected?.title"
                class="w-full h-60 object-cover hover:scale-[1.03] transition-transform"
                loading="lazy"
              />
            </div>
          </div>

          <!-- 푸터 -->
          <div
            class="px-6 py-3 border-t border-slate-200 bg-white text-[11px] text-slate-400 flex items-center justify-between"
          >
            <span>현장 이미지 예시 (무단복제 금지)</span>
            <span class="text-slate-300">배경 클릭 or ✕ 닫기</span>
          </div>
        </div>
      </div>
    </transition>
  </section>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.15s ease-out;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
