# InputDialog
A proxy of AlertDialog for Android that provides input and validation features.

### Appearance

![demo](http://7xawtr.com1.z0.glb.clouddn.com/input_dialog2.png)

### Use case

+ Put `InputDialog` into your project and put `dialog_input_layout.xml`, `dialog_bottom_line.9.png` into your resource folder and use InputDialog in the way just like AlertDialog.
```java
new InputDialog.Builder(context)
        .setTitle("新建文件夹")
        .setInputDefaultText("/sdcard/my")
        .setInputMaxWords(20)
        .setInputHint("文件夹路径")
        .setPositiveButton("确定", new InputDialog.ButtonActionListener() {
            @Override
            public void onClick(CharSequence inputText) {
                // TODO
            }
        })
        .setNegativeButton("取消", new InputDialog.ButtonActionListener() {
            @Override
            public void onClick(CharSequence inputText) {
                // TODO
            }
        })
        .setOnCancelListener(new InputDialog.OnCancelListener() {
            @Override
            public void onCancel(CharSequence inputText) {
                // TODO
            }
        })
        .interceptButtonAction(new InputDialog.ButtonActionIntercepter() { // 拦截按钮行为
            @Override
            public boolean onInterceptButtonAction(int whichButton, CharSequence inputText, InputDialog dialog) {
                if ("/sdcard/my".equals(inputText) && whichButton == DialogInterface.BUTTON_POSITIVE) {
                    CN21Toast.showToast(getActivity(), "此文件夹已存在");
                    return true;
                }
                return false;
            }
        })
        .show();
```

### Advanced

+ Customize your layout

Call build method `setView(int layoutResId, int editTextId)` to apply your EditText layout. The second parameter instructs you to bind your target EditText by id.
```java
new InputDialog.Builder(context)
        .setView(R.layout.my_edit_text, R.id.my_edit_text)
```

+ Apply input validation

Sometimes you are unwilling to dismiss your dialog after clicking its buttons. Instead, you may need an input validation to intercept the inherent `dismiss` behavior.

Just call build method `interceptButtonAction(ButtonActionIntercepter intercepter)` to catch illegal input and do whatever you want.
```java
new InputDialog.Builder(context)
        .interceptButtonAction(new InputDialog.ButtonActionIntercepter() { // 拦截按钮行为
            @Override
            public boolean onInterceptButtonAction(int whichButton, CharSequence inputText, InputDialog dialog) {
                if ("/sdcard/my".equals(inputText) && whichButton == DialogInterface.BUTTON_POSITIVE) {
                    CN21Toast.showToast(getActivity(), "此文件夹已存在");
                    return true;
                }
                return false;
            }
        })
```
