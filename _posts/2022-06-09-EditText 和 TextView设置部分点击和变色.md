---
title: EditText 和 TextView设置部分点击和变色
date: 2022-06-09 11:11:11.000000000 +09:00
categories: [Android]
tags: [Kotlin]
---

### EditText 和 TextView设置部分点击和变色

## 扩展方法

```kotlin
un TextView.makeLinks(vararg links: Pair<String, View.OnClickListener>) {
    val spannableString = SpannableString(this.text)
    var startIndexOfLink = -1
    for (link in links) {
        val clickableSpan = object : ClickableSpan() {
            override fun updateDrawState(textPaint: TextPaint) {
                // use this to change the link color
                textPaint.color = textPaint.linkColor
                // toggle below value to enable/disable
                // the underline shown below the clickable text
                textPaint.isUnderlineText = true
            }

            override fun onClick(view: View) {
                Selection.setSelection((view as TextView).text as Spannable, 0)
                view.invalidate()
                link.second.onClick(view)
            }
        }
        startIndexOfLink = this.text.toString().indexOf(link.first, startIndexOfLink + 1)
        //      if(startIndexOfLink == -1) continue // todo if you want to verify your texts contains links text
        spannableString.setSpan(
            clickableSpan, startIndexOfLink, startIndexOfLink + link.first.length,
            Spanned.SPAN_EXCLUSIVE_EXCLUSIVE
        )
    }
    this.movementMethod =
    LinkMovementMethod.getInstance() // without LinkMovementMethod, link can not click
    this.setText(spannableString, TextView.BufferType.SPANNABLE)
}
```

## 使用：

```
my_text_view.makeLinks(
        Pair("Terms of Service", View.OnClickListener {
            Toast.makeText(applicationContext, "Terms of Service Clicked", Toast.LENGTH_SHORT).show()
        }),
        Pair("Privacy Policy", View.OnClickListener {
            Toast.makeText(applicationContext, "Privacy Policy Clicked", Toast.LENGTH_SHORT).show()
        }))
```

