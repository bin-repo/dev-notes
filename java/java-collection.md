# java Collection（集合类）

## 简介

- 数组（元素可以是基本类型值、对象）
- 集合类（元素只能是对象）
- 保存的对象实际是对象的引用变量
- `Set`（无序、不可重复）
- `List`（有序、可重复）
- `Map`（映射关系）
- `Queue`（队列）

## `Collection`（接口）

### `Set`（接口）

- `HashSet`（实现）存储有序
- `LinkedHashSet`（子类）存储有序+链表结构，插入慢遍历快
- `SortedSet`（接口）
- `TreeSet`（实现）自然排序或自定义排序 `compare(obj_1, obj_2)`
- `EnumSet`（实现）专为枚举类设计的集合类，元素必须是指定枚举类型的枚举值

### `List`（接口）

- `ArrayList`（实现）
- `Vector`（实现）古老
- `Stack`（子类）
- `LinkedList`（实现）栈

### `Queue`（接口）

- `Deque`（接口）双端队列
- `LinkedList`（实现）队列
- `ArrayDeque`（实现）
- `PriorityQueue`（实现）元素按自然排序|自定义排序，而非按加入顺序排序

## Map（接口）key-value

- `HashMap`（实现）
- `LinkedHashMap`（子类）
- `SortedMap`（接口）
- `TreeMap`（实现）红黑树数据结构
- `EmumMap`（实现）
- `HashTable`（实现）古老
- `Properties`（子类）处理属性文件
- `WeakHashMap`（实现）对象为弱引用（当系统进行垃圾回收时回收了所引用对象，则该类会自动清除对应元素）
- `IdentityHashMap`（实现）严格区分不同的key

## Collections（工具类）

- 提供许多静态方法操作集合对象
