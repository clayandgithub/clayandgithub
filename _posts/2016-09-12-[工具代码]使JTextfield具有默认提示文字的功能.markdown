---
layout:     post
title:      "[工具代码]使JTextfield具有默认提示文字的功能"
subtitle:   "工具代码"
date:       2016-09-12
author:     "王维维"
header-img: "img/post-bg-2015.jpg"
tags:
    - java
    - swing
    - 工具代码
---

> “抛砖引玉”

## 简介<span id="简介" />

[跳过废话，直接看正文](#正文)

让JTextfield中出现默认提示内容，当获取焦点时自动消失

---

## 正文<span id = "正文" />

* JTextFieldHintListener

```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.FocusEvent;
import java.awt.event.FocusListener;

public class JTextFieldHintListener implements FocusListener {
    private String mHindText;
    private JTextField mTextField;

    public JTextFieldHintListener(String hintText, JTextField textField) {
        this.mHindText = hintText;
        this.mTextField = textField;
        textField.setForeground(Color.GRAY);
    }
    @Override
    public void focusGained(FocusEvent e) {
        String temp = mTextField.getText();
        if(temp.equals(mHindText)){
            mTextField.setText("");
            mTextField.setForeground(Color.BLACK);
        }
    }
    @Override
    public void focusLost(FocusEvent e) {
        String temp = mTextField.getText();
        if(temp.equals("")){
            mTextField.setForeground(Color.GRAY);
            mTextField.setText(mHindText);
        }
    }
}
```

在生成JTextField时调用以下代码即可：

```java
final JTextField textField = new JTextField(15);
textField.addFocusListener(new JTextFieldHintListener("提示文字", textField));
```

## 后记<span id="后记" />

如果有需要，还可以把文字颜色的变化也作为变量放入JTextfieldHintListener中