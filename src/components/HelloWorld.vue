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
  <div id="div">
    <el-radio-group v-model="radio">
      <el-radio label="1">选项1</el-radio>
      <el-radio label="2">选项2</el-radio>
      <el-radio label="3">选项3</el-radio>
      <el-radio label="4">选项4</el-radio>
    </el-radio-group>
  </div>
  <div id="div">
    <el-radio-group v-model="city">
      <el-radio-button label="1">北京</el-radio-button>
      <el-radio-button label="2">上海</el-radio-button>
      <el-radio-button label="3">广州</el-radio-button>
      <el-radio-button label="4">深圳</el-radio-button>
    </el-radio-group>
  </div>
  <div id="div">
    <el-checkbox-group v-model="checkBox" :min="1" :max="3">
      <el-checkbox label="1">A</el-checkbox>
      <el-checkbox label="2">B</el-checkbox>
      <el-checkbox label="3">C</el-checkbox>
      <el-checkbox label="4">D</el-checkbox>
    </el-checkbox-group>
  </div>
  <div style="margin: 40px">
    <el-input
      v-model="value"
      placeholder="请输入内容"
      :disabled="false"
      :show-password="true"
      :clearable="true"
      prefix-icon="el-icon-search"
      type="text"
    ></el-input>
  </div>
  <div style="margin: 40px">
    <el-input v-model="value" type="text">
      <template #prepend>Http://</template>
      <template #append>.com</template>
    </el-input>
  </div>
  <div style="margin-top: 240px">
    <el-autocomplete
      v-model="value"
      :fetch-suggestions="queryData"
      placeholder="请输入内容"
      @select="selected"
      :highlight-first-item="true"
    ></el-autocomplete>
  </div>
  <div id="div">
    <el-input-number
      :min="1"
      :max="10"
      :step="1"
      v-model="num"
    ></el-input-number>
  </div>
  <div>
    <el-select :multiple="true" :clearable="true" v-model="value">
      <el-option-group v-for="group in options" :key="group.label">
        <el-option :label="group.label" :value="group.label">
      </el-option>
      <el-option
          v-for="item in group.options"
          :value="item.value"
          :label="item.label"
          :key="item.value"
        >
        </el-option>
      </el-option-group>
    </el-select>
  </div>
  <div>
    <div class="m-4">
    <p>Child options expand when clicked (default)</p>
    <el-cascader v-model="value" :options="optiones" :props="{expandTrigger: 'hover'}" />
  </div>
  </div>
  <div id="div">
    <el-switch
      v-model="switch1"
      active-text="会员"
      inactive-text="非会员"
      active-color="#00FF00"
      inactive-color="#FF0000"
    ></el-switch>
  </div>
  <div id="div">
    <el-switch
      v-model="switch2"
      active-text="加载中"
      :loading="true"
    ></el-switch>
  </div>
  <div id="div">
    <el-switch
      v-model="switch3"
      inactive-text="禁用"
      :disabled="true"
    ></el-switch>
  </div>
  <el-slider v-model="sliderValue"
   :format-tooltip="format"
   :step="10"
   :show-stops="true"
   :show-input="true"
   range="true"></el-slider>
   <div style="padding: 40px;">
    <el-slider v-model="sliderValue" :marks="marks"></el-slider>
   </div>
   <div>
    <el-time-picker
      :is-range="true"
      v-model="time"
      range-separator="~"
      :arrow-control="true"
      start-placeholder="开始时间"
      end-placeholder="结束时间"
    >
    </el-time-picker>
  </div>
  <div>
    <el-date-picker
      v-model="date"
      type="daterange"
      range-separator="至"
      start-placeholder="开始日期"
      end-placeholder="结束日期"
      >
    </el-date-picker>
  </div>
  <div>
    <el-color-picker :show-alpha="true" v-model="color"></el-color-picker>
  </div>
</template>

<script>

export default {
  data() {
    return {
      switch1: false,
      switch2: true,
      switch3: false,
      sliderValue: 0,
      time: 0,
      tags: ["男装", "女装", "帽子", "鞋子"],
      show: false,
      inputValue: "",
      loading: true,
      msg: "",
      radio: "0",
      city: "1",
      checkBox: [],
      value: "",
      num: "0",
      date: 0,
      color: "",
      marks: {
        0: "起点",
        50: "半程啦！",
        90: {
          style: {
            color: "#ff0000",
          },
          label: "就到终点啦",
        },
      },
      options: [
        {
          label: "球类",
          options: [
            {
              value: "选项1",
              label: "足球",
            },
            {
              value: "选项2",
              label: "篮球",
              disabled: true,
            },
            {
              value: "选项3",
              label: "排球",
            },
            {
              value: "选项4",
              label: "乒乓球",
            },
          ],
          datas: [
        {
          value: "父1",
          label: "运动",
          children: [
            {
              value: "子1",
              label: "足球",
            },
            {
              value: "子2",
              label: "篮球",
            },
          ],
        },
        {
          value: "父2",
          label: "休闲",
          children: [
            {
              value: "子1",
              label: "游戏",
            },
            {
              value: "子2",
              label: "魔方",
            },
          ],
        },
      ],
        },
        {
          label: "休闲",
          options: [
            {
              value: "选项5",
              label: "散步",
            },
            {
              value: "选项6",
              label: "游泳",
            },
          ],
        },
      ],
      optiones : [
  {
    value: 'guide',
    label: 'Guide',
    children: [
      {
        value: 'disciplines',
        label: 'Disciplines',
        children: [
          {
            value: 'consistency',
            label: 'Consistency',
          },
          {
            value: 'feedback',
            label: 'Feedback',
          },
          {
            value: 'efficiency',
            label: 'Efficiency',
          },
          {
            value: 'controllability',
            label: 'Controllability',
          },
        ],
      },
      {
        value: 'navigation',
        label: 'Navigation',
        children: [
          {
            value: 'side nav',
            label: 'Side Navigation',
          },
          {
            value: 'top nav',
            label: 'Top Navigation',
          },
        ],
      },
    ],
  },
  {
    value: 'component',
    label: 'Component',
    children: [
      {
        value: 'basic',
        label: 'Basic',
        children: [
          {
            value: 'layout',
            label: 'Layout',
          },
          {
            value: 'color',
            label: 'Color',
          },
          {
            value: 'typography',
            label: 'Typography',
          },
          {
            value: 'icon',
            label: 'Icon',
          },
          {
            value: 'button',
            label: 'Button',
          },
        ],
      },
      {
        value: 'form',
        label: 'Form',
        children: [
          {
            value: 'radio',
            label: 'Radio',
          },
          {
            value: 'checkbox',
            label: 'Checkbox',
          },
          {
            value: 'input',
            label: 'Input',
          },
          {
            value: 'input-number',
            label: 'InputNumber',
          },
          {
            value: 'select',
            label: 'Select',
          },
          {
            value: 'cascader',
            label: 'Cascader',
          },
          {
            value: 'switch',
            label: 'Switch',
          },
          {
            value: 'slider',
            label: 'Slider',
          },
          {
            value: 'time-picker',
            label: 'TimePicker',
          },
          {
            value: 'date-picker',
            label: 'DatePicker',
          },
          {
            value: 'datetime-picker',
            label: 'DateTimePicker',
          },
          {
            value: 'upload',
            label: 'Upload',
          },
          {
            value: 'rate',
            label: 'Rate',
          },
          {
            value: 'form',
            label: 'Form',
          },
        ],
      },
      {
        value: 'data',
        label: 'Data',
        children: [
          {
            value: 'table',
            label: 'Table',
          },
          {
            value: 'tag',
            label: 'Tag',
          },
          {
            value: 'progress',
            label: 'Progress',
          },
          {
            value: 'tree',
            label: 'Tree',
          },
          {
            value: 'pagination',
            label: 'Pagination',
          },
          {
            value: 'badge',
            label: 'Badge',
          },
        ],
      },
      {
        value: 'notice',
        label: 'Notice',
        children: [
          {
            value: 'alert',
            label: 'Alert',
          },
          {
            value: 'loading',
            label: 'Loading',
          },
          {
            value: 'message',
            label: 'Message',
          },
          {
            value: 'message-box',
            label: 'MessageBox',
          },
          {
            value: 'notification',
            label: 'Notification',
          },
        ],
      },
      {
        value: 'navigation',
        label: 'Navigation',
        children: [
          {
            value: 'menu',
            label: 'Menu',
          },
          {
            value: 'tabs',
            label: 'Tabs',
          },
          {
            value: 'breadcrumb',
            label: 'Breadcrumb',
          },
          {
            value: 'dropdown',
            label: 'Dropdown',
          },
          {
            value: 'steps',
            label: 'Steps',
          },
        ],
      },
      {
        value: 'others',
        label: 'Others',
        children: [
          {
            value: 'dialog',
            label: 'Dialog',
          },
          {
            value: 'tooltip',
            label: 'Tooltip',
          },
          {
            value: 'popover',
            label: 'Popover',
          },
          {
            value: 'card',
            label: 'Card',
          },
          {
            value: 'carousel',
            label: 'Carousel',
          },
          {
            value: 'collapse',
            label: 'Collapse',
          },
        ],
      },
    ],
  },
  {
    value: 'resource',
    label: 'Resource',
    children: [
      {
        value: 'axure',
        label: 'Axure Components',
      },
      {
        value: 'sketch',
        label: 'Sketch Templates',
      },
      {
        value: 'docs',
        label: 'Design Documentation',
      },
    ],
  },
]

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
    queryData(queryString, callback){
      let array = [];
      if(queryString.length > 0) {
        array.push({value: queryString})
      }
      array.push(
        ...[
          { value: "衣服" },
          { value: "裤子" },
          { value: "帽子" },
          { value: "鞋子" },
        ]
      );
      callback(array)
    },
    selected(obj) {
      alert(obj.value);
    },
    format(value) {
      return `${value}%111`
    }
  },
  
}
</script>
