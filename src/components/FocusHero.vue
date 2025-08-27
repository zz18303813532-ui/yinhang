<script setup>
import { computed } from 'vue'

const props = defineProps({
  bannerSrc: { type: String, default: '/hero.jpg' },
  items: {
    type: Array,
    default: () => ([
      { icon: 'fa-solid fa-user', label: '个人网银登录', bg: '#ffffff', color: '#333' },
      { icon: 'fa-solid fa-lock', label: '企业网银登录', bg: '#ffffff', color: '#333' },
      { icon: 'fa-solid fa-circle-nodes', label: '在线办理及费率', bg: '#ffa51e', color: '#fff' }
    ])
  }
})

const safeBanner = computed(() => props.bannerSrc || '/vite.svg')
</script>

<template>
  <section class="focus-hero">
    <div class="hero">
      <img class="hero-img" :src="safeBanner" alt="banner" />
      <div class="panel" role="group" aria-label="登录入口">
        <a v-for="(it, idx) in items" :key="idx" class="row" :style="{ background: it.bg, color: it.color }" href="javascript:void(0)">
          <i :class="it.icon"></i>
          <span class="label">{{ it.label }}</span>
        </a>
      </div>
    </div>
  </section>
</template>

<style scoped>

/* 英雄区：全屏宽度背景，响应式高度 */
.hero {
  position: relative;
  max-width: 1600px;
  margin: 0 auto;
  /* 使用viewport高度比例，实现响应式 */
  height: 40vh; /* 视口高度的40% */
  min-height: 300px; /* 最小高度保证可用性 */
  max-height: 400px; /* 最大高度避免过高 */
  border-radius: 0;
  overflow: hidden;
}
/* 主图还原为不偏移，铺满容器 */
.hero-img { width: 100%; height: 100%; object-fit: cover; display: block; }
/* 叠加面板：简单固定定位，确保对齐 */
.panel {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 149px;
  width: var(--brand-width-px, 320px);
  background: rgba(255,255,255,.45);
  box-shadow: 0 8px 24px rgba(0,0,0,.08);
  border-radius: 0;
  padding: 16px 12px;
  display: flex;
  flex-direction: column;
}
.row {
  display: flex;
  align-items: center;
  height: 66px;
  margin: 0 0 10px 0;
  border-radius: 6px;
  padding: 0 18px;
  font-size: 20px;
  text-decoration: none;
  transition: transform .15s ease, box-shadow .15s ease, filter .15s ease;
}
.row i { font-size: 28px; margin-right: 12px; }
.row:last-child { margin-bottom: 0; }
/* hover 只改背景色为绿色 */
.row:hover { 
  background-color: #21b69b !important; 
  color: #fff !important;
}
</style>