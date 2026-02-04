<template>
  <div class="app">
    <header class="hero">
      <div>
        <p class="greeting">晚安，周先生</p>
        <h1 class="title">睡眠管家</h1>
      </div>
      <div class="sleep-score">
        <span>睡眠评分</span>
        <strong>89</strong>
      </div>
    </header>

    <main class="content">
      <section v-if="currentTab === 'home'" class="page">
        <div class="hero-card">
          <div>
            <p class="label">今晚入睡时间</p>
            <p class="time">23:10</p>
          </div>
          <div>
            <p class="label">预计起床</p>
            <p class="time">07:20</p>
          </div>
          <button class="primary">开始睡眠模式</button>
        </div>

        <h2 class="section-title">快速功能</h2>
        <div class="grid-nine">
          <button
            v-for="item in quickActions"
            :key="item.title"
            class="grid-card"
          >
            <span class="grid-icon">{{ item.icon }}</span>
            <span>{{ item.title }}</span>
          </button>
        </div>

        <div class="tip-banner">
          <span>💤</span>
          <p>睡前 30 分钟远离手机和强光，有助于提升深睡比例。</p>
        </div>
      </section>

      <section v-else-if="currentTab === 'plan'" class="page">
        <div class="section-header">
          <h2>睡眠计划</h2>
          <button class="link">设置目标</button>
        </div>
        <div class="plan-grid">
          <article v-for="plan in plans" :key="plan.title" class="plan-card">
            <div class="plan-icon">{{ plan.icon }}</div>
            <div>
              <h3>{{ plan.title }}</h3>
              <p>{{ plan.desc }}</p>
            </div>
          </article>
        </div>
        <div class="alarm-card">
          <div>
            <p class="label">智能闹钟</p>
            <p class="time">07:10 - 07:30</p>
          </div>
          <div class="toggle">
            <span>已开启</span>
            <span class="switch"></span>
          </div>
        </div>
      </section>

      <section v-else-if="currentTab === 'insights'" class="page">
        <h2 class="section-title">睡眠洞察</h2>
        <div class="insight-card">
          <div>
            <p class="label">本周平均睡眠时长</p>
            <p class="time">7小时36分</p>
          </div>
          <div class="progress">
            <div class="progress-bar" style="width: 76%"></div>
          </div>
          <p class="tip">建议本周再提前 20 分钟入睡，恢复深睡比例。</p>
        </div>
        <div class="insight-list">
          <div v-for="item in insights" :key="item.title" class="insight-item">
            <span class="dot"></span>
            <div>
              <h3>{{ item.title }}</h3>
              <p>{{ item.desc }}</p>
            </div>
          </div>
        </div>
      </section>

      <section v-else class="page">
        <h2 class="section-title">助眠空间</h2>
        <div class="sound-grid">
          <article v-for="sound in sounds" :key="sound.title" class="sound-card">
            <p class="sound-icon">{{ sound.icon }}</p>
            <h3>{{ sound.title }}</h3>
            <p>{{ sound.desc }}</p>
          </article>
        </div>
        <div class="profile-card">
          <div>
            <p class="label">我的睡眠偏好</p>
            <p class="time">轻柔白噪音 · 22°C</p>
          </div>
          <button class="primary ghost">编辑偏好</button>
        </div>
      </section>
    </main>

    <nav class="bottom-nav">
      <button
        v-for="item in tabs"
        :key="item.key"
        class="nav-item"
        :class="{ active: currentTab === item.key }"
        @click="currentTab = item.key"
      >
        <span>{{ item.icon }}</span>
        <span>{{ item.label }}</span>
      </button>
    </nav>
  </div>
</template>

<script setup>
import { ref } from "vue";

const currentTab = ref("home");

const tabs = [
  { key: "home", label: "首页", icon: "🏠" },
  { key: "plan", label: "计划", icon: "🗓️" },
  { key: "insights", label: "洞察", icon: "📈" },
  { key: "sounds", label: "助眠", icon: "🎧" },
];

const quickActions = [
  { title: "呼吸训练", icon: "🌿" },
  { title: "冥想", icon: "🧘" },
  { title: "夜间灯光", icon: "💡" },
  { title: "深睡追踪", icon: "🛌" },
  { title: "小憩", icon: "⏰" },
  { title: "情绪记录", icon: "📔" },
  { title: "白噪音", icon: "🌊" },
  { title: "睡前拉伸", icon: "🤸" },
  { title: "今日目标", icon: "🎯" },
];

const plans = [
  {
    title: "放松引导",
    desc: "5 分钟呼吸节奏，快速进入放松状态。",
    icon: "🌿",
  },
  {
    title: "轻断食提醒",
    desc: "距离入睡 2 小时停止进食。",
    icon: "🥗",
  },
  {
    title: "蓝光过滤",
    desc: "自动调整屏幕色温，保护褪黑素。",
    icon: "🌙",
  },
];

const sounds = [
  {
    title: "海浪",
    desc: "低频白噪音，帮助稳定心率。",
    icon: "🌊",
  },
  {
    title: "雨声",
    desc: "细雨背景，让大脑慢慢停机。",
    icon: "🌧️",
  },
  {
    title: "森林",
    desc: "微风与虫鸣，自然放松体验。",
    icon: "🌲",
  },
  {
    title: "壁炉",
    desc: "温暖火焰，减少夜晚焦虑。",
    icon: "🔥",
  },
];

const insights = [
  {
    title: "深睡不足",
    desc: "本周深睡比例偏低，睡前建议减少咖啡因。",
  },
  {
    title: "入睡波动",
    desc: "睡前使用手机时间增加 18 分钟。",
  },
  {
    title: "午后小憩",
    desc: "今日建议小憩 20 分钟保持清醒。",
  },
];
</script>

<style scoped>
:global(body) {
  margin: 0;
  font-family: "Inter", "PingFang SC", "Microsoft Yahei", sans-serif;
  background: #f5f6fb;
  color: #1f2a44;
}

.app {
  max-width: 480px;
  margin: 0 auto;
  padding: 24px 20px 110px;
}

.hero {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 16px;
}

.greeting {
  font-size: 14px;
  color: #5f6c87;
  margin: 0;
}

.title {
  margin: 4px 0 0;
  font-size: 28px;
}

.sleep-score {
  background: #ffffff;
  border-radius: 16px;
  padding: 12px 14px;
  text-align: right;
  box-shadow: 0 10px 20px rgba(20, 36, 86, 0.08);
  display: flex;
  flex-direction: column;
  gap: 4px;
  font-size: 12px;
}

.sleep-score strong {
  font-size: 20px;
}

.content {
  margin-top: 20px;
  display: grid;
  gap: 20px;
}

.page {
  display: grid;
  gap: 18px;
}

.hero-card {
  background: linear-gradient(135deg, #6d7bff, #88b2ff);
  border-radius: 24px;
  padding: 20px;
  color: #fff;
  display: grid;
  gap: 14px;
}

.section-title {
  margin: 0;
  font-size: 18px;
}

.label {
  font-size: 12px;
  margin: 0 0 6px;
  opacity: 0.8;
}

.time {
  font-size: 20px;
  margin: 0;
  font-weight: 600;
}

.primary {
  border: none;
  background: #ffffff;
  color: #4560ff;
  padding: 12px 16px;
  border-radius: 14px;
  font-weight: 600;
  font-size: 14px;
}

.primary.ghost {
  background: rgba(255, 255, 255, 0.2);
  color: #ffffff;
  border: 1px solid rgba(255, 255, 255, 0.4);
}

.grid-nine {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 12px;
}

.grid-card {
  background: #ffffff;
  border-radius: 18px;
  padding: 14px 10px;
  display: grid;
  gap: 8px;
  align-items: center;
  justify-items: center;
  border: none;
  box-shadow: 0 8px 16px rgba(20, 36, 86, 0.06);
  font-size: 12px;
  color: #4d5a78;
}

.grid-icon {
  font-size: 20px;
}

.tip-banner {
  background: #ffffff;
  border-radius: 18px;
  padding: 14px;
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 12px;
  align-items: center;
  box-shadow: 0 8px 16px rgba(20, 36, 86, 0.06);
  font-size: 13px;
  color: #4d5a78;
}

.section-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.section-header h2 {
  margin: 0;
  font-size: 18px;
}

.link {
  border: none;
  background: none;
  color: #5b75ff;
  font-size: 14px;
}

.plan-grid {
  display: grid;
  gap: 12px;
}

.plan-card {
  background: #ffffff;
  border-radius: 18px;
  padding: 14px;
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 12px;
  align-items: center;
  box-shadow: 0 8px 16px rgba(20, 36, 86, 0.06);
}

.plan-card h3 {
  margin: 0 0 4px;
  font-size: 16px;
}

.plan-card p {
  margin: 0;
  color: #5f6c87;
  font-size: 13px;
}

.plan-icon {
  width: 40px;
  height: 40px;
  background: #f0f3ff;
  border-radius: 12px;
  display: grid;
  place-items: center;
  font-size: 20px;
}

.alarm-card {
  background: #ffffff;
  border-radius: 18px;
  padding: 16px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0 8px 16px rgba(20, 36, 86, 0.06);
}

.toggle {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  gap: 6px;
  font-size: 12px;
  color: #5f6c87;
}

.switch {
  width: 42px;
  height: 22px;
  border-radius: 999px;
  background: #5b75ff;
  position: relative;
}

.switch::after {
  content: "";
  width: 18px;
  height: 18px;
  border-radius: 50%;
  background: #ffffff;
  position: absolute;
  top: 2px;
  right: 2px;
}

.sound-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 12px;
}

.sound-card {
  background: #ffffff;
  border-radius: 18px;
  padding: 14px;
  box-shadow: 0 8px 16px rgba(20, 36, 86, 0.06);
  display: grid;
  gap: 6px;
}

.sound-card h3 {
  margin: 0;
  font-size: 15px;
}

.sound-card p {
  margin: 0;
  color: #5f6c87;
  font-size: 12px;
}

.sound-icon {
  font-size: 22px;
  margin: 0;
}

.profile-card {
  background: linear-gradient(135deg, #4c5bff, #7aa1ff);
  border-radius: 20px;
  padding: 16px;
  color: #fff;
  display: grid;
  gap: 12px;
}

.insight-card {
  background: #ffffff;
  border-radius: 18px;
  padding: 14px;
  display: grid;
  gap: 10px;
  box-shadow: 0 8px 16px rgba(20, 36, 86, 0.06);
}

.progress {
  width: 100%;
  height: 8px;
  border-radius: 999px;
  background: rgba(86, 102, 255, 0.2);
  overflow: hidden;
}

.progress-bar {
  height: 100%;
  border-radius: 999px;
  background: #5b75ff;
}

.tip {
  margin: 0;
  font-size: 12px;
  color: #5f6c87;
}

.insight-list {
  display: grid;
  gap: 12px;
}

.insight-item {
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 10px;
  align-items: flex-start;
}

.insight-item h3 {
  margin: 0 0 4px;
  font-size: 14px;
}

.insight-item p {
  margin: 0;
  font-size: 12px;
  color: #5f6c87;
}

.dot {
  width: 10px;
  height: 10px;
  margin-top: 6px;
  border-radius: 50%;
  background: #5b75ff;
}

.bottom-nav {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  bottom: 16px;
  width: calc(100% - 32px);
  max-width: 480px;
  background: #ffffff;
  border-radius: 20px;
  padding: 10px 12px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 6px;
  box-shadow: 0 12px 24px rgba(20, 36, 86, 0.12);
}

.nav-item {
  border: none;
  background: none;
  display: grid;
  gap: 4px;
  justify-items: center;
  font-size: 11px;
  color: #6b7894;
}

.nav-item span:first-child {
  font-size: 18px;
}

.nav-item.active {
  color: #5b75ff;
  font-weight: 600;
}

@media (min-width: 540px) {
  .app {
    padding: 32px 24px 120px;
  }

  .sound-grid {
    grid-template-columns: repeat(3, minmax(0, 1fr));
  }
}
</style>
