<script setup lang="ts">
import { MessageCircle, MessageSquareText } from 'lucide-vue-next'
import logo from '@/assets/logo.png'
const year = new Date().getFullYear()

// 실제 링크 연결
const kakaoLink = 'https://pf.kakao.com/_nSxbxaG'
const smsLink = 'sms:010-4505-7575'
</script>

<template>
  <footer class="mt-16 border-t border-slate-200 bg-white">
    <div class="container-x py-10 grid gap-6 md:grid-cols-[1.2fr_0.8fr_0.8fr] items-start">
      <!-- 회사 정보 -->
      <div class="space-y-3">
        <div class="flex items-center gap-2">
          <p class="text-base font-semibold text-slate-900">
            <img :src="logo" alt="동진M&S 로고" class="h-8 w-auto" />
          </p>
        </div>
        <p class="text-sm text-slate-500 leading-6">
          위생·소독·저수조 청소 전문 업체<br />
          안전한 생활환경을 위한 정기관리 제공
        </p>
        <p class="text-xs text-slate-400">© {{ year }} Dongjin M&S. All rights reserved.</p>
      </div>

      <!-- 연락처 -->
      <div class="space-y-2 text-sm">
        <h3 class="text-sm font-semibold text-slate-900">Contact</h3>
        <p class="text-slate-500">Tel. 02-803-3355</p>
        <p class="text-slate-500">Mobile. 010-4505-7575</p>
        <p class="text-slate-500">Email. sky7090@naver.com</p>
      </div>

      <!-- 바로가기 -->
      <div class="space-y-2 text-sm">
        <h3 class="text-sm font-semibold text-slate-900">바로가기</h3>
        <ul class="space-y-1">
          <li><a href="#page-top" class="text-slate-500 hover:text-blue-600">홈</a></li>
          <li><a href="#services" class="text-slate-500 hover:text-blue-600">사업종목</a></li>
          <li><a href="#auth" class="text-slate-500 hover:text-blue-600">인허가</a></li>
          <li><a href="#projects" class="text-slate-500 hover:text-blue-600">회사실적</a></li>
          <li><a href="#contact" class="text-slate-500 hover:text-blue-600">문의</a></li>
        </ul>
      </div>
    </div>

    <!-- 하단 바 -->
    <div class="border-t border-slate-200/80 bg-slate-50">
      <div class="container-x py-3 flex flex-col md:flex-row gap-3 items-center justify-between">
        <p class="text-xs text-slate-400">
          사업자등록번호 119-86-60742 · 대표자 김동진 · 서울시 금천구 독산로 65길 2층
        </p>

        <!-- 오른쪽 아이콘 -->
        <div class="flex items-center gap-4">
          <a
            :href="kakaoLink"
            target="_blank"
            class="flex items-center gap-1 text-slate-500 hover:text-[#FAE100] transition"
            title="카카오톡 문의"
          >
            <MessageCircle class="w-4 h-4" />
            <span class="text-xs font-medium">카카오톡</span>
          </a>

          <a
            :href="smsLink"
            class="flex items-center gap-1 text-slate-500 hover:text-blue-600 transition"
            title="문자 문의"
          >
            <MessageSquareText class="w-4 h-4" />
            <span class="text-xs font-medium">문자</span>
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>
