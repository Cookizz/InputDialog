# InputDialog
A proxy class of AlertDialog that provides input abilities.

### Usage

+ Put `InputDialog` into your project and `dialog_input_layout.xml` and `dialog_bottom_line.9.png` into your resource folder.
+ User InputDialog in a way just like AlertDialog.
```java
new InputDialog.Builder(getActivity())
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
