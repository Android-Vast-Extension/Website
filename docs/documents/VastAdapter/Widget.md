# 组件

本文介绍了与适配器有关的一些组件

## AdapterDiffUtil 

该组件主要用来替代 `DiffUtil.ItemCallback`

=== "kotlin"

    ```kotlin
    class PictureDiffUtil : AdapterDiffUtil<Picture, PictureWrapper>() {
        override fun newAreItemsTheSame(oldItem: Picture, newItem: Picture): Boolean {
            return oldItem.drawable == newItem.drawable
        }

        override fun newAreContentsTheSame(oldItem: Picture, newItem: Picture): Boolean {
            return oldItem.drawable == newItem.drawable
        }
    }
    ```

=== "java"

    ```kotlin
    public class PersonDiffUtil extends AdapterDiffUtil<Person, PersonWrapper> {

        public PersonDiffUtil() {
        }

        @Override
        public boolean newAreContentsTheSame(Person oldItem, Person newItem) {
            return Objects.equals(oldItem.getFirstName(), newItem.getFirstName()) && Objects.equals(oldItem.getLastName(), newItem.getLastName());
        }

        @Override
        public boolean newAreItemsTheSame(Person oldItem, Person newItem) {
            return Objects.equals(oldItem.getFirstName(), newItem.getFirstName()) && Objects.equals(oldItem.getLastName(), newItem.getLastName());
        }

    }
    ```

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