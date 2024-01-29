<template>
  <div class="container">
    <div class="left-panel">
      <div class="logo">
        <!-- Logo部分 -->
      </div>
      <div class="category-list">
        <ul>
          <li v-for="category in categories" :key="category.id" @click="changeCategory(category.name)">
            {{ category.name }}
          </li>
        </ul>
      </div>
    </div>
    <div class="right-panel">
      <div class="card-list">
        <div v-for="card in currentCategoryCards" :key="card.id" class="card" :class="{ 'hovered': card.isHovered }"
             :style="{ transform: `rotate(${card.rotation}deg)` }"
             @mouseover="handleMouseOver(card)"
             @mouseleave="handleMouseLeave(card)">
          <div class="card-logo">
            <img :src="card.logo" alt="Logo">
          </div>
          <div class="card-content" @click="goToLink(card.link);">
            <h3 class="card-name">{{ card.name }}</h3>
            <p class="card-description">{{ card.description }}</p>
          </div>
        </div>
        <div v-if="currentCategoryCards.length === 0">该分类下没有卡片。</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isHovered: false,
      rotation: 0,
      currentCategory: '视频',
      categories: [
        {
          id: 1, name: '视频', cards: [
            {
              id: 1,
              logo: 'logo1.png',
              name: 'Card 1',
              description: 'Card 1的功能介绍',
              link: 'https://baidu.com'
            },
            {
              id: 2,
              logo: 'logo2.png',
              name: 'Card 2',
              description: 'Card 2的功能介绍',
              link: 'https://baidu.com'
            },
            // 添加更多卡片...
          ]
        },
        {
          id: 2, name: '前端', cards: [
            // 前端分类下的卡片
          ]
        },
        // 添加更多分类...
      ],
    };
  },
  computed: {
    currentCategoryCards() {
      const category = this.categories.find(cat => cat.name === this.currentCategory);
      return category ? category.cards : [];
    }
  },
  methods: {
    goToLink(url) {
      // 在这里使用编程式导航进行跳转
      window.location.href = url;
    },
    changeCategory(category) {
      this.currentCategory = category;
    },
    handleMouseOver(card) {
      card.isHovered = true;
      card.rotation = -1;
    },
    handleMouseLeave(card) {
      card.isHovered = false;
      card.rotation = 0;
    }
  }
}
</script>

<style scoped>

@font-face {
  font-family: 'moe';
  src: url('//at.alicdn.com/t/webfont_jq0x47mjt6a.eot'); /* IE9*/
  src: url('//at.alicdn.com/t/webfont_jq0x47mjt6a.eot?#iefix') format('embedded-opentype'), /* IE6-IE8 */ url('//at.alicdn.com/t/webfont_jq0x47mjt6a.woff2') format('woff2'),
  url('//at.alicdn.com/t/webfont_jq0x47mjt6a.woff') format('woff'), /* chrome、firefox */ url('//at.alicdn.com/t/webfont_jq0x47mjt6a.ttf') format('truetype'), /* chrome、firefox、opera、Safari, Android, iOS 4.2+*/ url('//at.alicdn.com/t/webfont_jq0x47mjt6a.svg#Alibaba-PuHuiTi-Regular') format('svg'); /* iOS 4.1- */
}

body {
  font-family: 'moe';
}

@media (max-width: 640px) {
  .meta-right .meta-view {
    display: unset !important;
  }
}

.hovered {
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
}

.container {
  display: flex;
  flex-wrap: wrap;
}

.left-panel {
  flex: 1;
  max-width: 200px; /* 调整左侧面板的最大宽度 */
  /* 左侧内容样式 */
}

.right-panel {
  flex: 2;
  /* 右侧内容样式 */
}

.logo {
  /* Logo部分样式 */
}

.category-list {
  /* 链接分享分类列表样式 */
}

.category-list ul {
  list-style: none;
  padding: 0;
}

.category-list li {
  margin-bottom: 10px;
  cursor: pointer;
  /* 其他样式 */
  display: flex;
  align-items: center;
  color: #8B4513;
  padding: 10px 15px;
  border-radius: 5px;
}

.category-list li:hover {
  background-color: #8B4513;
  color: white;
}

.card-list {
  display: flex;
  flex-wrap: wrap;
}

.card {
  width: 300px;
  margin-right: 20px;
  margin-bottom: 20px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.card-logo img {
  width: 50px;
  height: 50px;
}

.card-content {
  margin-top: 10px;
}

.card-name {
  font-size: 18px;
  font-weight: bold;
}

.card-description {
  margin-top: 5px;
}

.card-link {
  display: inline-block;
  margin-top: 10px;
  background-color: #8B4513;
  color: white;
  padding: 5px 10px;
  border-radius: 5px;
  text-decoration: none;
}

.card-link:hover {
  background-color: #654321;
}
</style>