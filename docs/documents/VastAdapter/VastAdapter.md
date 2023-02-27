# VastAdapter

> 如果可以的话，还是推荐使用**VastBindingAdapter**

## 快速开始

通过下面的示例，你可以快速的将 `VastAdapter` 运用到你的项目当中

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

=== "Picture 对应的 layout"

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical">

        <ImageView
            android:id="@+id/item_image"
            android:layout_width="100dp"
            android:layout_height="100dp"
            android:layout_gravity="center_horizontal"
            android:contentDescription="@string/picture" />
    </LinearLayout>
    ```

=== "Person 对应的 layout"

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical">

        <com.google.android.material.textview.MaterialTextView
            android:id="@+id/firstName"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:gravity="center" />

        <com.google.android.material.textview.MaterialTextView
            android:id="@+id/lastName"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:gravity="center" />
    </LinearLayout>
    ```

### 实现 ViewHolder

=== "kotlin"

    ```kotlin
    class PictureHolder(itemView: View) : BaseHolder(itemView) {

        private val iv: ImageView

        override fun onBindData(item: Any) {
            iv.setImageResource(cast<Picture>(item).drawable)
        }

        class Factory : HolderFactory {

            override fun onCreateHolder(
                parent: ViewGroup,
                viewType: Int
            ): BaseHolder {
                val inflater = LayoutInflater.from(parent.context)
                val itemView: View = inflater.inflate(R.layout.item_imageview, parent, false)
                return PictureHolder(itemView)
            }

            override fun getHolderType(): String {
                return Picture::class.java.simpleName
            }

        }

        init {
            iv = itemView.findViewById(R.id.item_image)
        }
    }
    ```

=== "java"

    ```java
    public class PersonHolder extends BaseHolder {

        private final MaterialTextView firstName;
        private final MaterialTextView lastName;
        private View itemView;

        public PersonHolder(@NonNull View itemView) {
            super(itemView);
            firstName = itemView.findViewById(R.id.firstName);
            lastName = itemView.findViewById(R.id.lastName);
        }

        @Override
        public void onBindData(@NonNull Object item) {
            try {
                Person person = Cast.cast(item);
                firstName.setText(person.getFirstName());
                lastName.setText(person.getLastName());
            } catch (Exception e) {
                e.printStackTrace();
            }
        }

        public final static class Factory implements HolderFactory {

            @NonNull
            @Override
            public BaseHolder onCreateHolder(@NonNull ViewGroup parent, int viewType) {
                return new PersonHolder(
                        LayoutInflater.from(parent.getContext()).inflate(R.layout.item_textview, parent, false)
                );
            }

            @NonNull
            @Override
            public String getHolderType() {
                return Person.class.getSimpleName();
            }

        }

    }
    ```

### 实现 Wrapper

具体可以参考 [AdapterItemWrapper](https://ave.entropy2020.cn/documents/VastAdapter/Widget/#adapteritemwrapper)

### 实现 Adapter

=== "kotlin"

    ```kotlin
    class BaseAdapter(
        private val items: MutableList<AdapterItemWrapper<*>>,
        factories: MutableList<BaseHolder.HolderFactory>
    ) : VastAdapter(items, factories)
    ```

=== "java"

    ```java
    public class BaseAdapter extends VastAdapter {

        public BaseAdapter(@NonNull List<AdapterItemWrapper<?>> mDataSource, @NonNull List<BaseHolder.HolderFactory> mFactories) {
            super(mDataSource, mFactories);
        }
        
    }
    ```

### 在 Activity 中使用

=== "kotlin"

    ```kotlin
    // 获取数据源
    private val datas: MutableList<AdapterItemWrapper<*>> = ArrayList()

    for (i in 0..10) {
        datas.add(PersonWrapper(Person(i.toString(), i.toString())))
        datas.add(PictureWrapper(Picture(R.drawable.ic_knots), click, longClick))
    }

    // 设置给RecyclerView
    adapter = BaseAdapter(datas, mutableListOf(PersonHolder.Factory(), PictureHolder.Factory()))

    // dataRv是RecyclerView
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
    adapter = new BaseAdapter(datas, Arrays.asList(new PersonHolder.Factory(),new PictureHolder.Factory()));

    getBinding().dataRv.setAdapter(adapter);
    getBinding().dataRv.setLayoutManager(new LinearLayoutManager(this));
    ```

<figure markdown>
  ![VastAdapter](../VastAdapter/img/vba_1.gif){ width="200" }
  <figcaption>列表</figcaption>
</figure>

## 添加点击（或长按）事件

对于列表来说，点击事件是必不可少的，`VastAdapter` 支持你为列表设置通用点击事件。

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

## 添加新的数据类型

如果你想向列表中添加第三种类型的数据，你只需要以下三步：

- 定义新的数据类型，例如 **CExample** 。

- 定义 **CExample** 对应的 ViewHolder ，例如 **CViewHolder** 。

- 将其对应的 **Factory** 添加到adapter中
  
=== "kotlin"

    ```kotlin
    adapter = BaseAdapter(datas, mutableListOf(PersonHolder.Factory(), PictureHolder.Factory(),CViewHolder.Factory()))
    ```

=== "java"

    ```java
    adapter = new BaseAdapter(datas, Arrays.asList(new PersonHolder.Factory(),new PictureHolder.Factory(),new CViewHolder.Factory()));
    ```

## 为Adapter添加其他功能

下面的示例向你展示了为Adapter增加判断数据源是否为空的功能

=== "kotlin"

    ```kotlin
    class BaseAdapter(
        private val items: MutableList<AdapterItemWrapper<*>>,
        factories: MutableList<BaseHolder.HolderFactory>
    ) : VastAdapter(items, factories) {

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
    public class BaseAdapter extends VastAdapter {

        public BaseAdapter(@NonNull List<AdapterItemWrapper<?>> mDataSource, @NonNull List<BaseHolder.HolderFactory> mFactories) {
            super(mDataSource, mFactories);
        }

        public Boolean isEmpty(){
            return getDataSource().isEmpty();
        }

    }
    ```

当然你也可以参考示例应用

## 引用

BaseVastAdapter部分设计参考自[彻底解耦 RecyclerView.Adapter](https://puke3615.github.io/2018/08/26/Android-RecyclerView-Architecture-Design/)