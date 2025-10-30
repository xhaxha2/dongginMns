<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue'
import logo from '@/assets/logo.png'

const scrolled = ref(false)
const activeId = ref('page-top')
const isOpen = ref(false)

// ✅ 메뉴에 있는 섹션 전부 나열
const sections = ['page-top', 'services', 'auth', 'projects', 'contact']

let observer: IntersectionObserver | null = null

const onScroll = () => {
  scrolled.value = window.scrollY > 10
}

onMounted(() => {
  window.addEventListener('scroll', onScroll, { passive: true })

  observer = new IntersectionObserver(
    (entries) => {
      for (const entry of entries) {
        if (entry.isIntersecting) {
          activeId.value = entry.target.id
        }
      }
    },
    {
      threshold: 0.35,
      rootMargin: '-80px 0px -40% 0px',
    },
  )

  // 실제로 있는 섹션만 observe
  sections.forEach((id) => {
    const el = document.getElementById(id)
    if (el) observer?.observe(el)
  })
})

onBeforeUnmount(() => {
  window.removeEventListener('scroll', onScroll)
  observer?.disconnect()
})

// ✅ 클릭 시 바로 active + 스크롤 + 모바일 닫기
const goTo = (hash: string) => {
  const id = hash.replace('#', '')
  activeId.value = id
  isOpen.value = false

  const el = document.getElementById(id)
  if (el) {
    el.scrollIntoView({ behavior: 'smooth', block: 'start' })
  }
}
</script>

<template>
  <header
    :class="[
      'fixed top-0 inset-x-0 z-50 transition-all duration-300',
      scrolled
        ? 'bg-white/85 backdrop-blur border-b border-slate-200/80 shadow-sm'
        : 'bg-transparent',
    ]"
  >
    <div class="container-x h-14 md:h-16 flex items-center justify-between">
      <!-- 로고 -->
      <a
        href="#page-top"
        class="flex items-center gap-2 font-semibold text-slate-900"
        @click.prevent="goTo('#page-top')"
      >
        <img :src="logo" alt="동진M&S 로고" class="h-8 w-auto" />
      </a>

      <!-- 데스크톱 메뉴 -->
      <nav class="hidden md:flex gap-6 text-sm font-medium">
        <button
          type="button"
          @click="goTo('#page-top')"
          :class="
            activeId === 'page-top'
              ? 'text-blue-600 border-b-2 border-blue-600 pb-1'
              : 'text-slate-700 hover:text-blue-600'
          "
        >
          소개
        </button>
        <button
          type="button"
          @click="goTo('#services')"
          :class="
            activeId === 'services'
              ? 'text-blue-600 border-b-2 border-blue-600 pb-1'
              : 'text-slate-700 hover:text-blue-600'
          "
        >
          사업종목
        </button>
        <button
          type="button"
          @click="goTo('#auth')"
          :class="
            activeId === 'auth'
              ? 'text-blue-600 border-b-2 border-blue-600 pb-1'
              : 'text-slate-700 hover:text-blue-600'
          "
        >
          인허가
        </button>
        <button
          type="button"
          @click="goTo('#projects')"
          :class="
            activeId === 'projects'
              ? 'text-blue-600 border-b-2 border-blue-600 pb-1'
              : 'text-slate-700 hover:text-blue-600'
          "
        >
          회사실적
        </button>
        <button
          type="button"
          @click="goTo('#contact')"
          :class="
            activeId === 'contact'
              ? 'text-blue-600 border-b-2 border-blue-600 pb-1'
              : 'text-slate-700 hover:text-blue-600'
          "
        >
          문의
        </button>
      </nav>

      <!-- CTA -->
      <button
        type="button"
        class="hidden md:inline-flex px-4 py-2 rounded bg-blue-600 text-white text-sm hover:bg-blue-700 transition"
        @click="goTo('#contact')"
      >
        견적문의
      </button>

      <!-- 모바일 토글 -->
      <button
        class="md:hidden inline-flex items-center justify-center rounded-lg p-2 text-slate-700 hover:bg-slate-100"
        @click="isOpen = !isOpen"
        aria-label="메뉴 열기/닫기"
      >
        <span v-if="!isOpen">☰</span>
        <span v-else>✕</span>
      </button>
    </div>

    <!-- 모바일 메뉴 -->
    <div v-if="isOpen" class="md:hidden bg-white border-t border-slate-200/80">
      <div class="container-x py-3 flex flex-col gap-2 text-sm">
        <button
          class="text-left py-2"
          :class="activeId === 'page-top' ? 'text-blue-600 font-medium' : 'text-slate-700'"
          @click="goTo('#page-top')"
        >
          소개
        </button>
        <button
          class="text-left py-2"
          :class="activeId === 'services' ? 'text-blue-600 font-medium' : 'text-slate-700'"
          @click="goTo('#services')"
        >
          사업종목
        </button>
        <button
          class="text-left py-2"
          :class="activeId === 'auth' ? 'text-blue-600 font-medium' : 'text-slate-700'"
          @click="goTo('#auth')"
        >
          인허가
        </button>
        <button
          class="text-left py-2"
          :class="activeId === 'projects' ? 'text-blue-600 font-medium' : 'text-slate-700'"
          @click="goTo('#projects')"
        >
          회사실적
        </button>
        <button
          class="text-left py-2"
          :class="activeId === 'contact' ? 'text-blue-600 font-medium' : 'text-slate-700'"
          @click="goTo('#contact')"
        >
          문의
        </button>
        <button
          class="mt-2 inline-flex items-center justify-center rounded-lg bg-blue-600 text-white py-2"
          @click="goTo('#contact')"
        >
          견적문의
        </button>
      </div>
    </div>
  </header>
</template>
