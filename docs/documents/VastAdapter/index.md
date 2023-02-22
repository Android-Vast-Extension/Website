# 概览

## 特性

- 👍 支持有DataBinding和无DataBinding两种模式
- 👍 支持多种数据类型
- 👍 支持为不同数据类型添加不同的点击事件
- 👍 支持点击和长按两种事件
- 👍 支持快速添加新的数据类型

## Adapter对比

|适配器|数据绑定|同一列表支持多种数据类型|支持自定义点击事件|适用场景|ViewHolder类型|
|:-:|:-:|:-:|:-:|:-:|:-:|
|VastAdapter|❌|✅|✅|RecyclerView||
|VastListAdapter|❌|❌|✅|RecyclerView||
|VastBindAdapter|✅|✅|✅|RecyclerView➕DiffUtil||
|VastBindListAdapter|✅|❌|✅|RecyclerView➕DiffUtil||
|VastBindPagingAdapter|✅|❌|✅|RecyclerView➕Paging||