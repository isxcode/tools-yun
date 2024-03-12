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
            <p class="card-description">{{ card.description }}</p>
            <h3 class="card-name">{{ card.name }}</h3>
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
      currentCategory: 'AI',
      categories: [
        {
          id: 0, name: 'AI', cards: [
            {
              id: 1,
              logo: 'logo1.png',
              name: 'Poe',
              description: 'ChatGPT3.5',
              link: 'https://poe.com/ChatGPT',
            },
            {
              id: 2,
              logo: 'logo2.png',
              name: 'Bard',
              description: 'google的ai chat',
              link: 'https://bard.google.com/chat',
            },
            {
              id: 3,
              logo: 'logo2.png',
              name: 'Copilot',
              description: '微软的ai chat',
              link: 'https://www.bing.com/search?q=Bing+AI&showconv=1&FORM=hpcodx',
            },
          ]
        },
        {
          id: 1, name: '视频', cards: [
            {
              id: 1,
              logo: 'logo1.png',
              name: 'BiliBili',
              description: '哔哩哔哩',
              link: 'https://www.bilibili.com/',
            },
          ]
        },
        {
          id: 1, name: '后端', cards: [
            {
              id: 1,
              logo: 'logo1.png',
              name: 'Maven仓库',
              description: 'maven仓库',
              link: 'https://mvnrepository.com/'
            },
            {
              id: 2,
              logo: 'logo2.png',
              name: 'Docker hub',
              description: 'docker仓库',
              link: 'https://hub.docker.com/'
            },
            // 添加更多卡片...
          ]
        },
        {
          id: 2, name: '前端', cards: [
            // 前端分类下的卡片
          ]
        },
        {
          id: 3, name: '加密', cards: [
            {
              id: 1,
              logo: 'logo2.png',
              name: '密码生成器',
              description: '生成密码',
              link: 'https://www.bchrt.com/tools/suijimima/'
            },
          ]
        },
        {
          id: 4, name: '书籍', cards: [
            {
              id: 1,
              logo: 'logo2.png',
              name: 'Z-library',
              description: '免费书籍',
              link: 'https://zh.z-library.se/'
            },
          ]
        },
        {
          id: 5, name: '音乐', cards: [
            {
              id: 1,
              logo: 'logo2.png',
              name: 'musicenc',
              description: '免费歌词',
              link: 'https://www.musicenc.com/'
            },
          ]
        },
        {
          id: 6, name: '游戏', cards: [
            {
              id: 1,
              logo: 'logo2.png',
              name: '在线小霸王',
              description: '免费GBA在线游戏',
              link: 'https://www.yikm.net/'
            },
            {
              id: 2,
              logo: 'logo2.png',
              name: 'GBA专区',
              description: '免费GBA下载',
              link: 'http://gbayouxi.ysepan.com/',
            },
          ]
        },
        {
          id: 8, name:
              '导航合集', cards:
              [
                {
                  id: 1,
                  logo: 'logo2.png',
                  name: 'TBox导航',
                  description: '在线链接合集',
                  link: 'https://www.tboxn.com/'
                },
                {
                  id: 2,
                  logo: 'logo2.png',
                  name: '奇迹秀工具箱',
                  description: '在线工具箱合集',
                  link: 'https://www.qijishow.com/down/index.html'
                },
                {
                  id: 3,
                  logo: 'logo2.png',
                  name: '图钉AI导航',
                  description: '在线AI链接合集',
                  link: 'https://www.tudingai.com/'
                },
              ]
        }
        ,
        {
          id: 9, name:
              'VPN', cards:
              [
                {
                  id: 1,
                  logo: 'logo2.png',
                  name: '东方网络',
                  description: '科学翻墙VPN',
                  link: 'https://panel3.touhou.tel/'
                },
              ]
        }
        ,
        {
          id: 10, name:
              '转换', cards:
              [
                {
                  id: 1,
                  logo: 'logo2.png',
                  name: 'Unicode转码',
                  description: '在线Unicode编码转换',
                  link: 'https://www.jyshare.com/front-end/3602/',
                },
              ]
        }
        ,
        {
          id: 11, name:
              '镜像仓库', cards:
              [
                {
                  id: 1,
                  logo: 'logo2.png',
                  name: '阿里巴巴官网镜像站',
                  description: '阿里巴巴免费镜像合集',
                  link: 'https://developer.aliyun.com/mirror/',
                },
              ]
        },
        {
          id: 12, name:
              '画图', cards:
              [
                {
                  id: 1,
                  logo: 'logo2.png',
                  name: 'draw.io',
                  description: '免费流程图在线编辑工具',
                  link: 'https://app.diagrams.net/',
                },
                {
                  id: 2,
                  logo: 'logo2.png',
                  name: 'Muse',
                  description: '免费文件传输',
                  link: 'https://musetransfer.com/',
                },
                {
                  id: 3,
                  logo: 'logo2.png',
                  name: 'MoreCopy',
                  description: '免费文件传输',
                  link: 'https://air.9998k.cn/',
                },
              ]
        }
        , {
          id: 12, name:
              '传输', cards:
              [
                {
                  id: 1,
                  logo: 'logo2.png',
                  name: 'Muse',
                  description: '免费文件传输',
                  link: 'https://musetransfer.com/',
                },
                {
                  id: 2,
                  logo: 'logo2.png',
                  name: 'MoreCopy',
                  description: '免费文件传输',
                  link: 'https://air.9998k.cn/',
                },
              ]
        },
        {
          id: 16, name:
              '转换格式', cards:
              [
                {
                  id: 1,
                  logo: 'logo2.png',
                  name: 'converter',
                  description: 'PNG转SVG',
                  link: 'https://converter.app/png-to-svg/result.php?lang=cn',
                },
                {
                  id: 2,
                  logo: 'logo2.png',
                  name: 'aigei',
                  description: '图片去底色',
                  link: 'https://www.aigei.com/bgremover/',
                },
                {
                  id: 3,
                  logo: 'logo2.png',
                  name: 'aigei',
                  description: 'PNG转PDF',
                  link: 'http://www.pdfdo.com/image-to-pdf.aspx',
                },
                {
                  id: 4,
                  logo: 'logo2.png',
                  name: 'smallpdf',
                  description: 'WORD转PDF',
                  link: 'https://smallpdf.com/cn/word-to-pdf',
                },
                {
                  id: 5,
                  logo: 'logo2.png',
                  name: 'convertio',
                  description: '文件转换',
                  link: 'https://convertio.co/zh/',
                },
              ]
        }
        ,
        {
          id: 13, name:
              '会员', cards:
              [
                {
                  id: 1,
                  logo: 'logo2.png',
                  name: '逮虾户',
                  description: '会员顺风车',
                  link: 'https://daixiahu.co/#/buses',
                }
              ]
        }
        ,
        {
          id: 14, name:
              '在线编辑', cards:
              [
                {
                  id: 1,
                  logo: 'logo2.png',
                  name: 'Arya',
                  description: 'Markdown在线编辑',
                  link: 'https://markdown.lovejade.cn/',
                }
              ]
        }
        ,
        {
          id: 15, name:
              '通信', cards:
              [
                {
                  id: 1,
                  logo: 'logo2.png',
                  name: 'sms-activate',
                  description: '短信激活通讯',
                  link: 'https://sms-activate.org/en',
                }
              ]
        },
        {
          id: 16, name:
              '文件生成', cards:
              [
                {
                  id: 1,
                  logo: 'logo2.png',
                  name: 'patorjk',
                  description: 'Banner生成器',
                  link: 'https://patorjk.com/software/taag/#p=display&f=Graffiti&t=Type%20Something',
                }
              ]
        }
      ],
    }
        ;
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