<template>
  <div id="download" class="py-16 px-4 max-w-7xl mx-auto">
    <h2
      class="text-4xl font-bold text-center mb-12 bg-gradient-to-r from-emerald-400 to-yellow-300 bg-clip-text text-transparent"
    >
      选择您的下载版本
    </h2>

    <div class="grid md:grid-cols-2 gap-8 max-w-4xl mx-auto">
      <!-- 免费版 -->
      <div
        class="bg-gray-800 rounded-xl p-6 border border-gray-700 hover:border-emerald-500 transition-colors flex flex-col h-full"
      >
        <div class="flex justify-between items-start mb-4">
          <h3 class="text-2xl font-bold text-white">开源版</h3>
        </div>
        <ul class="space-y-3 mb-auto text-gray-300">
          <li class="flex items-center">
            <svg
              class="w-5 h-5 text-emerald-500 mr-2"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M5 13l4 4L19 7"
              ></path>
            </svg>
            基础录制功能
          </li>
          <li class="flex items-center">
            <svg
              class="w-5 h-5 text-emerald-500 mr-2"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M5 13l4 4L19 7"
              ></path>
            </svg>
            支持主流直播平台
          </li>
          <li class="flex items-center">
            <svg
              class="w-5 h-5 text-emerald-500 mr-2"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M5 13l4 4L19 7"
              ></path>
            </svg>
            社区支持
          </li>
          <li class="flex items-center">
            <svg
              class="w-5 h-5 text-emerald-500 mr-2"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M5 13l4 4L19 7"
              ></path>
            </svg>
            不定期更新
          </li>
        </ul>
        <a
          href="https://github.com/chenfan0/fideo-live-record/releases"
          target="_blank"
          class="block w-full text-center py-3 px-6 bg-emerald-500 hover:bg-emerald-600 text-white rounded-lg transition-colors mt-6"
        >
          前往 GitHub 下载
        </a>
      </div>

      <!-- 专业版 -->
      <div
        class="bg-gray-800 rounded-xl p-6 border border-gray-700 hover:border-emerald-500 transition-colors flex flex-col h-full"
      >
        <div class="flex justify-between items-start mb-4">
          <h3 class="text-2xl font-bold text-white">Pro版</h3>
        </div>
        <ul class="space-y-3 mb-auto text-gray-300">
          <li class="flex items-center">
            <svg
              class="w-5 h-5 text-emerald-500 mr-2"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M5 13l4 4L19 7"
              ></path>
            </svg>
            包含社区版所有功能
          </li>
          <li class="flex items-center">
            <svg
              class="w-5 h-5 text-emerald-500 mr-2"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M5 13l4 4L19 7"
              ></path>
            </svg>
            优先功能更新
          </li>
          <li class="flex items-center">
            <svg
              class="w-5 h-5 text-emerald-500 mr-2"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M5 13l4 4L19 7"
              ></path>
            </svg>
            专属技术支持
          </li>
          <li class="flex items-center">
            <svg
              class="w-5 h-5 text-emerald-500 mr-2"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M5 13l4 4L19 7"
              ></path>
            </svg>
            弹幕录制
          </li>
        </ul>

        <div class="mt-6">
          <div class="relative">
            <button
              @click.stop="isOpen = !isOpen"
              class="w-full p-3 bg-gray-700 text-white rounded-lg flex justify-between items-center hover:bg-gray-600 transition-colors"
            >
              <span>{{ "选择下载版本" }}</span>
              <svg
                class="w-5 h-5 transition-transform"
                :class="{ 'rotate-180': isOpen }"
                fill="none"
                stroke="currentColor"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M19 9l-7 7-7-7"
                ></path>
              </svg>
            </button>

            <!-- 下拉菜单 -->
            <div
              v-if="isOpen"
              @click.stop
              class="absolute w-full mt-2 bg-gray-700 rounded-lg shadow-lg overflow-hidden z-10 pb-2"
            >
              <div class="p-2 text-sm text-gray-400">Mac</div>
              <button
                @click="selectVersion('mac_arm')"
                class="w-[calc(100%-16px)] px-4 py-2 text-left text-white hover:bg-gray-600 transition-colors mx-2 rounded-lg"
              >
                Mac ARM64 (M1/M2)
              </button>
              <button
                @click="selectVersion('mac_x64')"
                class="w-[calc(100%-16px)] px-4 py-2 text-left text-white hover:bg-gray-600 transition-colors mx-2 rounded-lg"
              >
                Mac Intel
              </button>

              <div class="p-2 text-sm text-gray-400">Windows</div>
              <button
                @click="selectVersion('win_arm')"
                class="w-[calc(100%-16px)] px-4 py-2 text-left text-white hover:bg-gray-600 transition-colors mx-2 rounded-lg"
              >
                Windows ARM64
              </button>
              <button
                @click="selectVersion('win_x64')"
                class="w-[calc(100%-16px)] px-4 py-2 text-left text-white hover:bg-gray-600 transition-colors mx-2 rounded-lg"
              >
                Windows x64
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";

const baseUrl = import.meta.env.DEV ? 'http://localhost:12345' : 'https://api.fideo.site'

const isOpen = ref(false);

const selectVersion = (platform: string) => {
  isOpen.value = false;

  window.open(`${baseUrl}/api/download/fideo?platform=${platform}`, '_blank')
};

onMounted(() => {
  // 添加全局点击事件来关闭下拉菜单
  window.addEventListener("click", () => {
    isOpen.value = false;
  });
});
</script>
