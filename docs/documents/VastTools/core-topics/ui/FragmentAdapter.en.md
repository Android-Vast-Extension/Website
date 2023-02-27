# FragmentAdapter

`VastFragmentAdapter` can facilitate you to quickly build a view pager2 suitable for [ViewPager2](https://developer.android.com/reference/kotlin/androidx/viewpager2/widget/ViewPager2).

## Get started

You can add `VastFragmentAdapter` to your `Activity` in the following way:

```kotlin
vp2.adapter =
     VastFragmentAdapter(this@BaseFragmentActivity, ArrayList<Fragment>().apply {
         add(OneFragment())
         add(TwoFragment())
         add(ThreeFragment())
     })
```