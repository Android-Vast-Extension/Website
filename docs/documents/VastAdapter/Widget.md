# 组件

本文介绍了与适配器有关的一些组件

## AdapterItemWrapper

该组件主要用来实现以下功能

1. 匹配数据项的布局 id
2. 匹配数据项的 [BaseHolder](https://ave.entropy2020.cn/documents/VastAdapter/VastAdapter/#viewholder)
3. 实现数据项自定义事件

=== "kotlin"

    ```kotlin
    class PictureWrapper(
        picture: Picture,
        clickListener: AdapterClickListener?,
        longClickListener: AdapterLongClickListener?
    ) : AdapterItemWrapper<Picture>(
        picture,
        "Picture",
        R.layout.item_bind_imageview,
        clickListener,
        longClickListener
    )
    ```

=== "java"

    ```java
    public class PersonWrapper extends AdapterItemWrapper<Person> {

        public PersonWrapper(Person mData) {
            super(mData, "Person", R.layout.item_bind_textview);
        }

    }
    ```