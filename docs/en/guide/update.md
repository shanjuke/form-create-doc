---
title: Update log (1.6.5)
---

### current document version 1.5.4

### current version [1.6.5](/guide/update.html)



--------

::: tip Suggestion

Recommended to stay in the latest version

:::


---


#### 1.6.5 (2019-05-06)
- Fixed invalid issue when `element.upload` component `before-remove` event returned `false`
- Fixed invalidating `value` in `mounted`
- Added extended built-in component configuration items to set configuration items such as built-in component `style`
- Added support for mounting custom components to `form-create` [#76](https://github.com/xaboy/form-create/issues/76)
```js
    // Mount custom components
    formCreate.component('test',Vue.extend({
        template:'<span>test</span>'
    }));
    // Generate custom components
    formCreate.maker.create('test');
    // Get the custom component
    formCreate.component('test');
    // Get all custom components
    formCreate.component();
```

- Added support for partial mount `form-create` [#74](https://github.com/xaboy/form-create/issues/74)
```js
new vue({
    'el':'#app',
    components:{
        'FormCreate': formCreate.component('form-create')
    },
    template:'<form-create :rule="rule"></form-create>',
    data:function(){
        return {
            rule:[]
        }
    }
})
```



#### 1.6.4 (2019-04-22)
- Fix `element` date component, time component interval selection time value type problem
- New Support for setting built-in components `slot` via `children` configuration items [#72](https://github.com/xaboy/form-create/issues/72)

```js
maker.input('商品价格','price','100').children([
    maker.create('span').slot('append').children(['元'])
])
```


#### 1.6.3 (2019-04-12)
- Fixed `field` error when there was a special symbol
- Fixed an issue where the form reset value was incorrect after the form was reloaded
- Fix automatically triggers form validation issues after modifying rules
- Update TypeScript file
- Optimization performance issues after multiple generation of build rules
- Added `init` method to manually mount and remove form nodes

```js
$m = formCreate.init(rule,options);

//mount form
$m.mount();
// Remove the form
$m.remove();
// Get form data
$m.$f.formData();
```

#### 1.6.2 (2019-03-26)
- **Fixed an error when including a string in the `children` configuration item**
- **Fixed component configuration items such as element-ui part are invalid**
- **New Use the emit method to set the `mounted`, `reload` callback event**

    - Component mode:

    ```html
    <form-create @mounted="fcMounted" @reload="fcReload">
    ```
    
    
    ```js
    methods:{
      fcMounted:function($f) {
          //TODO form callback event after creation
      },
      fcReload:function($f) {
          //TODO form reload after callback event
      }
    }
    ```
    
    - Vue prototype method:


    ```js
    new Vue({
        mounted:function(){
            //Create a form
            //this.$formCreate([...rule])
        
            this.$on('fc:mounted',function($f){
                //TODO form callback event after creation
            })
            this.$on('fc:reload',function($f){
                //TODO form reload after callback event
            })
        }
    
    })
    ```
  
#### 1.6.1 (2019-03-10)
- **Support typescript**
- Fixed preview button error when element.upload component type is file
- **Repair Import {maker} error report**
- Optimize **All internal prompt text, button text can be customized by configuration parameters**[#48](https://github.com/xaboy/form-create/issues/48)
    - `okBtnText`, `closeBtnText`: Customize the pop-up button text of the `frame` component. The default is `OK`, `Close`
    - `modalTitle`: custom `frame`, `upload` component title text when previewing, default is `preview`
    - `loadingText`: Customize the pop-up box of the `iview.frame` component when loading the prompt text, the default is `Loading...`


- Optimization **Custom component support setting `title`**, when `title` is not set, label width defaults to 0
- Optimize `tree`, `frame` components
- Optimize `formData`, the value returned by the `getValue` method is the value after deep copy


#### 1.6.0 (2019-02-18)
- Optimize `ElementUI`.`tree` component to expand by default

#### 1.6.0-bata.2 (2019-02-12)

- Fixed value cannot be modified after dynamically adding components
- Optimization Internal structure
- **Support ElementUi 2.5.2+**
- Refactoring `frame`, `upload` component popup
- Added `maker.parse(json)` method to convert `json` rules to build rules
- Added custom component event `fc:input`, triggered when formData, getValue gets custom component field
    ```js
    This.$on('fc:input',function(cb,$f) {
      // asynchronous call is invalid
      cb(newValue);
    })
    ```
- Add custom component event `fc:set-value`, set by setValue, changeValue when custom component field value is set
    ```js
      This.$on('fc:set-value',function(newValue,$f) {
      //TODO
    })
    ```

**Note: The following changes are not backward compatible**
- **Modify the data structure returned by the model() method**
    ```js
    {
        Field1:{value,props,validate,options,slot,event,...[other configuration items]},
        Field2: {value,props,validate,options,slot,event,...[other configuration items]}
    }
    ```
- **Modify the closeModal(field) method, now you need to pass in the field field**
- **Modify custom component event name, add `fc:` prefix**


#### 1.5.5 (2019-01-25)

- Fixed component value bug after dynamically adding components
- Fixed `append`, `prepend` method to insert location error bug
- Added `disabled` method to disable components
- Added `setValue` method to modify component values in batches
- Added `show` method to show/hide forms
- Added `clearValidateState` method, manual case form error message
- Support for custom components to listen for `disabled` events, triggered when component is disabled
- Support for custom component listener `reset-field` events, triggered when component resets
- Remove some error tips
- Optimization project packaging, **file reduction 20kb**
- Support custom built-in reset button, submit button click event


#### 1.5.4 (2019-01-15)

- Optimization internal structure
- **Refactoring component addition, modification, deletion**
- **Support Custom internal nested built-in components**
- Optimization **Custom components can be set without `field`**
- Optimize form overloading
- **Add global configuration item `form.size`**to configure form element size
- Remove custom component cache
- Fix event repeat trigger bug
- Optimize `$f ` questions that need to be fetched frequently...
- Added `$f.component()` method, **to get custom component generation rules**
- Added `$f.changeValue(field,value)` method, which is an alias for `$f.changeField`
- Added `$f.rule` attribute to get the form generation rules
- Fix `select` component event does not trigger `bug`


#### 1.5.2 (2018-12-31) <Badge text="金猪年" type="warn"/>

- 新增 upload 组件**列表样式**
- 修改 upload 组件按钮图标
- 修复 upload 组件上传 成功后不显示 bug
- 新增 自定义`datePicker`,`timePicker`,`select`组件 **slot**功能 
- 新增 表单重载后回调函数`onReload`全局配置项,可用于更新`$f`
- 新增 组件`className`配置项,设置组件的 class



#### 1.5.2 (2018-12-26)

- 修复 `rule.value`未同步 bug
- 修复 `options.mounted` 多次触发 bug
- 增强 `iframeHelper`,新增全局方法`form_create_helper`
- 新增 `emitPrefix` 配置项,可自定义 组件`emit `事件的前缀
- 优化 `iview` 版本获取
- 新增 `option.submitBtn.col` 配置项,自定义提交按钮布局规则
- 新增 `option.resetBtn.col` 配置项,自定义重置按钮布局规则
- 新增 通过 `v-model` 获取$f



#### 1.5.1 (2018-12-17)
* 修复 意外添加字段的 bug
* 修复 maker 生成器`directives`方法 bug
* 新增 upload 组件`props.maxLength`参数默认为0
* 增强 maker 生成,新增方法`uploadFile`,`uploadImage`,`uploadFileOne`,`uploadImageOne`

* 优化 `upload`,`frame` 组件样式



#### 1.5.0 (2018-12-15)

* 优化 **内部重构**
* 优化 内置组件缓存功能,**按需重新渲染**
* 优化 **性能优化**,优化内部结构,优化内部事件机制,**性能秒杀之前所有版本**
* 增强 **maker 生成器功能**,可直接根据具体type生成,如`datePicker`组件的`.date`、`.dateRange`等
* 新增 `options`、`onSuccess` 方法,重新修改 options 配置
* 新增 `sync(field)`**手动刷新**指定组件、和`reflash`方法**手动全局刷新**
* 新增 `autoComplete`  **自动生成组件**
* 增强 自定义组件
* 新增 `createTmp `的别名`template`
* 修复 自定义组件获取 `$el`
* 修复 `upload` 组件上传失败后会显示新图片
* 新增 `options.mounted`增加参数`$f`
* 修复 `checkbox`  和`radio`组件首屏加载时选中 bug
* 新增  配置参数`options.switchMaker=ture`是否将规则中的 maker 生成器自动转换为对象
* 新增 配置参数`options.iframeHelper=false`是否开启 `iframe`组件 **子页面助手函数**`${field}_change` ,**快速修改该组件的 value**.**跨域无效**


#### 1.4.6 (2018-11-25)

* 修复 `upload` 组件 `onRemove` 不触发bug
* 修复 `ie` 下兼容性问题
* 修复 `checkbox,radio` 组件不能选中 bug
* 修复 滑块组件不传值时默认 NAN bug

#### 1.4.5 (2018-11-12)
* 优化 上传组件图标显示
* 修复 上传组件图片无法删除 
* 新增 `options.mounted` 表单创建成功后的回调函数
* 支持 `iview>=3.1.4`版本- 
* 修复 上传组件图片无法删除 bug

#### 1.4.4 (2018-11-4)
* 优化 内部功能优化,参数优化
* 新增 使用 **reload 更新生成规则** `$f.reload(newRules)`
* 新增 **标签模式下生成规则发生变化时表单自动刷新**
* 修复 npm run dev命令无法有时打开 Demo

#### 1.4.3 (2018-10-21)
* 修复 ie 兼容性问题,hidden 组件bug
* 新增 使用 template 快速生成自定义组件 `maker.createTmp(template,vm)`


#### 1.4.2 (2018-9-8)

* 新增  `bind`方法.以键值对的方式获取双向数据绑定的表单数据
* 修改  `model`方法. 修改为 `form = $f.model()`无需再传入对象
* 新增  `hidden` 和`visibility`方法设置组件的隐藏和显示

#### 1.4.0 \(2018-8-26\)

* 新增 打包命令`build`和调试命令`dev`

* 修复 frame,tree,inputNumber组件,弹出框BUG

* 新增 表单重置按钮,默认不显示

* 新增 frame组件关闭事件`cancel`

* 优化 maker规则生成器

* 新增 使用标签模式生成

* 新增 **生成任意标签组件**`maker.create(componentName)`\([点击查看iviewUI需要加`i-`前缀的组件列表](#iviewUI需要加`i-`前缀的组件列表)\)

* 新增 表单**重置按钮**

* 新增 标签模式下支持**emit触发事件**

#### 1.3.3 \(2018-8-4\)

* 新增 增加**col栅格布局**规则,设置组件的布局

* 新增 **树型组件**

* 新增`$f.set`方法

#### 1.3.2 \(2018-8-3\)

* 修复 多级联动,时间,日期组件初始化值的BUG

#### 1.3.1 \(2018-6-25\)

* 修复 无法获取时间组件值的bug

#### 1.3.0 \(2018-6-24\)

* 优化和精简内部结构

* 支持 双向数据绑定,可动态修改组件的值和配置参数。单独绑定`make.model(obj,field=''')`,批量绑定`$f.model(obj)`

* 支持 使用`window.formCreate`全局方法快速创建表单，也可以在Vue内部使用`this.$formCreate`

* 新增`option.mounted`事件 ，当组件加载完成后触发

* 修复 一些BUG

#### 1.2.3 \(2018-6-13\)

* 新增 **frame组件**,可通过iframe扩展功能,例如:在已有素材库中选择图片,文件等,图标等定制功能扩展
* 修改 Upload组件type为file时默认不可预览

#### 1.2.2 \(2018-5-27\)

* 修复 Bug
* 修复 显示问题

#### 1.2.0 \(2018-5-27\)

* 内部结构优化

* 新增 **组件规则生成器**`$formCreate.maker`

* 新增 **滑块、评分组件**

* 优化 文件上传组件

* 修复 上传组件无法验证等问题

> 感谢[wxxtqk](https://github.com/wxxtqk) \| [williamBoss](https://github.com/williamBoss)

#### 1.1.7 \(2018-5-18\)

* 修复表单排序问题

* 添加上传图片组件默认预览事件

#### 1.1.6 \(2018-5-17\)

* 修复 require加载问题

* 支持 **cmd,amd加载**

#### 1.1.5

1. 修复时间,日期组件值获取问题
2. 修复同时生成多个form表单冲突问

> 感谢 [时光弧线](https://github.com/shiguanghuxian)

#### 1.1.4

1. 新增动态添加表单元素功能
2. 优化操作接口

#### 1.1.0

1. 内部结构重新
2. 优化上传组件,时间组件
3. 添加多级联动组件
4. 添加多级联动组件的省市区json数据
5. 表单元素事件扩展


