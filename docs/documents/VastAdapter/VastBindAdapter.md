# 使用VastBindAdapter构建适配器

## 快速开始

通过下面的示例，你可以快速将 `VastBindAdapter` 运用到你的项目当中。

### 实现 VastBindAdapterItem 接口

你需要让你列表项实现 `VastBindAdapterItem` 接口， `VastBindAdapterItem` 接口提供了事件点击和获取布局id的功能。

.. tabset::实现 VastBindAdapterItem 接口

    ## Kotlin

    ```kotlin
    // 在Kotlin中使用
    class Person(
        val firstName: String, val lastName: String,
        override var vbAapClickEventListener: VAapClickEventListener? = null,
        override var vbAdpLongClickEventListener: VAdpLongClickEventListener? = null,
    ) :VastBindAdapterItem {

        override fun getVBAdpItemType(): Int {
            return R.layout.item_bind_textview
        }

    }
    ```

    ## Java

    ```java
    // 在Java中使用
    public class Picture implements VastBindAdapterItem {

        private int drawable;
        private VAapClickEventListener clickEventListener;
        private VAdpLongClickEventListener longClickEventListener;

        public Picture(int drawable, VAapClickEventListener clickEventListener, VAdpLongClickEventListener longClickEventListener) {
            this.drawable = drawable;
            this.clickEventListener = clickEventListener;
            this.longClickEventListener = longClickEventListener;
        }

        public int getDrawable() {
            return drawable;
        }

        public void setDrawable(int drawable) {
            this.drawable = drawable;
        }

        @Override
        public int getVBAdpItemType() {
            return R.layout.item_bind_imageview;
        }


        @Nullable
        @Override
        public VAapClickEventListener getVbAapClickEventListener() {
            return clickEventListener;
        }

        @Override
        public void setVbAapClickEventListener(@Nullable VAapClickEventListener value) {
            clickEventListener = value;
        }

        @Nullable
        @Override
        public VAdpLongClickEventListener getVbAdpLongClickEventListener() {
            return longClickEventListener;
        }

        @Override
        public void setVbAdpLongClickEventListener(@Nullable VAdpLongClickEventListener value) {
            longClickEventListener = value;
        }
    }
    ```

### 编辑对应的layout

对于同一列表内的元素，当你使用 `data` 标签将他们绑定进对应的布局时，他们的 `name` 字段应该是一样的。

例如：`Person` 和 `Picture` 在同一列表中，他们的布局文件内 `name` 字段均为 `item` 。

.. details::Person对应的layout

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <layout>
        <data>
            <variable
                name="item"
                type="com.gcode.vastutils.basebindadpexample.model.Person" />
        </data>
        <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
            android:orientation="vertical"
            android:layout_width="match_parent"
            android:layout_height="wrap_content">
            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:gravity="center"
                android:text="@{item.firstName}"/>
            <TextView
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:gravity="center"
                android:text="@{item.lastName}"/>
        </LinearLayout>
    </layout>
    ```

.. details::Picture对应的layout

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <layout>
        <data>
            <variable
                name="item"
                type="com.gcode.vastutils.basebindadpexample.model.Picture" />
        </data>
        <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical">
            <ImageView
                android:id="@+id/item_image"
                android:layout_width="100dp"
                android:layout_height="100dp"
                android:src="@{item.drawable}"
                android:contentDescription="@string/picture"
                android:layout_gravity="center_horizontal"/>
        </LinearLayout>
    </layout>
    ```

### 实现Adapter

.. tabset::实现 Adapter
    :id: tabset2

    ## Kotlin

    ```kotlin
    class BaseBindingAdapter(
        dataSource: MutableList<VastBindAdapterItem>,
        mContext: Context
    ) : VastBindAdapter(dataSource, mContext) {

        override fun setVariableId(): Int {
            return BR.item
        }

    }
    ```

    ## Java

    ```java
    public class BaseBindAdapter extends VastBindAdapter {

        public BaseBindAdapter(@NonNull List<VastBindAdapterItem> dataSource,@NonNull Context mContext) {
            super(dataSource,mContext);
        }

        @Override
        public int setVariableId() {
            return BR.item;
        }

    }
    ```

### 在Activity中使用

下面的示例展示了在 Kotlin 和 Java 环境下的使用

.. tabset::在 Activity 中使用
    :id: tabset3

    ## Kotlin

    ```kotlin
    private val datas:MutableList<VastBindAdapterItem> = ArrayList()

    for(i in 0..10){
        datas.add(Person(i.toString(),i.toString(),null,null))
        datas.add(Picture(R.drawable.ic_knots,null,null))
    }

    // 设置给RecyclerView
    val adapter = BaseBindingAdapter(datas, this)
    dataRv.adapter = adapter
    dataRv.layoutManager = LinearLayoutManager(this)
    ```

    ## Java

    ```java
    private ArrayList<VastBindAdapterItem> datas = new ArrayList<>();

    for (int i = 0; i < 10; i++) {
        datas.add(new Picture(R.drawable.ic_knots, null, null));
    }

    // 设置给RecyclerView
    BaseBindAdapter adapter = new BaseBindAdapter(datas, this);
    dataRv.setAdapter(adapter);
    dataRv.setLayoutManager(new LinearLayoutManager(this));
    ```

<div align="center"><img src="../assets/images/VastAdapter.gif" width=50%/></div>

## 添加点击（或长按）事件

对于列表来说，点击事件是必不可少的，`VastBindAdapter` 支持你为列表设置通用点击事件，当然因为你的类实现了 `VastBindAdapterItem` 接口，因此你也可以单独为其设定点击事件。

### 通用点击事件设置

.. tabset::通用点击事件设置
    :id: tabset4

    ## Kotlin

    ```kotlin
    adapter.setOnItemClickListener(object : VastBindAdapter.OnItemClickListener {
        override fun onItemClick(view: View, position: Int) {
            // Something you want to do
        }
    })
    adapter.setOnItemLongClickListener(object : VastBindAdapter.OnItemLongClickListener {
        override fun onItemLongClick(view: View, position: Int): Boolean {
            // Something you want to do
            return true
        }
    })
    ```

    ## Java

    ```java
    adapter.setOnItemClickListener((view, position) -> {
        // Something you want to do
    });
    adapter.setOnItemLongClickListener((view, position) -> {
        // Something you want to do
        return true;
    });
    ```

### 设置单独点击事件

注意，如果你为某一项单独定义了点击事件，那么它不再支持通用点击事件。

.. tabset::设置单独点击事件
    :id: tabset5

    ## Kotlin

    ```kotlin
    // 定义点击事件
    val click = object : VAapClickEventListener {
        override fun vAapClickEvent(view: View, pos: Int) {
            showShortMsg("Click event and pos is $pos.")
        }
    }

    val longClick = object : VAdpLongClickEventListener {
        override fun vAdpLongClickEvent(view: View, pos: Int): Boolean {
            showShortMsg("Long click event and pos is $pos.")
            return true
        }
    }

    // 在设置数据源的时候设置
    for(i in 0..10){
        datas.add(Person(i.toString(),i.toString(),click,null))
        datas.add(Picture(R.drawable.ic_knots,null,longClick))
    }
    ```

    ## Java

    ```java
    // 定义点击事件
    VAapClickEventListener click = (view, pos) -> {
        ToastUtils.showShortMsg(this, "Click event and pos is " + pos);
    };

    VAdpLongClickEventListener longClick = (view, pos) -> {
        ToastUtils.showShortMsg(this, "Long click event and pos is " + pos);
        return true;
    };

    // 在设置数据源的时候设置
    for (int i = 0; i < 10; i++) {
        datas.add(new Picture(R.drawable.ic_knots, click, longClick));
    }
    ```

<div align="center"><img src="../assets/images/VastAdapterClick.gif" width=50%/></div>

## 为Adapter添加其他功能

下面的示例向你展示了为Adapter增加判断数据源是否为空的功能

.. tabset::设置单独点击事件
    :id: tabset6

    ## Kotlin

    ```kotlin
    class BaseBindingAdapter(
        dataSource: MutableList<VastBindAdapterItem>,
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

    ## Java

    ```java
    public class BaseBindAdapter extends VastBindAdapter {

        public BaseBindAdapter(@NonNull List<VastBindAdapterItem> dataSource,@NonNull Context mContext) {
            super(dataSource,mContext);
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

.. tabset::设置单独点击事件
    :id: tabset7

    ## Kotlin

    ```kotlin
    class BaseBindingAdapter(
        dataSource: MutableList<VastBindAdapterItem>,
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

    ## Java

    ```java
    public class BaseBindAdapter extends VastBindAdapter {

        @BindingAdapter("drawableStartCompat")
        public static void loadImage(TextView tv, int resId) {
            Drawable drawable = ResourcesCompat.getDrawable(App.context.getResources(),resId,null);
            tv.setCompoundDrawablesWithIntrinsicBounds(drawable,null,null,null);
        }
        
        public BaseBindAdapter(@NonNull List<VastBindAdapterItem> dataSource,@NonNull Context mContext) {
            super(dataSource,mContext);
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
