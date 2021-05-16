对话框

基本使用

- 内容分为 body 和 footer，footer 需要具名 slot 

- title：用于定义标题
- width：表示宽度 50%
- center：居中布局 
- fullscreen：是否全屏 false
- top：顶端距离 15vh



- visible：接收 boolean 值，用于显示和隐藏对话框
- before-close：关闭前的回调，function(done)，done 用于关闭 Dialog
- destroy-on-close：关闭后销毁 dialog 元素 false
- custom-class：自定义类名
- append-to-body：嵌套 dialog （不建议使用）

事件

- open：打开前的回调
- opened：打开完成动画的回调E
- close：关闭前的回调
- closed：关闭动画结束时的回调

```js
<el-button type="text" @click="dialogVisible = true">点击打开 Dialog</el-button>

<el-dialog
  title="提示"
  :visible.sync="dialogVisible"
  width="30%"
  :before-close="handleClose">
  <span>这是一段信息</span>
  <span slot="footer" class="dialog-footer">
    <el-button @click="dialogVisible = false">取 消</el-button>
    <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
  </span>
</el-dialog>

<script>
  export default {
    data() {
      return {
        dialogVisible: false
      };
    },
    methods: {
      handleClose(done) {
        this.$confirm('确认关闭？')
          .then(_ => {
            done();
          })
          .catch(_ => {});
      }
    }
  };
</script>
```

> Dialog 的内容是懒渲染的，即在第一次被打开之前，传入的默认 slot 不会被渲染到 DOM 上。因此，如果需要执行 DOM 操作，或通过 `ref` 获取相应组件，请在 `open` 事件回调中进行。
>
> 如果 `visible` 属性绑定的变量位于 Vuex 的 store 内，那么 `.sync` 不会正常工作。此时需要去除 `.sync` 修饰符，同时监听 Dialog 的 `open` 和 `close` 事件，在事件回调中执行 Vuex 中对应的 mutation 更新 `visible` 属性绑定的变量的值

