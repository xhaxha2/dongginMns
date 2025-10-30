<script setup lang="ts">
import mainBannerImg from '@/assets/img/header.jpg'
</script>

<template>
  <section
    id="page-top"
    class="pt-24 md:pt-32 pb-16 bg-gradient-to-b from-slate-50 via-white to-slate-50/30"
  >
    <div class="container-x grid md:grid-cols-2 gap-10 items-center">
      <div class="space-y-6">
        <span
          class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-blue-50 text-blue-700 text-xs font-medium"
        >
          위생·소독·저수조 전문
        </span>
        <h1 class="text-2xl md:text-2xl font-bold tracking-tight leading-tight">
          성실과 친절로 고객에게 다가가는 기업<br class="hidden md:block" />
          <span class="text-blue-600">동진엠엔에스</span>
        </h1>
        <p class="text-slate-800 md:text-sm leading-7">
          주식회사 동진엠엔에스는<strong>도시와 인류의 조화로운 주거문화 창조</strong>를 목표로
          탄생했으며, 쾌적 하고 위생적인 도시 주거문화의 새로운 패러다임을 제공하며 항상 고객의
          입장에서 최선을 다하고 있습니다. 또한 저희 회사는
          <strong>인간중심, 절대친절, 인화단결</strong>을 사훈으로 임직원이 일체가 되어 자만하지
          않고 최고의 위치를 향하여 노력하고 있으며 고객의 재산이 곧 나의 것이라는
          <strong>주인의식과 선량한 관리자로서의 사명감으로 임하고 있습니다.</strong> 아무쪼록 당
          사에 대한 사업체 대표님, 입주자 대표님들께 진심으로 감사하게 생각하면서 여러분의 다양한
          목소리에 적극 부응하여 고객이 감동할 수 있도록
          <strong>최고의 서비스와 긍지를 가지고 무한책임의식으로 보답하겠습니다</strong>.감사합니다.
        </p>
        <div class="flex flex-wrap gap-3">
          <a
            href="#contact"
            class="px-5 py-3 rounded-xl bg-blue-600 text-white font-medium shadow-sm hover:bg-blue-700"
          >
            견적 문의
          </a>
          <a
            href="#projects"
            class="px-5 py-3 rounded-xl bg-white border border-slate-200 text-slate-800 hover:bg-slate-50"
          >
            회사 실적
          </a>
        </div>
      </div>
      <div class="card-soft p-3 md:p-4">
        <img :src="mainBannerImg" class="rounded-xl w-full h-60 object-cover" alt="작업 현장" />
      </div>
    </div>
  </section>
</template>
