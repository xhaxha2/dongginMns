<script setup lang="ts">
import { reactive, ref } from 'vue'

const form = reactive({
  name: '',
  phone: '',
  email: '',
  buildingType: '아파트',
  area: '',
  message: '',
  agree: false,
})
const errors = ref<string[]>([])
const done = ref(false)
const ticket = ref('')

function validate() {
  errors.value = []

  if (!form.name.trim()) errors.value.push('이름을 입력해주세요.')
  const phoneNum = form.phone.replace(/[^0-9]/g, '')
  if (phoneNum.length < 9) errors.value.push('연락처를 정확히 입력해주세요.')
  if (form.email && !/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.email)) {
    errors.value.push('이메일 형식이 올바르지 않습니다.')
  }
  if (!form.agree) errors.value.push('개인정보 수집·이용에 동의해주세요.')

  return errors.value.length === 0
}

async function submit() {
  if (!validate()) return

  try {
    const res = await fetch('https://formspree.io/f/meopzadg', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(form),
    })

    if (!res.ok) throw new Error()

    ticket.value =
      'DJ-' +
      Math.floor(Math.random() * 999999)
        .toString()
        .padStart(6, '0')
    done.value = true
    Object.assign(form, {
      name: '',
      phone: '',
      email: '',
      buildingType: '아파트',
      area: '',
      message: '',
      agree: false,
    })
  } catch {
    errors.value = ['전송에 실패했습니다.']
  }
  // 폼 비우기
  // Object.assign(form, { name:'', phone:'', email:'', buildingType:'아파트', area:'', message:'', agree:false })
}
</script>

<template>
  <section id="contact" class="section">
    <div class="container-x grid md:grid-cols-2 gap-10 items-start">
      <!-- 왼쪽 안내 -->
      <div class="space-y-4">
        <h2 class="text-2xl md:text-3xl font-semibold tracking-tight">문의하기</h2>
        <p class="text-slate-500">현장 정보와 연락처만 남겨주시면 담당자가 확인 후 연락드립니다.</p>

        <ul class="text-sm text-slate-500 space-y-2">
          <li>• 영업시간: 평일 09:00 ~ 17:00</li>
          <li>• 서비스 지역: 수도권(서울/경기/인천)</li>
          <li>• 긴급 소독/저수조는 전화 문의 권장</li>
        </ul>

        <div
          class="inline-flex items-center gap-2 rounded-full bg-emerald-50 text-emerald-700 px-4 py-2 text-sm"
        >
          <span class="h-2 w-2 rounded-full bg-emerald-500"></span>
          지금 문의 시, 오늘 중 1차 회신 (업무시간 기준)
        </div>

        <p v-if="done" class="text-sm text-slate-400">
          문의번호 <span class="font-mono text-slate-600">{{ ticket }}</span> 로 접수되었습니다.
        </p>
      </div>

      <!-- 오른쪽 폼 -->
      <form class="card-soft p-6 space-y-4" @submit.prevent="submit">
        <input text="문의번호" type="hidden" :value="ticket" />
        <!-- 에러 박스 -->
        <div v-if="errors.length" class="rounded-xl bg-red-50 border border-red-100 p-3 space-y-1">
          <p class="text-sm font-medium text-red-700">입력값을 확인해주세요.</p>
          <ul class="text-xs text-red-600 list-disc ml-4">
            <li v-for="e in errors" :key="e">{{ e }}</li>
          </ul>
        </div>

        <!-- 현장정보 -->
        <div class="grid md:grid-cols-2 gap-4">
          <label class="text-sm space-y-1">
            <span>현장 유형</span>
            <select
              v-model="form.buildingType"
              class="w-full rounded-lg border border-slate-200 px-3 py-2 focus:outline-none focus:ring-2 focus:ring-blue-500"
            >
              <option value="아파트">아파트</option>
              <option value="빌딩">빌딩/오피스</option>
              <option value="상가">상가/창고</option>
              <option value="기타">기타</option>
            </select>
          </label>
          <label class="text-sm space-y-1">
            <span>면적/세대수 (선택)</span>
            <input
              v-model="form.area"
              type="text"
              placeholder="예: 1,200세대 / 500평"
              class="w-full rounded-lg border border-slate-200 px-3 py-2 focus:ring-2 focus:ring-blue-500"
            />
          </label>
        </div>

        <!-- 연락처 -->
        <div class="grid md:grid-cols-2 gap-4">
          <label class="text-sm space-y-1">
            <span>이름 *</span>
            <input
              v-model="form.name"
              type="text"
              autocomplete="name"
              class="w-full rounded-lg border border-slate-200 px-3 py-2 focus:ring-2 focus:ring-blue-500"
              placeholder="홍길동"
            />
          </label>
          <label class="text-sm space-y-1">
            <span>연락처 *</span>
            <input
              v-model="form.phone"
              type="tel"
              autocomplete="tel"
              class="w-full rounded-lg border border-slate-200 px-3 py-2 focus:ring-2 focus:ring-blue-500"
              placeholder="01012341234"
            />
          </label>
        </div>

        <label class="text-sm space-y-1">
          <span>이메일 (선택)</span>
          <input
            v-model="form.email"
            type="email"
            autocomplete="email"
            class="w-full rounded-lg border border-slate-200 px-3 py-2 focus:ring-2 focus:ring-blue-500"
            placeholder="you@example.com"
          />
        </label>

        <!-- 문의내용 -->
        <label class="text-sm space-y-1">
          <span>문의 내용</span>
          <textarea
            v-model="form.message"
            rows="4"
            placeholder="예: 000아파트 저수조 청소 견적 요청 / 희망 일정 11월 5일 이후"
            class="w-full rounded-lg border border-slate-200 px-3 py-2 focus:ring-2 focus:ring-blue-500"
          ></textarea>
        </label>

        <!-- 약관 -->
        <label class="flex items-start gap-2 text-sm text-slate-600">
          <input
            v-model="form.agree"
            type="checkbox"
            class="mt-1 rounded border-slate-300 text-blue-600 focus:ring-blue-500"
          />
          <span>
            개인정보 수집·이용에 동의합니다.
            <span class="text-slate-400 text-xs block"
              >문의 응대 후 일정 기간 보관될 수 있습니다.</span
            >
          </span>
        </label>

        <button
          type="submit"
          class="w-full py-3 rounded-lg bg-blue-600 text-white font-medium hover:bg-blue-700 transition disabled:opacity-50"
          :disabled="done"
        >
          {{ done ? '접수되었습니다' : '문의 보내기' }}
        </button>
      </form>
    </div>
  </section>
</template>
