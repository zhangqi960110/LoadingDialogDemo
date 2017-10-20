# LoadingDialogDemo
Android简单的Loading Dialog实现

大家在使用APP的时候都会遇到网络不好的情况，如果没有加载条之类的，会感觉APP体验很差；所以一般都会有一个loading过程，告诉用户正在请求数据；
下面我们先看一下实现效果
![image](https://github.com/zhangqi960110/LoadingDialogDemo/raw/master/loading.gif)

在这里我只是简单的讲解一下思路：

第一步；先写一个自定义dialog，代码也比较详细。就是创建一个dialog，如下：

```
  public static Dialog createLoadingDialog(Context context, String msg) {
        LayoutInflater inflater = LayoutInflater.from(context);
        View v = inflater.inflate(R.layout.dialog_loading, null);// 得到加载view
        LinearLayout layout = (LinearLayout) v
                .findViewById(R.id.dialog_loading_view);// 加载布局
        TextView tipTextView = (TextView) v.findViewById(R.id.tipTextView);// 提示文字
        tipTextView.setText(msg);// 设置加载信息

        Dialog loadingDialog = new Dialog(context, R.style.MyDialogStyle);// 创建自定义样式dialog
        loadingDialog.setCancelable(true); // 是否可以按“返回键”消失
        loadingDialog.setCanceledOnTouchOutside(false); // 点击加载框以外的区域
        loadingDialog.setContentView(layout, new LinearLayout.LayoutParams(
                LinearLayout.LayoutParams.MATCH_PARENT,
                LinearLayout.LayoutParams.MATCH_PARENT));// 设置布局
        /**
         *将显示Dialog的方法封装在这里面
         */
        Window window = loadingDialog.getWindow();
        WindowManager.LayoutParams lp = window.getAttributes();
        lp.width = WindowManager.LayoutParams.MATCH_PARENT;
        lp.height = WindowManager.LayoutParams.WRAP_CONTENT;
        window.setGravity(Gravity.CENTER);
        window.setAttributes(lp);
        window.setWindowAnimations(R.style.PopWindowAnimStyle);
        loadingDialog.show();

        return loadingDialog;
    }
```

然后我们就可以看到返回的是dialog对象，我们在我们的类中调用即可。当然，有显示，就有关闭，我们直接将关闭的方法，也封装在自定义dialog中。

第二步；封装的关闭的方法如下：
```
    /**
     * 关闭dialog
     *
     * @param mDialogUtils
     */
    public static void closeDialog(Dialog mDialogUtils) {
        if (mDialogUtils != null && mDialogUtils.isShowing()) {
            mDialogUtils.dismiss();
        }
    }
```

欢迎给意见！！！


