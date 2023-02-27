# VastBindAdapter

## 快速开始

通过下面的示例，你可以快速将 `VastBindAdapter` 运用到你的项目当中。

### 创建数据对象

=== "kotlin"

    ```kotlin
    data class Picture(val drawable: Int)
    ```

=== "java"

    ```java
    public class Person {
        private String firstName;
        private String lastName;

        ... // 构造函数、get和set方法

    }
    ```

### 编辑对应的 Layout

!!! warning "关于布局内 variable 标签 name 字段的说明"

    对于同一列表内的元素，当你使用 `data` 标签将他们绑定进对应的布局时，他们的 `name` 字段应该是一样的。

    例如：`Person` 和 `Picture` 在同一列表中，他们的布局文件内 `name` 字段均为 `item` 。

=== "Picture 对应的 layout"

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <layout>
        <data>
            <variable
                name="item"
                type="com.ave.vastgui.app.activity.adpexample.model.Picture" />
        </data>

        <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical">

            <ImageView
                android:id="@+id/item_image"
                android:layout_width="100dp"
                android:layout_height="100dp"
                android:layout_gravity="center_horizontal"
                android:contentDescription="@string/picture"
                android:src="@{item.drawable}" />
        </LinearLayout>
    </layout>
    ```

=== "Person 对应的 layout"

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <layout>
        <data>
            <variable
                name="item"
                type="com.ave.vastgui.app.activity.adpexample.model.Person" />
        </data>

        <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical">

            <com.google.android.material.textview.MaterialTextView
                android:layout_width="match_parent"
                android:layout_height="20dp"
                android:gravity="center"
                android:text="@{item.firstName}" />

            <com.google.android.material.textview.MaterialTextView
                android:layout_width="match_parent"
                android:layout_height="20dp"
                android:gravity="center"
                android:text="@{item.lastName}" />
        </LinearLayout>
    </layout>
    ```

### 实现 Wrapper

具体可以参考 [AdapterItemWrapper](https://ave.entropy2020.cn/documents/VastAdapter/Widget/#adapteritemwrapper)

### 实现 Adapter

=== "kotlin"

    ```kotlin
    class BaseBindAdapter(
        dataSource: MutableList<AdapterItemWrapper<*>>,
        mContext: Context
    ) : VastBindAdapter(dataSource, mContext) {

        override fun setVariableId(): Int {
            return BR.item
        }

    }
    ```

=== "java"

    ```java
    public class BaseBindAdapter extends VastBindAdapter {

        public BindAdapter1(@NonNull List<AdapterItemWrapper<?>> mDataSource, @NonNull Context mContext) {
            super(mDataSource, mContext);
        }


        @Override
        public int setVariableId() {
            return BR.item;
        }

    }
    ```

### 在 Activity 中使用


=== "kotlin"

    ```kotlin
    private val datas: MutableList<AdapterItemWrapper<Any>> = ArrayList()

    for (i in 0..10) {
        datas.add(PersonWrapper(Person(i.toString(), i.toString())))
        datas.add(PictureWrapper(Picture(R.drawable.ic_knots), click, longClick))
    }

    // 设置给RecyclerView
    val adapter = BaseBindAdapter(datas, this)
    dataRv.adapter = adapter
    dataRv.layoutManager = LinearLayoutManager(this)
    ```

=== "java"

    ```java
    private final ArrayList<AdapterItemWrapper<?>> datas = new ArrayList<>();

    for (int i = 0; i < 10; i++) {
        Picture picture = new Picture(R.drawable.ic_knots);
        PictureWrapper pictureWrapper = new PictureWrapper(picture,null,null);
        datas.add(pictureWrapper);
        Person person = new Person(String.valueOf(i),String.valueOf(i));
        PersonWrapper personWrapper = new PersonWrapper(person);
        datas.add(personWrapper);
    }

    // 设置给RecyclerView
    BaseBindAdapter adapter = new BaseBindAdapter(datas, this);
    getBinding().dataRv.setAdapter(adapter);
    getBinding().dataRv.setLayoutManager(new LinearLayoutManager(this));
    ```

<figure markdown>
  ![VastBindAdapter](../VastAdapter/img/vba_1.gif){ width="200" }
  <figcaption>列表</figcaption>
</figure>

## 添加点击（或长按）事件

对于列表来说，点击事件是必不可少的，`VastBindAdapter` 支持你为列表设置通用点击事件。

### 通用点击事件设置

=== "kotlin"

    ```kotlin
    adapter.registerClickEvent(object : AdapterClickListener {
        override fun onItemClick(view: View, pos: Int) {
            // Something you want to do
        }
    })
    adapter.registerLongClickEvent(object : AdapterLongClickListener {
        override fun onItemLongClick(view: View, pos: Int): Boolean {
            // Something you want to do
            return true
        }
    })
    ```

=== "java"

    ```java
    adapter.registerClickEvent((view, pos) -> {
        // Something you want to do
    });
    adapter.registerLongClickEvent((view, pos) -> {
        // Something you want to do
        return true;
    });
    ```

### 设置单独点击事件

!!! warning 

    如果你为某一项单独定义了点击事件，那么它不再支持通用点击事件。


=== "kotlin"

    ```kotlin
    // 定义点击事件
    val click = object : AdapterClickListener {
        override fun onItemClick(view: View, pos: Int) {
            // Something you want to do
            ToastUtils.showShortMsg("This is a click listener.")
        }
    }

    val longClick = object : AdapterLongClickListener {
        override fun onItemLongClick(view: View, pos: Int): Boolean {
            // Something you want to do
            ToastUtils.showShortMsg("This is a long click listener.")
            return true
        }
    }

    // 在设置数据源的时候设置
    for (i in 0..10) {
        datas.add(PictureWrapper(Picture(R.drawable.ic_knots), click, longClick))
    }
    ```

=== "java"

    ```java
    // 定义点击事件
    AdapterClickListener click = (view, pos) -> {
        ToastUtils.showShortMsg("Click event and pos is " + pos);
    };

    AdapterLongClickListener longClick = (view, pos) -> {
        ToastUtils.showShortMsg("Long click event and pos is " + pos);
        return true;
    };

    // 在设置数据源的时候设置
    for (int i = 0; i < 10; i++) {
        Picture picture = new Picture(R.drawable.ic_knots);
        PictureWrapper pictureWrapper = new PictureWrapper(picture,click,longClick);
        datas.add(pictureWrapper);
    }
    ```

<figure markdown>
  ![VastBindAdapter](../VastAdapter/img/vba_2.gif){ width="200" }
  <figcaption>点击事件</figcaption>
</figure>

## 为Adapter添加其他功能

下面的示例向你展示了为Adapter增加判断数据源是否为空的功能

=== "kotlin"

    ```kotlin
    class BaseBindAdapter(
        dataSource: MutableList<AdapterItemWrapper<*>>,
        mContext: Context
    ) : VastBindAdapter(dataSource, mContext) {

        /**
        * 如果集合为空（不包含任何元素），则返回true，否则返回false。
        * @return Boolean
        */
        fun isItemEmpty() = dataSource.isEmpty()

        override fun setVariableId(): Int {
            return BR.item
        }

    }
    ```

=== "java"

    ```java
    public class BaseBindAdapter extends VastBindAdapter {

        public BindAdapter1(@NonNull List<AdapterItemWrapper<?>> mDataSource, @NonNull Context mContext) {
            super(mDataSource, mContext);
        }

        @Override
        public int setVariableId() {
            return BR.item;
        }

        public Boolean isEmpty(){
            return getDataSource().isEmpty();
        }

    }
    ```

当然你也可以参考示例应用

## 绑定适配器使用

在使用 `DataBinding` 时，我们有时需要自定义一些内容，下面的示例为你演示了如何在 `VastBindAdapter` 里面使用 `@BindingAdapter` 。

当然，如果你想了解更多，你可以点击[绑定适配器](https://developer.android.google.cn/topic/libraries/data-binding/binding-adapters)了解更多。

=== "kotlin"

    ```kotlin
    class BaseBindAdapter(
        dataSource: MutableList<AdapterItemWrapper<*>>,
        mContext: Context
    ) : VastBindAdapter(dataSource, mContext) {

        companion object {
            @JvmStatic @BindingAdapter("android:src")
            fun setImageUri(view: ImageView, imageUri: String?) {
                if (imageUri == null) {
                    view.setImageURI(null)
                } else {
                    view.setImageURI(Uri.parse(imageUri))
                }
            }
        }

        override fun setVariableId(): Int {
            return BR.item
        }

    }
    ```

=== "java"

    ```java
    public class BaseBindAdapter extends VastBindAdapter {

        public BindAdapter1(@NonNull List<AdapterItemWrapper<?>> mDataSource, @NonNull Context mContext) {
            super(mDataSource, mContext);
        }

        @BindingAdapter("drawableStartCompat")
        public static void loadImage(TextView tv, int resId) {
            Drawable drawable = ResourcesCompat.getDrawable(App.context.getResources(),resId,null);
            tv.setCompoundDrawablesWithIntrinsicBounds(drawable,null,null,null);
        }

        @Override
        public int setVariableId() {
            return BR.item;
        }

        public Boolean isEmpty(){
            return getDataSource().isEmpty();
        }

    }
    ```
