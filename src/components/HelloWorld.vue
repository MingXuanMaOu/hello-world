<template>
  <div id="div">
    <div id="div">
      <el-button>默认按钮</el-button>
      <el-button size="large">中等按钮</el-button>
      <el-button size="small">小型按钮</el-button>
    </div>
    <div id="div">
      <el-button type="primary">常规按钮</el-button>
      <el-button type="success">成功按钮</el-button>
      <el-button type="info">信息按钮</el-button>
      <el-button type="warning">警告按钮</el-button>
      <el-button type="danger">危险按钮</el-button>
    </div>
    <div id="div">
      <el-button type="primary" :plain="true">描边</el-button>
      <el-button type="primary" :round="true">圆角</el-button>
      <el-button type="primary" :circle="true">圆形</el-button>
      <el-button type="primary" :disable="true">禁用</el-button>
      <el-button type="primary" :loading="true">加载</el-button>
    </div>
    <div id="div">
      <el-button type="primary" icon="share"></el-button>
      <el-button type="primary" icon="delete"></el-button>
      <el-button type="primary" icon="search">图标在前</el-button>
      <el-button type="primary"
        >图标在后<el-icon class="el-icon--right"><upload/></el-icon></el-button>
    </div>
    <div id="div">
      <el-tag>普通标签</el-tag>
      <span style="margin: 10px"></span>
      <el-tag :hit="true">描边标签</el-tag>
      <span style="margin: 10px"></span>
      <el-tag color="purple">紫色背景标签</el-tag>
    </div>
    <div id="div">
      <template v-for="(tag,index) in tags" :key="tag">
        <el-tag :closable="true" @close="closeTag(index)">{{ tag }}</el-tag>
        <span style="padding: 10px;"></span>
      </template>
      <el-input style="width: 90px"
        v-if="show"
        v-model="inputValue"
        @keyup.enter="handleInputConfirm"
        @blur="handleInputConfirm"
        size="small">
      </el-input>
      <el-button size="small" v-else @click="showInput">新建标签 +</el-button>
    </div>
    <div id="div">
      <el-check-tag :checked="true">足球</el-check-tag>
      <span style="padding: 10px"></span>
      <el-check-tag :checked="false">篮球</el-check-tag>
    </div>
    <div id="div">
      <el-empty description="设置空态图的描述文案" :image-size="400"></el-empty>
      <el-empty>
        <!-- image具名插槽用来替换默认的图片部分 -->
        <template v-slot:image>
          <img src="@/assets/logo.png" alt="Logo"/>
        </template>
        <!-- description具名插槽用来替换默认的描述部分 -->
        <template v-slot:description>
          <h3>自定义描述内容</h3>
        </template>
        <!-- 默认的插槽用来在空态图的尾部追加内容 -->
        <el-button>看看其他内容</el-button>
      </el-empty>
    </div>
    <div>
      <el-skeleton :row="10" :animated="true"></el-skeleton>
    </div>
  </div>
  <div id="div" style="text-align: left;">
    <el-skeleton :animated="true">
      <template #template>
        <el-skeleton-item
          variant="h1"
          style="width: 100px; height: 30px; padding: 0;"/>
        <el-skeleton-item 
          variant="image"
          style="width: 240px; height: 240px; padding: 0;"/>
          <el-skeleton-item
            variant="p"
            style="width: 30%; padding: 0; margin-top: 20px"
          />
          <el-skeleton-item variant="p" style="width: 90%; padding: 0" />
          <el-skeleton-item variant="p" style="width: 90%; padding: 0" />
      </template>
    </el-skeleton>
  </div>
  <div id="div" style="text-align: left;">
    <el-skeleton :rows="1" :animated="true" :loading="loading">
      <h1>这里是真实的页面元素</h1>
      <p>{{ msg }}</p>
    </el-skeleton>
    <el-image style="width: 500px" src="http://huishao.cc/img/head-img.png">
      <template #placeholder>
        <h1>加载中...</h1>
      </template>
      <template #error>
        <h1>加载失败</h1>
      </template>
    </el-image>
  </div>
  <div id="div">
    <!-- 使用文本类型的头像 -->
    <el-avatar style="margin: 20px">用户</el-avatar>
    <!-- 使用图标类型的头像 -->
    <el-avatar style="margin: 20px" icon="upload"></el-avatar>
    <!-- 使用图片类型的头像 -->
    <el-avatar
      style="margin: 20px"
      :size="100"
      src="http://huishao.cc/img/avatar.jpg"
    ></el-avatar>
    <el-avatar
      style="margin: 20px"
      src="http://huishao.cc/img/avatar.jpg"
    ></el-avatar>
    <el-avatar
      style="margin: 20px"
      shape="square"
      src="http://huishao.cc/img/avatar.jpg"
    ></el-avatar>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tags: ["男装", "女装", "帽子", "鞋子"],
      show: false,
      inputValue: "",
      loading: true,
      msg: "",
    }
  },
  mounted() {
    setTimeout(this.getData,3000);
  },
  methods: {
    closeTag(index) {
      this.tags.splice(index,1);
    },
    showInput() {
      this.show = true
    },
    handleInputConfirm() {
      let inputValue = this.inputValue;
      if (inputValue) {
        this.tags.push(inputValue);
      }
      this.show = false;
      this.inputValue = "";
    },
    getData() {
      this.msg = "这里是请求到的数据",
      this.loading = false;
    },
  },
}
</script>
