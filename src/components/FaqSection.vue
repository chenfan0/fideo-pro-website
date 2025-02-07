<template>
  <div id="faq" class="py-16 px-4 max-w-4xl mx-auto">
    <h2
      class="text-4xl font-bold text-center mb-12 bg-gradient-to-r from-emerald-400 to-yellow-300 bg-clip-text text-transparent"
    >
      常见问题
    </h2>

    <div class="space-y-4">
      <div
        v-for="(faq, index) in faqs"
        :key="index"
        class="bg-gray-800 rounded-lg overflow-hidden border border-gray-700"
      >
        <button
          @click.stop="toggleFaq(index)"
          class="w-full p-4 text-left flex justify-between items-center hover:bg-gray-700/50 transition-colors"
        >
          <span class="text-white font-medium">{{ faq.question }}</span>
          <svg
            class="w-5 h-5 text-gray-400 transition-transform"
            :class="{ 'rotate-180': openIndex === index }"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M19 9l-7 7-7-7"
            />
          </svg>
        </button>

        <div
          v-show="openIndex === index"
          class="p-4 text-gray-300 border-t border-gray-700 bg-gray-800/50"
        >
          <template v-for="(item, itemIndex) in faq.content" :key="itemIndex">
            <!-- 普通文本 -->
            <template v-if="item.type === 'text'">
              {{ item.content }}
            </template>

            <!-- 链接 -->
            <a
              v-else-if="item.type === 'link'"
              :href="item.link"
              target="_blank"
              class="text-emerald-500 hover:text-emerald-400 transition-colors"
            >
              {{ item.content }}
            </a>

            <!-- 可复制的命令 -->
            <div
              v-else-if="item.type === 'copy'"
              class="flex items-center gap-2 bg-gray-900 p-2 rounded my-2"
            >
              <code class="flex-1">{{ item.content }}</code>
              <button
                @click="copyToClipboard(item.content)"
                class="p-1.5 hover:bg-gray-700 rounded transition-colors"
                title="复制到剪贴板"
              >
                <svg
                  class="w-4 h-4 text-gray-400"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M8 5H6a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2v-1M8 5a2 2 0 002 2h2a2 2 0 002-2M8 5a2 2 0 012-2h2a2 2 0 012 2m0 0h2a2 2 0 012 2v3m2 4H10m0 0l3-3m-3 3l3 3"
                  ></path>
                </svg>
              </button>
            </div>
          </template>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

interface FAQContent {
  type: "text" | "link" | "copy";
  content: string;
  link?: string;
}

interface FAQ {
  question: string;
  content: FAQContent[];
}

const faqs: FAQ[] = [
  {
    question: "Fideo 支持哪些直播平台？",
    content: [
      {
        type: "text",
        content:
          "Fideo 支持主流直播平台，包括 YouTube，Twitch，TikTok，Bigo，抖音，虎牙，哔哩哔哩，斗鱼，快手，小红书，Kwai，17Live, ACFun，网易cc，淘宝，京东，陌陌，克拉克拉，花椒，畅聊，微博等。",
      },
    ],
  },
  {
    question: "我应该下载哪个版本？",
    content: [
      {
        type: "text",
        content:
          "请根据您的操作系统选择对应的版本：\n\nMac系统：\n M1/M2芯片设备选择arm64版本\n Intel芯片设备选择x64版本\n\nWindows系统：\n 如果不确定CPU架构，建议选择x64版本\n 仅在使用搭载Windows on ARM的设备（如Surface Pro X）时，才需要选择arm64版本",
      },
    ],
  },
  {
    question: "检测分辨率变化有什么用？",
    content: [
      {
        type: "text",
        content:
          "有些直播平台会在直播过程中动态调整分辨率，这可能导致录制后视频花屏。开启分辨率变化检测，Fideo 会自动检测这些变化并重新开始录制，确保不会出现花屏效果",
      },
    ],
  },
  {
    question: "免费版和 Pro 版有什么区别？",
    content: [
      {
        type: "text",
        content:
          "免费版本是开源由社区维护可能更新不及时，Pro版本在免费版本所有功能基础上，会额外增加一些功能，比如一键开启，一键暂停，抖音弹幕录制，更多平台支持等等",
      },
    ],
  },
  {
    question: "Mac文件显示文件已损坏，无法打开，怎么办？",
    content: [
      {
        type: "text",
        content:
          "这是 macOS 的安全机制导致的，您可以通过打开命令行输入以下命令解决：",
      },
      {
        type: "copy",
        content: "sudo xattr -rd com.apple.quarantine /Applications/Fideo.app",
      },
    ],
  },
  {
    question: "Windows报病毒怎么办？",
    content: [
      {
        type: "text",
        content:
          "这是由于软件签名导致的，直接忽略即可。软件不会有任何病毒，请放心使用",
      },
    ],
  },
  {
    question: "下载时被浏览器屏蔽怎么办？",
    content: [
      {
        type: "text",
        content: "尝试使用其他浏览器",
      },
    ],
  },
  {
    question: "如何获取Cookie？",
    content: [
      {
        type: "link",
        content: "点击查看如何获取cookie",
        link: 'https://www.bilibili.com/video/BV1G24y1o75g/?spm_id_from=333.337.search-card.all.click&vd_source=7175c3866fe9ca259066ef7898056268'
      },
    ],
  },
  {
    question: '如何获取息知Key?',
    content: [
      {
        type: 'text',
        content: '息知Key是息知平台的API密钥，接收微信推送消息。请在息知平台获取息知Key。',
      },
      {
        type: 'link',
        content: '点击查看如何获取息知Key',
        link: 'https://xz.qqoq.net/#/index'
      },
    ],
  },
  {
    question: '为什么填写了息知Key，没有给我推送相关信息？',
    content: [
      {
        type: 'text',
        content: '只有在软件 最小化 的时候才会进行微信的推送，如果软件没有最小化，则不会进行推送。',
      },
      
    ],
  },
  
];

const openIndex = ref<number | null>(null);

const toggleFaq = (index: number) => {
  openIndex.value = openIndex.value === index ? null : index;
};

const copyToClipboard = async (text: string) => {
  try {
    await navigator.clipboard.writeText(text);
    // 这里可以添加复制成功的提示
  } catch (err) {
    console.error("复制失败:", err);
  }
};
</script>

<style scoped>
.rotate-180 {
  transform: rotate(180deg);
}
</style>
