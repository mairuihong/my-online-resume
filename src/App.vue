<template>
  <div class="wrapper">
    <!-- 简历标题 -->
    <div class="title">{{ title }}</div>
    <!-- 个人信息 -->
    <div class="content-list">
      <div v-for="(item, index) in introduce" :key="index" class="list-item">
        <div class="item-icon"><span class="icon"></span></div>
        <div v-if="item.icon && item.icon.length > 0" class="content-icon">
          <img
            :src="'/src/assets/' + item.icon + '.svg'"
            :alt="item.icon"
            style="width: 16px; height: 16px"
          />
        </div>
        <div>{{ item.content }}</div>
      </div>
    </div>
    <!-- 在线简历二维码 -->
    <div v-if="online" class="online-resume">
      <img src="/src/assets/online-resume-QrCode.png" alt="QrCode" class="online-resume-QrCode" />
      <span style="font-size: 12px">扫码查看在线简历</span>
    </div>

    <!-- 简历分类 -->
    <!-- 分类标题：专业技能 -->
    <div class="sort-title">专业技能</div>
    <div class="content-list">
      <div v-for="(item, index) in skills" :key="index" class="list-item">
        <div class="item-icon"><span class="icon"></span></div>
        <div>{{ item.content }}</div>
      </div>
    </div>
    <!-- 分类标题：工作经历 -->
    <div class="sort-title">工作经历</div>
    <div class="content-list" v-for="(item, index) in workExperienceList" :key="index">
      <div class="work-title">{{ item.title }}</div>
      <div class="tag-list">
        <div v-for="(tag, tagIndex) in item.tagList" :key="tagIndex" class="tag">{{ tag }}</div>
      </div>
      <div style="padding: 2px 0">工作岗位：{{ item.workPost }}</div>
      <div class="content-list">
        <div v-for="(item1, index1) in item.contentList" :key="index1" class="list-item">
          <div class="item-icon"><span class="icon"></span></div>
          <div>{{ item1.content }}</div>
        </div>
      </div>
    </div>
    <!-- 分类标题：项目经历 -->
    <div class="sort-title">项目经历</div>
    <div
      class="content-list"
      :style="index === 1 ? 'page-break-before: always; padding-top: 50px;' : ''"
      v-for="(item, index) in projectList"
      :key="index"
    >
      <div class="work-title">{{ item.title }}</div>
      <div class="tag-list">
        <div v-for="(tag, tagIndex) in item.tagList" :key="tagIndex" class="tag">{{ tag }}</div>
      </div>
      <div style="padding: 2px 0">介绍：{{ item.introduce }}</div>
      <div style="padding: 2px 0">工作内容：{{ item.workContent }}</div>
      <div class="content-list">
        <div v-for="(item1, index1) in item.contentList" :key="index1" class="list-item">
          <div class="item-icon"><span class="icon"></span></div>
          <div v-if="item1.icon && item1.icon.length > 0" class="content-icon">
            {{ item1.icon }}
          </div>
          <div>{{ item1.content }}</div>
        </div>
      </div>
    </div>
    <!-- 分类标题：个人项目 -->
    <div class="sort-title">个人项目</div>
    <div class="project-list" v-for="(item, index) in selfProjectList" :key="index">
      <div class="project-content">
        <div class="project-title">{{ item.title }}</div>
        <div class="project-introduce">{{ item.introduce }}</div>
        <template v-if="online">
          <a
            v-if="!item.QrCodePath && item.previewLink.length > 0"
            :href="item.previewLink"
            target="_blank"
            class="code-link"
          >
            <img
              src="/src/assets/link.svg"
              alt="link"
              style="margin-right: 4px; width: 16px; height: 16px"
            />
            <span>请使用电脑点击连接预览</span>
          </a>
          <a :href="item.sourceCodeLink" target="_blank" class="code-link">
            <img
              src="/src/assets/github.svg"
              alt="github"
              style="margin-right: 4px; width: 16px; height: 16px"
            />
            <span>源码链接</span>
          </a>
        </template>
      </div>
      <a
        v-if="item.QrCodePath && item.QrCodePath.length > 0"
        :href="item.previewLink"
        target="_blank"
        class="QrCode-wrapper"
      >
        <img :src="item.QrCodePath" class="QrCode" />
        <div class="text">扫码预览</div>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      online: true, // 是否为在线版本
      // online: false, // 是否为在线版本
      title: '麦锐鸿 - 前端开发工程师',
      // 个人信息
      introduce: [
        { icon: '', content: '麦锐鸿 | 男 | 1.5年工作经验' },
        { icon: '', content: '五邑大学 | 本科 | CET-4' },
        { icon: 'phone', content: '17520315098' },
        { icon: 'email', content: 'mairuihong1@foxmail.com' },
        { icon: 'github', content: 'https://github.com/mairuihong' }
      ],
      // 专业技能
      skills: [
        { content: '熟练掌握 HTML5/CSS3/JavaScript，熟悉响应式布局和移动端开发' },
        { content: '掌握 Vue 及其生态库，熟练使用相关 UI 框架' },
        { content: '掌握微信小程序、uniapp，熟悉小程序开发流程' },
        { content: '熟悉 ECharts、uCharts 的使用，有数据看板开发经验' },
        { content: '了解 Vite、webpack、ESlint、Git 等工具的使用，有前端项目搭建经验' },
        { content: '了解 TypeScript、Node.js，使用其开发过简易项目' }
      ],
      // 工作经历
      workExperienceList: [
        {
          title: '广州新维智能科技有限公司（2022.5-2023.9）',
          tagList: ['后台管理系统', '小程序', 'APP', '移动端'],
          workPost: '前端开发工程师',
          contentList: [
            {
              content: '负责工业 SasS 项目的后台管理系统、小程序、公司内部后台系统的更新迭代和维护'
            },
            { content: '负责大屏数据看板开发，部分后台项目的搭建及开发规范化' },
            { content: '负责部分小程序项目的代码架构升级，代码优化及代码规范化' }
          ]
        }
      ],
      // 项目经历
      projectList: [
        {
          title: '云维保（工业维保项目）',
          tagList: ['Vue', 'uniapp', '微信小程序', 'ECharts', 'uCharts'],
          introduce:
            '面向工业生产客户，提供设备售后和设备生产监控、报修维护等功能的系统，包括工厂维保、售后运营、设备报修、管理分析等系列产品。',
          workContent:
            '负责相关后台、小程序的更新迭代、代码优化。负责数据看板开发，小程序代码架构升级。',
          contentList: [
            {
              content:
                '封装后台系统的设备新建编辑业务弹窗组件，优化设备信息、图片的展示，优化表格、弹窗组件交互提示'
            },
            { content: '优化文件上传公共函数，实现多文件同时上传和上传失败提示功能' },
            { content: '优化小程序代码架构，缩小主包大小，加快小程序加载速度' },
            { content: '封装 ECharts 组件，开发后台的数据分析页面及大屏数据看板' },
            { content: '将部分项目的原生小程序代码重构为 uniapp' }
          ]
        },
        {
          title: '云维检',
          tagList: ['Vue', 'ECharts'],
          introduce:
            '面向工厂、物业、店铺等多行业通用的维检系统，用于日常维护、检查任务的分配和执行情况的统计分析。',
          workContent: '负责后台前端项目的搭建、开发规范化，及部分组件、页面功能开发。',
          contentList: [
            {
              content: '基于 Vue2 + TDesign UI，使用 TDesign 脚手架搭建后台前端项目，完善代码架构'
            },
            { content: '使用 ESlint、prettier、Husky 等作为代码规范化工具 ，规范代码开发流程' },
            { content: '实现用户登录功能、页面路由鉴权功能，封装路由跳转提示组件' },
            {
              content:
                '封装顶部用户导航栏、侧边菜单栏等组件，封装企业编辑、成员编辑、部门编辑等通用弹窗组件'
            },
            { content: '负责企业信息、成员信息、部门信息、巡检任务等页面开发' }
          ]
        }
      ],
      // 个人项目
      selfProjectList: [
        {
          title: '团子记账',
          introduce:
            'Vue2 + TypeScript 开发的纯前端简易记账项目，包括记账、明细、统计三个主页面，用于日常消费记账。',
          sourceCodeLink: 'https://github.com/mairuihong/tuanzi-tally',
          previewLink: 'https://mairuihong.github.io/tuanzi-tally-website',
          QrCodePath: '/src/assets/tuanzi-tally-qrcode.png'
        },
        {
          title: 'Wheat UI',
          introduce:
            '使用 Vite 搭建的 Vue3 + TypeScript 的简单 UI 框架，包括开关 Switch、按钮 Button、对话框 Dialog、导航栏 Nav 基础组件。',
          sourceCodeLink: 'https://github.com/mairuihong/wheat-ui',
          previewLink: 'https://mairuihong.github.io/wheat-ui-website/',
          QrCodePath: '/src/assets/wheat-ui-qrcode.png'
        },
        {
          title: 'Paddy UI',
          introduce:
            'React 开发的简单 UI 框架，包括图标 Icon、按钮 Button、对话框 Dialog、布局 Layout 基础组件。',
          sourceCodeLink: 'https://github.com/mairuihong/paddy-ui',
          previewLink: 'https://mairuihong.github.io/paddy-ui-website/'
        },
        {
          title: 'Todo Api',
          introduce:
            '基于 React + Node.js，使用 Ant Design 作为 UI 框架的 todo 应用，以表格形式记录 todo 任务。',
          sourceCodeLink: 'https://github.com/mairuihong/todo-api',
          previewLink: 'http://175.178.162.111:8080/index.html'
        }
      ]
    }
  }
}
</script>

<style scoped lang="less">
@import './style.scss';
</style>
