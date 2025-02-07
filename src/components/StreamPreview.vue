<template>
  <header
    class="relative z-10 px-4 pt-16 md:pt-24 md:py-20 max-w-[1140px] mx-auto text-center overflow-hidden"
  >
    <section>
      <!-- 背景装饰 -->
      <div
        class="absolute left-1/2 top-1/2 -z-10 h-[400px] w-[800px] -translate-x-1/2 -translate-y-1/2 opacity-10 blur-[100px] bg-emerald-500"
      />

      <!-- 标题部分 -->
      <h1
        class="inline-flex flex-col gap-1 transition font-display text-6xl font-bold leading-none md:text-[8rem] bg-gradient-to-r from-20% bg-clip-text text-transparent from-emerald-400 to-yellow-300"
      >
        Fideo
      </h1>
      <p
        class="fideo-desc mx-auto w-full max-w-screen-sm text-sm leading-snug text-neutral-400 lg:pr-8 2xl:text-lg mt-4"
      >
        可一键录制主流直播间精彩内容。它支持实时监控直播间，支持检测分辨率变化，即刻自动重新录制，确保录制质量始终卓越。完美兼容
        Mac 与 Windows 系统，让你轻松畅享便捷录制体验。
      </p>
    </section>

    <!-- 平台图标滚动部分 -->
    <section
      class="overflow-hidden mt-8 md:mt-16 mx-auto max-w-[800px] make-mask px-4 md:px-10"
    >
      <div class="platforms-container">
        <div class="platforms flex gap-8 opacity-50 md:gap-16">
          <template v-for="platform in platforms" :key="platform.name">
            <a
              :href="platform.link"
              class="cursor-pointer"
              target="_blank"
              rel="noopener noreferrer"
            >
              <img
                :src="platform.icon"
                width="48"
                height="48"
                :alt="platform.name"
                class="min-w-[24px] md:min-w-[48px]"
              />
            </a>
          </template>
        </div>
        <div class="platforms flex gap-8 opacity-50 md:gap-16">
          <template
            v-for="platform in platforms"
            :key="`${platform.name}-clone`"
          >
            <a
              :href="platform.link"
              class="cursor-pointer"
              target="_blank"
              rel="noopener noreferrer"
            >
              <img
                :src="platform.icon"
                width="48"
                height="48"
                :alt="platform.name"
                class="min-w-[24px] md:min-w-[48px]"
              />
            </a>
          </template>
        </div>
      </div>
    </section>

    <!-- 输入框部分 -->
    <section class="flex gap-4 max-w-[800px] mx-auto mt-24">
      <div class="relative flex-1">
        <input
          v-model="streamUrl"
          type="text"
          class="w-full bg-transparent border-b border-neutral-700 px-4 py-2 text-white focus:outline-none focus:border-emerald-500 transition-colors"
          placeholder="请输入直播流地址"
        />
      </div>
      <button
        @click="handlePreview"
        class="px-6 py-2 bg-emerald-500 text-white rounded-lg hover:bg-emerald-600 transition-colors"
      >
        开始预览
      </button>
    </section>
  </header>

  <DPlayer
    v-if="isPreviewVisible"
    :stream-url="streamUrl"
    @close="handleClose"
  />
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from "vue";
import DPlayer from "./DPlayer.vue";

const platforms = [
  {
    name: "Youtube",
    icon: "/platforms/youtube.svg",
    link: "https://youtube.com",
  },
  { name: "Twitch", icon: "/platforms/twitch.svg", link: "https://twitch.tv" },
  {
    name: "Tiktok",
    icon: "/platforms/tiktok.svg",
    link: "https://www.tiktok.com/live/",
  },
  { name: "Bigo", icon: "/platforms/bigo.svg", link: "https://www.bigo.tv" },
  {
    name: "Douyin",
    icon: "/platforms/tiktok.svg",
    link: "https://live.douyin.com/",
  },
  { name: "Huya", icon: "/platforms/huya.svg", link: "https://www.huya.com" },
  {
    name: "Bilibili",
    icon: "/platforms/bilibili.svg",
    link: "https://live.bilibili.com/",
  },
  {
    name: "Douyu",
    icon: "/platforms/douyu.svg",
    link: "https://www.douyu.com/",
  },
  {
    name: "Kuaishou",
    icon: "/platforms/kuaishou.svg",
    link: "https://live.kuaishou.com/",
  },
  {
    name: "Weibo",
    icon: "/platforms/weibo.svg",
    link: "https://weibo.com/l/wblive/p/show/1022:2321325052506609680949",
  },
];

const streamUrl = ref("");
const isPreviewVisible = ref(false);

const handlePreview = () => {
  if (!streamUrl.value.trim()) return;
  isPreviewVisible.value = true;
};

const handleClose = () => {
  isPreviewVisible.value = false;
};

onMounted(() => {
  // 初始化：检查 URL 参数
  const urlParams = new URLSearchParams(window.location.search);
  const initialStreamUrl = urlParams.get("streamUrl");
  if (initialStreamUrl) {
    streamUrl.value = initialStreamUrl;
    isPreviewVisible.value = true;
  }
});
</script>

<style scoped>
.make-mask {
  mask-image: linear-gradient(
    to right,
    transparent,
    black 20%,
    black 80%,
    transparent
  );
  -webkit-mask-image: linear-gradient(
    to right,
    transparent,
    black 20%,
    black 80%,
    transparent
  );
}

.platforms-container {
  display: flex;
  width: fit-content;
  gap: 0;
}

.platforms {
  display: flex;
  gap: 32px;
  padding-right: 32px;
}

@media (min-width: 768px) {
  .platforms {
    gap: 48px;
    padding-right: 48px;
  }
}

@keyframes scroll {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-50%);
  }
}

.platforms-container {
  animation: scroll 20s linear infinite;
}

.platforms-container:hover {
  animation-play-state: paused;
}
</style>
