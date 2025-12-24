<template>
  <div class="divider-container" :class="{'category-divider': type === 'category', 'count-divider': type === 'count'}">
    <!-- 图片模式 -->
    <img
      v-if="imageUrl"
      :src="imageUrl"
      alt="分隔广告"
      class="h-full w-full object-cover object-center rounded-lg"
    >
    <!-- 分组分隔线：带组名 -->
    <div v-else-if="type === 'category'" class="category-divider-line">
      <div class="divider-line-part"></div>
      <div class="category-label">
        <span class="category-text">{{ categoryName }}</span>
      </div>
      <div class="divider-line-part"></div>
    </div>
    <!-- 数量分隔线：简单虚线 -->
    <div v-else class="count-divider-line">
      <div class="dashed-line"></div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    imageUrl: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: 'count', // 'category' 或 'count'
      validator: (value) => ['category', 'count'].includes(value)
    },
    categoryName: {
      type: String,
      default: ''
    },
    content: {
      type: String,
      default: ''
    }
  }
}
</script>

<style scoped>
/* 容器基础样式 */
.divider-container {
  width: 100%;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
}

.divider-container.category-divider {
  height: auto;
  padding: 1.5rem 0;
}

.divider-container.count-divider {
  height: 1px;
  padding: 1rem 0;
}

/* ============ 分组分隔线样式（带组名）============ */
.category-divider-line {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1rem;
}

.divider-line-part {
  flex: 1;
  height: 2px;
  background: linear-gradient(
    90deg,
    transparent 0%,
    rgba(99, 102, 241, 0.4) 50%,
    transparent 100%
  );
  position: relative;
  overflow: hidden;
}

.divider-line-part::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(99, 102, 241, 0.6),
    transparent
  );
  animation: slide 3s ease-in-out infinite;
}

@keyframes slide {
  0% {
    left: -100%;
  }
  50% {
    left: 100%;
  }
  100% {
    left: 100%;
  }
}

.category-label {
  flex-shrink: 0;
  padding: 0.5rem 1.5rem;
  background: linear-gradient(135deg, rgba(99, 102, 241, 0.1), rgba(139, 92, 246, 0.1));
  border: 1px solid rgba(99, 102, 241, 0.3);
  border-radius: 9999px;
  backdrop-filter: blur(8px);
  box-shadow: 0 2px 8px rgba(99, 102, 241, 0.1);
}

.category-text {
  font-size: 0.875rem;
  font-weight: 600;
  color: #6366f1;
  letter-spacing: 0.05em;
  text-transform: uppercase;
}

/* 暗黑模式 - 分组分隔线 */
:global(.dark) .divider-line-part {
  background: linear-gradient(
    90deg,
    transparent 0%,
    rgba(139, 92, 246, 0.4) 50%,
    transparent 100%
  );
}

:global(.dark) .divider-line-part::before {
  background: linear-gradient(
    90deg,
    transparent,
    rgba(139, 92, 246, 0.6),
    transparent
  );
}

:global(.dark) .category-label {
  background: linear-gradient(135deg, rgba(139, 92, 246, 0.15), rgba(99, 102, 241, 0.15));
  border-color: rgba(139, 92, 246, 0.3);
  box-shadow: 0 2px 8px rgba(139, 92, 246, 0.2);
}

:global(.dark) .category-text {
  color: #a78bfa;
}

/* ============ 数量分隔线样式（简单虚线）============ */
.count-divider-line {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.dashed-line {
  width: 100%;
  height: 1px;
  background-image: linear-gradient(
    to right,
    rgba(203, 213, 225, 0.4) 50%,
    transparent 50%
  );
  background-size: 12px 1px;
  background-repeat: repeat-x;
}

/* 暗黑模式 - 数量分隔线 */
:global(.dark) .dashed-line {
  background-image: linear-gradient(
    to right,
    rgba(71, 85, 105, 0.4) 50%,
    transparent 50%
  );
}

/* ============ 图片模式样式 ============ */
img {
  transition: transform 0.3s ease;
  max-height: 120px;
}

img:hover {
  transform: scale(1.02);
}
</style>