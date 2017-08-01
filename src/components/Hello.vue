<template>
<div>
<el-button type="text" @click="dialogFormVisible = true">点击生成题目</el-button>
<el-dialog class="max-height" :top='"5%"' :visible.sync="dialogFormVisible" title="新增" style="text-align:left">
    <el-form label-width='100px'>
        <el-row :gutter="20">
        <!-- 所属类型 -->
            <el-col :span="12">
                <el-form-item class="inline-form" label='所属类型'>
                    <el-radio-group v-model="fields.flx">
                        <el-radio-button label="0">从业人员</el-radio-button>
                        <el-radio-button label="1">管理人员</el-radio-button>
                    </el-radio-group>
                </el-form-item>
            </el-col>
        <!-- 所属类型end -->
        <!-- 所属模块 -->           
              <el-col :span="12">
                <el-form-item label='所属模块'>
                   <el-cascader
                    :options="options"
                    v-model="selectedOptions"
                    @change="handleChange">
                  </el-cascader>
                </el-form-item>
            </el-col>
        <!-- 所属模块end -->
        <!-- 题目类别 -->     
            <el-col :span="12" style="clear:left;">
                <el-form-item class="inline-form" label='题型类别'>
                    <el-radio-group v-model="fields.flb" >
                        <el-radio-button label="0" class="wordQ">文字题</el-radio-button>
                        <el-radio-button label="1" class="wordQ">图片题</el-radio-button>
                    </el-radio-group>
                </el-form-item>
            </el-col>
        <!-- 题目类别end -->       
        <!-- 题型编号 -->        
            <el-col :span="12">
                <el-form-item label='题型编号'>
                    <el-radio-group v-model="fields.ftxbh">
                        <el-radio-button label="01">判断题</el-radio-button>
                        <el-radio-button label="02">单选题</el-radio-button>
                        <el-radio-button label="03">多选题</el-radio-button>
                    </el-radio-group>
                </el-form-item>
            </el-col>
        <!-- 题型编号end -->
        <!-- 序号 -->
            <el-col :span="12">
                <el-form-item class="inline-form" label='序号'>
                    <el-input-number :min="1" placeholder='序号' v-model="num1"></el-input-number>
                </el-form-item>
            </el-col>
        <!-- 序号end -->
        <!-- 分值 -->
            <el-col :span="12">
                <el-form-item class="inline-form" label='分值'>
                    <el-input-number placeholder='分值' :min="1" :max="100" v-model="num2"></el-input-number>
                </el-form-item>
            </el-col>
        <!-- 分值end -->
        <!-- 是否显示 -->
            <el-col :span="12">
                <el-form-item label='是否显示'>
                    <el-checkbox true-label="1" false-label="0"></el-checkbox>
                </el-form-item>
            </el-col>
        <!-- 是否显示end -->
        <!-- 知识点编号-->
            <el-col :span="12">
                <el-form-item label='知识点编号'>
                    <el-input placeholder='知识点编号'></el-input>
                </el-form-item>
            </el-col>
        <!-- 知识点编号end--> 
        <!-- 题目 -->
            <el-col :span="24">
                <el-form-item label='题目'>
                    <el-input type='textarea' placeholder='题目'></el-input>
                </el-form-item>
            </el-col>
        <!-- 题目end -->
        <!-- 备注 -->
            <el-col :span="24">
                <el-form-item label='备注'>
                    <el-input type="textarea" placeholder='备注'></el-input>
                </el-form-item>
            </el-col>
        <!-- 备注end -->
        </el-row>
        <el-row class="rowSelection">
            <el-col :span="24">
              <span class="increasedGroup">选项组:</span> 
              <span class="newIncreased"><i class="el-icon-plus"></i>新增选项</span>
            </el-col>
        </el-row>
    <!-- 选项标题 -->
        <el-row :gutter="24" class="selectTitle">
          <el-col :span="3"><div class="grid-content bg-purple">正确答案</div></el-col>
          <el-col :span="14"><div class="grid-content bg-purple">选项内容</div></el-col>
          <el-col :span="4"><div class="grid-content bg-purple">是否显示</div></el-col>
          <el-col :span="3"><div class="grid-content bg-purple">编辑</div></el-col>
        </el-row>
    <!-- 选项标题end -->
    <!-- 第一部分内容 -->
        <el-row :gutter="24" class="firstContent">
          <el-col :span="3"><div class="grid-content bg-purple"><el-checkbox></el-checkbox></div></el-col>
          <el-col :span="14"><div class="grid-content bg-purple"><textarea placeholder="请输入选项内容.如判断题：将显示对与错" type="textarea" rows="2" autocomplete="off" validateevent="true" class="el-textarea__inner"></textarea></div></el-col>
          <el-col :span="4"><div class="grid-content bg-purple"><el-checkbox></el-checkbox></div></el-col>
          <el-col :span="3"><div class="grid-content bg-purple"><el-button type="primary">删除</el-button></div></el-col>
        </el-row>
    <!-- 第一部分内容end -->
    <!-- 第二部分内容 -->
        <el-row :gutter="24" class="secondContent">
          <el-col :span="3"><div class="grid-content bg-purple"><el-checkbox></el-checkbox></div></el-col>
          <el-col :span="14"><div class="grid-content bg-purple"><textarea placeholder="请输入选项内容.如判断题：将显示对与错" type="textarea" rows="2" autocomplete="off" validateevent="true" class="el-textarea__inner"></textarea></div></el-col>
          <el-col :span="4"><div class="grid-content bg-purple"><el-checkbox></el-checkbox></div></el-col>
          <el-col :span="3"><div class="grid-content bg-purple"><el-button type="primary">删除</el-button></div></el-col>
        </el-row>
    <!-- 第二部分内容end -->
    </el-form>
    <!-- 取消、提交 -->
        <div slot='footer' class='dialog-footer'>
         <el-button @click="dialogFormVisible = false">取消</el-button>
         <el-button type='primary' @click="dialogFormVisible = false">提交</el-button>
        </div>
    <!-- 取消、提交end -->
</el-dialog>
</div>
</template>
<script>
  export default{
    data(){
      return{
        num1: 1,
        num2: 1,
        fields: {
          flx:0,
          flb:0,
          ftxbh:"01"
        },
        formLabelWidth: '120px',
        dialogFormVisible: false,
        options: [{
          value: 'zhinan',
          label: '指南',
          children: [{
            value: 'shejiyuanze',
            label: '设计原则',
            children: [{
              value: 'yizhi',
              label: '一致'
            }, {
              value: 'fankui',
              label: '反馈'
            }, {
              value: 'xiaolv',
              label: '效率'
            }, {
              value: 'kekong',
              label: '可控'
            }]
          }, {
            value: 'daohang',
            label: '导航',
            children: [{
              value: 'cexiangdaohang',
              label: '侧向导航'
            }, {
              value: 'dingbudaohang',
              label: '顶部导航'
            }]
          }]
        }, {
          value: 'zujian',
          label: '组件',
          children: [{
            value: 'basic',
            label: 'Basic',
            children: [{
              value: 'layout',
              label: 'Layout 布局'
            }, {
              value: 'color',
              label: 'Color 色彩'
            }, {
              value: 'typography',
              label: 'Typography 字体'
            }, {
              value: 'icon',
              label: 'Icon 图标'
            }, {
              value: 'button',
              label: 'Button 按钮'
            }]
          }, {
            value: 'form',
            label: 'Form',
            children: [{
              value: 'radio',
              label: 'Radio 单选框'
            }, {
              value: 'checkbox',
              label: 'Checkbox 多选框'
            }, {
              value: 'input',
              label: 'Input 输入框'
            }, {
              value: 'input-number',
              label: 'InputNumber 计数器'
            }, {
              value: 'select',
              label: 'Select 选择器'
            }, {
              value: 'cascader',
              label: 'Cascader 级联选择器'
            }, {
              value: 'switch',
              label: 'Switch 开关'
            }, {
              value: 'slider',
              label: 'Slider 滑块'
            }, {
              value: 'time-picker',
              label: 'TimePicker 时间选择器'
            }, {
              value: 'date-picker',
              label: 'DatePicker 日期选择器'
            }, {
              value: 'datetime-picker',
              label: 'DateTimePicker 日期时间选择器'
            }, {
              value: 'upload',
              label: 'Upload 上传'
            }, {
              value: 'rate',
              label: 'Rate 评分'
            }, {
              value: 'form',
              label: 'Form 表单'
            }]
          }, {
            value: 'data',
            label: 'Data',
            children: [{
              value: 'table',
              label: 'Table 表格'
            }, {
              value: 'tag',
              label: 'Tag 标签'
            }, {
              value: 'progress',
              label: 'Progress 进度条'
            }, {
              value: 'tree',
              label: 'Tree 树形控件'
            }, {
              value: 'pagination',
              label: 'Pagination 分页'
            }, {
              value: 'badge',
              label: 'Badge 标记'
            }]
          }, {
            value: 'notice',
            label: 'Notice',
            children: [{
              value: 'alert',
              label: 'Alert 警告'
            }, {
              value: 'loading',
              label: 'Loading 加载'
            }, {
              value: 'message',
              label: 'Message 消息提示'
            }, {
              value: 'message-box',
              label: 'MessageBox 弹框'
            }, {
              value: 'notification',
              label: 'Notification 通知'
            }]
          }, {
            value: 'navigation',
            label: 'Navigation',
            children: [{
              value: 'menu',
              label: 'NavMenu 导航菜单'
            }, {
              value: 'tabs',
              label: 'Tabs 标签页'
            }, {
              value: 'breadcrumb',
              label: 'Breadcrumb 面包屑'
            }, {
              value: 'dropdown',
              label: 'Dropdown 下拉菜单'
            }, {
              value: 'steps',
              label: 'Steps 步骤条'
            }]
          }, {
            value: 'others',
            label: 'Others',
            children: [{
              value: 'dialog',
              label: 'Dialog 对话框'
            }, {
              value: 'tooltip',
              label: 'Tooltip 文字提示'
            }, {
              value: 'popover',
              label: 'Popover 弹出框'
            }, {
              value: 'card',
              label: 'Card 卡片'
            }, {
              value: 'carousel',
              label: 'Carousel 走马灯'
            }, {
              value: 'collapse',
              label: 'Collapse 折叠面板'
            }]
          }]
        }, {
          value: 'ziyuan',
          label: '资源',
          children: [{
            value: 'axure',
            label: 'Axure Components'
          }, {
            value: 'sketch',
            label: 'Sketch Templates'
          }, {
            value: 'jiaohu',
            label: '组件交互文档'
          }]
        }],
        selectedOptions: [],
        selectedOptions2: []
      }
    },
    methods:{
      handleChange(value) {
        console.log(value);
      }
    }
  };  
</script>
<style>
*{
  box-sizing: border-box;
}
html,body,ul,li{margin:0; padding:0;}
.el-dialog__title {
    line-height: 1;
    font-size: 16px;
    font-weight: 700;
     color:#fff;
    float: left;
}
.el-radio-button__orig-radio:checked+.el-radio-button__inner {
    color: #fff;
    background-color: #ff0000;
    border-color: #ff0000;
    box-shadow: -1px 0 0 0 #ff0000;
}
.el-dialog__header {
    padding: 21px 20px 28px;
    background: #ff0000;
}
.el-checkbox__input {
    outline: 0;
    line-height: 1;
    vertical-align: middle;
}
.el-checkbox__input.is-checked .el-checkbox__inner {
    background-color: #ff0000; 
    border-color: #ff0000; 
}
.el-checkbox__inner:hover {
    border-color: #fff;
}
.el-button--primary {
    color: #fff;
    background-color: #ff0000;
    border-color: #ff0000;
}
.rowSelection{
    background-color: #ff0000;
    padding: 10px 0;
    border-radius: 4px;
}
.increasedGroup{
    color:#fff;
    font-weight:500;
    margin-left:14px;
}
.newIncreased{
    float:right;
    color:#fff;
    font-weight:500;
    margin-right:14px;
}
.selectTitle{
    background-color: #f7efef;
    color: #000;
    font-weight:500;
    line-height:36px;
    text-align:center;
}
.grid-content {
    border-radius: 4px;
    min-height: 36px;
  }
.firstContent,.secondContent{
    line-height:36px;
    text-align:center;
    margin-bottom: 12px;
}
.wordQ span{
    display:block;
    padding: 10px 22px;
}
</style>
