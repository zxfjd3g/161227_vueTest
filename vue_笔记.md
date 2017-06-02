* Vue.js是什么?
	* 一位华裔前Google工程师开发的前端js库
	* 一个M-V-VM的框架
	  * M model data数据
	  * V view 模板页面
	  * VM viewModel Vue的实例对象
	* 核心概念
	  * 数据绑定
	  * 组件
  * 与angular.js类似的是声明式开发，但性能高于angular，体积小很多, 比较适合移动端开发
  * 它本身不是全能框架, 只关注UI, 如果需要router/ajax, 可以使用对应插件或使用别的库来实现
  
* 基本使用
	* 引入vue.js
	* 创建Vue对象(vm), 指定选项(配置)对象
		* el : 指定dom标签容器的选择器
		* data : 指定初始化状态属性数据的对象
		        对象/函数(返回一个对象)
		* vm代理了data所有的属性的操作(读写)
	* 页面中
		* 使用v-model: 实现双向数据绑定
		* 使用{{}}: 显示数据
		
* Vue对象的选项
	* el
	  * 指定dom标签容器的选择器
		* Vue就会管理对应的标签及其子标签
	* data
	  * 对象或函数类型
		* 指定初始化状态属性数据的对象
		* vue对象可以直接访问其属性
		* 页面中可以直接访问使用
		* 数据代理: 由vm对象来代理对data中所有属性的操作(读/写)
	* methods
		* 包含多个方法的对象
		* 供页面中的事件指令来绑定回调
		* 回调函数默认有event参数, 但也可以指定自己的参数
		* 所有的方法由vue对象来调用, 访问data中的属性直接使用this.xxx
	* computed
		* 包含多个方法的对象
		* 对状态属性进行计算返回一个新的数据, 供页面获取显示
		* 一般情况下是相当于是一个只读的属性
		* 利用set/get方法来实现属性数据的计算读取, 同时监视属性数据的变化
		* 如何给对象定义get/set属性
		  * 在创建对象时指定: get name () {return xxx} / set name (value) {}
		  * 对象创建之后指定: Object.defineProperty(obj, age, {get(){}, set(value){}})
	* watch
	  * Vue.$watch(propertyName, function(value){})
		* 包含多个属性监视的对象
		* 分为一般监视和深度监视
      ```
      'xxx' : {
        deep : true,
        handler : fun(value)
      }
      ```

* 扩展数组
  * 对数组的常用方法进行了包装(用于数据绑定)
	* $remove(item) : 删除数组中对应的元素
	* $set(index, ele) : 给数组中指定下标指定对应的元素  arr[index] = ele

* 过渡
  * 利用vue去操控css的动画
  * transition/animation
  * 使用
    * <div v-show="a"  v-if="a" transition="xxx">
    * 定义css样式
      * .xxx-transition: 在其中去指定transition/animation
      * .xxx-enter
      * .xxx-leave
  * 动画的钩子函数

* 生命周期
  * vm/组件对象
  * 生命周期图
  * 主要的生命周期函数(钩子)
    * created(): 启动异步任务(发送ajax请求, 启动定时器)
    * beforeDestroy(): 做一些收尾的工作

* 页面指令
	* v-text/v-html: 指定标签体
    * v-text : 当作纯文本
		* v-html : 将value作为html标签来解析
	* v-if v-else v-show
		* v-if : 如果vlaue为true, 当前标签会输出在页面中
		* v-else : 与v-if一起使用, 如果value为false, 将当前标签输出到页面中
		* v-show: 就会在标签中添加display样式, 如果vlaue为true, display=block, 否则是none
	* v-for : 遍历
		* 遍历数组 : v-for="person in persons"   $index
		* 遍历对象 : v-for="value in person"   $key
	* v-on : 绑定事件监听
		* v-on:事件名, 可以缩写为: @事件名
		* 监视具体的按键: @keyup.keyCode   @keyup.enter
		* 阻止事件的冒泡和事件默认行为: @click.stop   @click.prevent
		* 隐含对象: $event
	* v-bind : 强制绑定解析表达式  
		* 很多属性值是不支持表达式的, 就可以使用v-bind
		* 可以缩写为:  :id='name'
		* :class
		  * :class="a"
			* :class="{classA : isA, classB : isB}"
			* :class="[classA, classB]"
		* :style
			:style="{color : color}"
	* v-model
		* 双向数据绑定
	* v-el : 标识某个标签
		* v-el:xxx
		* 读取得到标签对象: this.$els.xxx
		
* 过滤器
  * 内置
    * capitalize : 首字母大小
    * uppercase : 全部大写
    * lowercase : 全部小写
    * currency : 货币化
    * pluralize : 单数/复数处理
    * json : json格式化

    * limitBy : 限定数组的部分元素(下标)
    * filterBy : 限定数组的部分元素(值)
    * orderBy : 对数组进行排序
  * 自定义
  * 全局过滤器
    ```
    Vue.filter('过滤器名', function(value, xxx, yyy) {
      //处理逻辑
      return result;
    })
    ```
  * 局部过滤器
    ```
    new Vue({
      filters : {
        '过滤器名' : function(value, xxx, yyy) {
            //处理逻辑
            return result;
        }
      }
    })
    ```
* 指令
  * 内置
    * v:text : 更新元素的 textContent
    * v-html : 更新元素的 innerHTML
    * v-if : 如果为true, 当前标签才会输出到页面
    * v-else: 如果为false, 当前标签才会输出到页面
    * v-show : 通过控制display样式来控制显示/隐藏
    * v-for : 遍历数组/对象
    * v-on : 绑定事件监听, 一般简写为@
    * v-bind : 强制绑定解析表达式, 可以省略v-bind
    * v-model : 双向数据绑定
    * v-el : 为某个元素注册一个唯一标识, vue对象通过$els属性访问这个元素对象
    * v-cloak : 使用它防止闪现表达式, 与css配合: [v-cloak] { display: none }
  * 自定义
    * 注册全局指令
      ```
      Vue.directive('my-directive', function(value){
        this.el.innerHTML = value.toUpperCase();
      })
      ```
    * 注册局部指令
      ```
      directives : {
        'my-directive' : function(value) {
          this.el.innerHTML = value;
        }
      }
      ```
    * 使用指令:
      ```
      v-my-directive='xxx'
      ```

* git管理项目
  * 在github上创建远程仓库
  * 为项目添加.gitignore, 并指定要忽略的文件/文件夹
  * 为项目添加README.md文件
  * git config --global  user.name "zxfjd3g"  设置github账号
  * git config --global user.email "258147149@qq.com"  设置github邮箱
  * git init  初始化本地仓库(.git)
  * git add * 从工作区添加到缓存区
  * git commit -m "xxx" 从缓存区提交到版本区(本地)
  * git remote add origin url  与github远程仓库进行关联
  * git push origin master 将本地版本推送到远程仓库
  * git pull origin master 将远程仓库的更新拉取到本地仓库
  * git clone url 将远程仓库克隆到本地