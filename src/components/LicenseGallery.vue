<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue'
import license1 from '@/assets/img/auth/나무병원.jpg'
import license2 from '@/assets/img/auth/사업자등록증_1.jpg'
import license3 from '@/assets/img/auth/사업자등록증_2.jpg'
import license4 from '@/assets/img/auth/사업자등록증_3.jpg'
import license5 from '@/assets/img/auth/소독업_신고증.jpg'
import license6 from '@/assets/img/auth/영업신고증.jpg'
import license7 from '@/assets/img/auth/저수조청소업_증명서.jpg'

const licenses = [
  {
    id: 'lic-001',
    name: '사업자 등록증',
    desc: '서울본사',
    src: license3,
  },
  {
    id: 'lic-002',
    name: '사업자 등록증',
    desc: '문경지점',
    src: license2,
  },
  {
    id: 'lic-003',
    name: '사업자 등록증',
    desc: '경북지사',
    src: license4,
  },
  {
    id: 'lic-004',
    name: '나무병원 등록증',
    desc: '공식적으로 인증된 법적 문서',
    src: license1,
  },
  {
    id: 'lic-005',
    name: '소독업 신고증',
    desc: '공식적으로 인증된 법적 문서',
    src: license5,
  },
  {
    id: 'lic-006',
    name: '영업 신고증',
    desc: '공식적으로 인증된 법적 문서',
    src: license6,
  },
  {
    id: 'lic-007',
    name: '저수조청소업 신고증',
    desc: '공식적으로 인증된 법적 문서',
    src: license7,
  },
]

const open = ref(false)
const selected = ref<(typeof licenses)[number] | null>(null)

function show(lic: (typeof licenses)[number]) {
  selected.value = lic
  open.value = true
}

function close() {
  open.value = false
  selected.value = null
}

// ESC로 닫기
const onKey = (e: KeyboardEvent) => {
  if (e.key === 'Escape') close()
}

onMounted(() => window.addEventListener('keydown', onKey))
onBeforeUnmount(() => window.removeEventListener('keydown', onKey))

// 슬라이드
const current = ref(0)
const visibleCount = 3 // md 이상에서 보여줄 카드 수
const next = () => {
  if (current.value < licenses.length - 1) current.value++
}
const prev = () => {
  if (current.value > 0) current.value--
}
</script>

<template>
  <section id="licenses" class="section">
    <div class="container-x">
      <div class="flex items-center justify-between gap-4 mb-6">
        <div>
          <h2 class="text-2xl md:text-3xl font-semibold tracking-tight">인허가 및 인증서</h2>
          <p class="text-slate-500 mt-2">클릭하면 원본 크기로 확인할 수 있습니다.</p>
        </div>
        <!-- 화살표 -->
        <div class="hidden md:flex gap-2">
          <button
            class="w-8 h-8 rounded-full border border-slate-200 flex items-center justify-center text-slate-600 hover:bg-slate-100 disabled:opacity-40"
            @click="prev"
            :disabled="current === 0"
            aria-label="이전"
          >
            ‹
          </button>
          <button
            class="w-8 h-8 rounded-full border border-slate-200 flex items-center justify-center text-slate-600 hover:bg-slate-100 disabled:opacity-40"
            @click="next"
            :disabled="current >= licenses.length - 1"
            aria-label="다음"
          >
            ›
          </button>
        </div>
      </div>

      <!-- 슬라이더 래퍼 -->
      <div class="relative">
        <!-- 모바일용 좌우 버튼 -->
        <div class="md:hidden flex justify-end gap-2 mb-3">
          <button
            class="w-8 h-8 rounded-full border border-slate-200 flex items-center justify-center text-slate-600 hover:bg-slate-100 disabled:opacity-40"
            @click="prev"
            :disabled="current === 0"
          >
            ‹
          </button>
          <button
            class="w-8 h-8 rounded-full border border-slate-200 flex items-center justify-center text-slate-600 hover:bg-slate-100 disabled:opacity-40"
            @click="next"
            :disabled="current >= licenses.length - 1"
          >
            ›
          </button>
        </div>

        <!-- 넘치는 카드 숨기고, translateX로 슬라이드 -->
        <div class="overflow-hidden">
          <div
            class="flex gap-6 transition-transform duration-300"
            :style="{
              transform: `translateX(-${current * (100 / visibleCount)}%)`,
            }"
          >
            <div
              v-for="lic in licenses"
              :key="lic.id"
              class="min-w-[85%] sm:min-w-[45%] md:min-w-[calc(100%/3-16px)] lg:min-w-[calc(100%/4-18px)]"
            >
              <button
                type="button"
                class="group relative rounded-2xl border border-slate-200/70 bg-white/70 backdrop-blur p-3 text-left shadow-sm hover:shadow-md transition w-full"
                @click="show(lic)"
              >
                <div class="aspect-[3/4] w-full overflow-hidden rounded-xl bg-slate-100">
                  <img
                    :src="lic.src"
                    :alt="lic.name"
                    class="h-full w-full object-cover transition group-hover:scale-[1.02]"
                    loading="lazy"
                  />
                </div>
                <div class="mt-4 space-y-1">
                  <p class="text-sm font-semibold text-slate-900 flex items-center gap-2">
                    {{ lic.name }}
                    <span
                      class="inline-flex items-center rounded-full bg-emerald-50 text-emerald-600 px-2 py-[2px] text-[10px]"
                    >
                      인증
                    </span>
                  </p>
                  <p class="text-xs text-slate-500">{{ lic.desc }}</p>
                </div>
                <div
                  class="pointer-events-none absolute right-3 top-3 rounded-full bg-white/80 px-2 py-1 text-[10px] text-slate-700 shadow-sm opacity-0 group-hover:opacity-100 transition"
                >
                  크게보기
                </div>
              </button>
            </div>
          </div>
        </div>
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
          class="relative max-w-3xl w-full max-h-[90vh] rounded-2xl bg-white shadow-2xl overflow-hidden"
        >
          <div
            class="flex items-center justify-between px-5 py-3 border-b border-slate-200 bg-slate-50/80"
          >
            <div>
              <h3 class="text-sm font-semibold text-slate-900">{{ selected?.name }}</h3>
              <p class="text-xs text-slate-500">{{ selected?.desc }}</p>
            </div>
            <button
              class="inline-flex items-center justify-center rounded-full bg-white w-7 h-7 border border-slate-200 text-slate-500 hover:text-slate-900"
              @click="close"
            >
              ✕
            </button>
          </div>
          <div class="p-4 bg-slate-100 flex items-center justify-center">
            <img
              v-if="selected"
              :src="selected.src"
              :alt="selected.name"
              class="max-h-[70vh] w-auto rounded-lg shadow-sm"
            />
          </div>
          <div
            class="px-5 py-3 bg-white text-[11px] text-slate-400 flex items-center justify-between"
          >
            <span>원본 해상도 제출 가능</span>
            <span class="text-slate-300">ESC로 닫기</span>
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
