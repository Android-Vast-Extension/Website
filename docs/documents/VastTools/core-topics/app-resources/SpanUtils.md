# 自定义字符串

`SpanStrUtils` 能够让文本内容和标记都可以更改。

## 特性

1. 支持的角标类型

    |     类型      |         描述         |
    | :-----------: | :------------------: |
    | `Superscript` | 文本以上标的形式展现 |
    |  `Subscript`  | 文本以下标的形式展现 |


2. 支持的风格类型

    | 风格类型 |                   描述                   |
    | :------: | :--------------------------------------: |
    |   SIE    | SpannableString.SPAN_INCLUSIVE_EXCLUSIVE |
    |   SEI    | SpannableString.SPAN_EXCLUSIVE_INCLUSIVE |
    |   SII    | SpannableString.SPAN_INCLUSIVE_INCLUSIVE |
    |   SEE    | SpannableString.SPAN_EXCLUSIVE_EXCLUSIVE |

3. 支持的字体

    |    字体     |         描述         |
    | :---------: | :------------------: |
    |   NORMAL    |   Typeface.NORMAL    |
    |    __BOLD__     |    Typeface.BOLD     |
    | ___BOLDITALIC___ | Typeface.BOLD_ITALIC |
    |   _ITALIC_    |   Typeface.ITALIC    |

## 快速开始

```kotlin
getBinding().tv1.text = SpanStrUtils
    .getBuilder("Hello")
    .setFlag(SpanMode.SEE)
    .setTextSize(15F.SP.toInt())
    .build()
```

## 字符串拼接

```kotlin
getBinding().tv1.text = SpanStrUtils
    .getBuilder("Hello")
    .setFlag(SpanMode.SEE)
    .setTextSize(15F.SP.toInt())
    .append("你好")
    .setFlag(SpanMode.SEE)
    .setScriptMode(ScriptMode.Superscript)
    .build()
```