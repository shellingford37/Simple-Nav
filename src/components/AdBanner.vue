<template>
  <div class="divider-container">
    <!-- 图片模式 -->
    <img
      v-if="imageUrl"
      :src="imageUrl"
      alt="分隔广告"
      class="h-full w-full object-cover object-center rounded-lg"
    >
    <!-- 分隔线模式 -->
    <div v-else class="divider-line">
      <div class="divider-gradient"></div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    imageUrl: {
      type: String,
      default: ''  // 替换为实际图片URL（如https://example.com/banner.jpg）
    },
    content: {
      type: String,
      default: ''  // 不再显示文字
    }
  }
}
</script>

<style scoped>
.divider-container {
  width: 100%;
  height: 2px;
  position: relative;
  padding: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}

.divider-line {
  width: 100%;
  height: 100%;
  position: relative;
  overflow: hidden;
}

.divider-gradient {
  width: 100%;
  height: 100%;
  background: linear-gradient(
    90deg,
    transparent 0%,
    rgba(203, 213, 225, 0.3) 15%,
    rgba(203, 213, 225, 0.6) 50%,
    rgba(203, 213, 225, 0.3) 85%,
    transparent 100%
  );
  animation: shimmer 3s ease-in-out infinite;
}

/* 暗黑模式下的渐变色 */
:global(.dark) .divider-gradient {
  background: linear-gradient(
    90deg,
    transparent 0%,
    rgba(71, 85, 105, 0.3) 15%,
    rgba(71, 85, 105, 0.6) 50%,
    rgba(71, 85, 105, 0.3) 85%,
    transparent 100%
  );
}

/* 添加微妙的闪烁动画 */
@keyframes shimmer {
  0%, 100% {
    opacity: 1;
  }
  50% {
    opacity: 0.6;
  }
}

/* 图片模式的样式 */
img {
  transition: transform 0.3s ease;
}

img:hover {
  transform: scale(1.02);
}
</style>