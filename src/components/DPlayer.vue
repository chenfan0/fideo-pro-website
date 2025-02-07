<template>
  <div
    class="fixed top-0 left-0 w-[100vw] h-[100vh] flex justify-center items-center z-[999] bg-[rgba(0,0,0,0.5)]"
  >
    <div
      class="rounded-lg w-[80vw] h-[80vh] border-[rgba(255,255,255,0.8)] border-2 overflow-hidden"
      ref="playerRef"
    />
    <img
      src="/close.svg"
      alt="close"
      class="absolute top-6 right-6 w-10 h-10 cursor-pointer"
      @click="$emit('close')"
    />
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from "vue";

const props = defineProps<{
  streamUrl: string;
}>();

defineEmits<{
  (e: "close"): void;
}>();

const playerRef = ref<HTMLElement | null>(null);
let dp: any = null;

const loadScript = (url: string): Promise<void> => {
  return new Promise((resolve, reject) => {
    if (document.querySelector(`script[src="${url}"]`)) {
      resolve();
      return;
    }

    const script = document.createElement("script");
    script.src = url;
    script.onload = () => resolve();
    script.onerror = reject;
    document.head.appendChild(script);
  });
};

const initializePlayer = async () => {
  if (!playerRef.value) return;

  await Promise.all([
    loadScript("https://cdn.jsdelivr.net/npm/dplayer/dist/DPlayer.min.js"),
    loadScript("https://cdn.jsdelivr.net/npm/flv.js/dist/flv.min.js"),
    loadScript("https://cdn.jsdelivr.net/npm/hls.js/dist/hls.min.js"),
  ]);

  // @ts-ignore
  dp = new window.DPlayer({
    container: playerRef.value,
    video: {
      url: props.streamUrl,
    },
  });

  dp.play();
};

onMounted(() => {
  initializePlayer();
});

onBeforeUnmount(() => {
  if (dp) {
    dp.destroy();
  }
});
</script>
