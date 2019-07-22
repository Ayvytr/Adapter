# SmartAdapter  [![](https://img.shields.io/badge/jCenter-0.1.0-red.svg)](https://bintray.com/ayvytr/maven/smart-adapter/_latestVersion)
Kotlin Android Adapter of RecyclerView, named SmartAdapter.

## Import

Android:

​	implementation "com.ayvytr:smart-adapter:{latestVersion}"

Androidx:

​	implementation "com.ayvytr:smart-adapter-androidx:{latestVersion}"



## [Javadoc](https://ayvytr.github.io/projects/smartadapter/javadoc/index.html)



## Usage: 

```kotlin
//single item view
recycler_view.bind(list, R.layout.item, 1) { item: Item ->    
	item_text.text = item.value    
}}.build()


```



```kotlin
//multiple item view:
recycler_view.bind(list, R.layout.item, 1) { item: Item ->
            item_text.text = item.value
        }
        	//anther item view
            .map(R.layout.item_second, 2) { item: Item ->
                item_second_text.text = item.value
            }
            .map(R.layout.item_custom, 3) { item: Item ->
                item_custom_text.text = item.value
            }
            .map(BindMap4())
            //add custom diff util
            //            .diff({ oldItem, newItem -> oldItem.type == newItem.type },
            //                  { oldItem, newItem -> oldItem.value == newItem.value },
            //                  { oldItem, newItem ->
            //                      if (oldItem.value != newItem.value) {
            //                          newItem
            //                      } else null
            //                  },
            //                  { holder, item, payloads -> holder.bind(item) })
            //another way to add custom diff util
            .diff(Diff())
            //how to get item type from your item.
            .type { it.type }
            //item click listener
            .click { item: Item, i: Int ->
                toast("clicked $i $item")
            }
            //item long click listener
            .longClick { item: Item, i: Int ->
                toast("long clicked $i $item")
            }
            //real method to create adapter
            .build()
            
class Diff : SmartDiffCallback<Item>({ oldItem, newItem -> oldItem === newItem },
                                     { oldItem, newItem -> oldItem === newItem && oldItem.value == newItem.value },
                                     { item: Item, item1: Item -> },
                                     { param: Any, item: Item, mutableList: MutableList<Any> -> }
)

class BindMap4 : SmartContainer<Item>(R.layout.item_4, 4, { item_text_4.text = it.value }) {
}
```















