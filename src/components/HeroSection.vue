<script setup lang="ts">
import mainBannerImg from '@/assets/img/header.jpg'
</script>

<template>
  <section id="page-top" class="relative overflow-hidden pt-24 md:pt-32 pb-20 bg-slate-950">
    <!-- 배경 그라데이션 레이어 -->
    <div
      class="pointer-events-none absolute inset-0 bg-[radial-gradient(circle_at_top,_rgba(59,130,246,0.35),_rgba(15,23,42,0))]"
    ></div>
    <div
      class="pointer-events-none absolute -right-36 top-10 h-72 w-72 rounded-full bg-sky-400/10 blur-3xl"
    ></div>
    <div
      class="pointer-events-none absolute -left-10 bottom-0 h-72 w-72 rounded-full bg-cyan-300/10 blur-3xl"
    ></div>

    <div class="container-x relative z-10 grid gap-10 lg:grid-cols-[1.1fr_0.9fr] items-center">
      <!-- LEFT -->
      <div class="space-y-7 text-white/90">
        <!-- 작은 배지 -->
        <div
          class="inline-flex items-center gap-2 rounded-full bg-white/5 border border-white/10 px-3 py-1 text-xs text-sky-100 backdrop-blur"
        >
          <span class="h-1.5 w-1.5 rounded-full bg-emerald-400 animate-pulse"></span>
          위생·소독·저수조 전문 기업
        </div>

        <!-- 헤드라인 -->
        <div>
          <h1 class="text-3xl md:text-4xl font-semibold tracking-tight leading-tight">
            성실함과 기술력으로<br />
            <span class="text-sky-200">주거 위생 환경을 설계합니다.</span>
          </h1>
          <p class="mt-4 text-sm md:text-base text-slate-200/80 leading-relaxed max-w-xl">
            동진엠엔에스는 도시·건축 공간의 위생성과 안정성을 높이는 서비스에 집중해 왔습니다.
            저수조 청소, 실내 소독, 수목 소독까지 하나의 흐름으로 제공하여 관리자의
            <strong class="text-slate-50/90 font-medium"
              >관리 부담을 줄이고, 안전 기준을 맞추는 것</strong
            >을 목표로 합니다.
          </p>
        </div>

        <!-- CTA -->
        <div class="flex flex-wrap gap-3">
          <a
            href="#contact"
            class="inline-flex items-center gap-2 rounded-lg bg-sky-400 text-slate-950 font-medium px-5 py-3 shadow-lg shadow-sky-400/30 hover:bg-sky-300 transition"
          >
            견적 문의하기
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="w-4 h-4"
              fill="none"
              viewBox="0 0 24 24"
              stroke="currentColor"
              stroke-width="1.8"
            >
              <path stroke-linecap="round" stroke-linejoin="round" d="M5 12h14m-7-7l7 7-7 7" />
            </svg>
          </a>
          <a
            href="#projects"
            class="inline-flex items-center gap-2 rounded-lg border border-white/15 text-slate-100 px-5 py-3 hover:border-white/40 transition"
          >
            회사 실적 보기
          </a>
        </div>

        <!-- 하단 스펙/신뢰 -->
        <div class="flex gap-6 pt-3 text-xs md:text-sm text-slate-200/60">
          <div>
            <p class="text-slate-100 font-semibold">15년+</p>
            <p>현장 경험</p>
          </div>
          <div>
            <p class="text-slate-100 font-semibold">아파트</p>
            <p>정기 위생 관리</p>
          </div>
          <div>
            <p class="text-slate-100 font-semibold">원칙</p>
            <p>CS 대응</p>
          </div>
        </div>
      </div>

      <!-- RIGHT -->
      <div class="relative">
        <!-- 글라스 카드 -->
        <div
          class="rounded-2xl border border-white/10 bg-white/5 backdrop-blur-xl p-4 md:p-5 shadow-2xl animate-float-soft"
        >
          <div class="rounded-xl overflow-hidden bg-slate-900/50 aspect-[4/3]">
            <img :src="mainBannerImg" alt="작업 현장" class="w-full h-full object-cover" />
          </div>

          <!-- 오버레이 정보 -->
          <div class="mt-4 flex items-center justify-between gap-4">
            <div>
              <p class="text-xs text-slate-200/70">현재 진행중</p>
              <p class="text-sm text-slate-50 font-medium">저수조 청소ㆍ소독 패키지</p>
            </div>
            <span
              class="rounded-full bg-emerald-400/10 text-emerald-200 text-[10px] px-3 py-1 border border-emerald-300/20"
            >
              안전 기준 준수
            </span>
          </div>
        </div>

        <!-- 옆의 작은 카드 -->
        <div
          class="hidden md:flex flex-col gap-2 absolute -right-10 top-10 bg-slate-900/70 border border-white/5 rounded-2xl px-4 py-3 backdrop-blur-lg w-40"
        >
          <p class="text-[10px] uppercase tracking-wide text-slate-200/60">service rate</p>
          <p class="text-2xl font-semibold text-white leading-none">98.4%</p>
          <p class="text-[11px] text-slate-200/70">고객 만족도</p>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
@keyframes float-soft {
  0% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-5px);
  }
  100% {
    transform: translateY(0);
  }
}
.animate-float-soft {
  animation: float-soft 5s ease-in-out infinite;
}
</style>
