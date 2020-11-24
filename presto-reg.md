### reg

#### 前置约定
> 用于约定下文中的一些规则，并且下文不会再进行解释

##### 1. 约定 ${table_name} 表示这里需要放置一张表的名称，可以是数据库中的任何表

##### 2. 约定 ${field} 表示这里需要放置 ${table_name} 表中的字段

#### 常用正则含义
##### 1. `.`(小数点)
> 匹配除了换行符以外的任何字符

```
// 如果field不是换行符，那么这行数据就会被查询出来
SELECT * FROM ${table_name} where regexp_like(${field}, '.');
```

##### 2. `*`(星号)
> 匹配前一个表达式0次或者多次，等价于{0,}
```
SELECT * FROM ${table_name} where regexp_like(${field},'a*')
```

##### 3. `+`(加号)
> 匹配前一个表达式1次或者多次，等价于{1,}

##### 4. `?`(问号)
> 匹配前一个表达式0次或者1次，等价于{0,1}

#### `regexp_like`(string, pattern) → boolean

##### 判断是否是数字

```sql
// \d 表示数字，+ 表示一个或者多个，b在这里表示字符串b，所以正则的含义就是【一个或者多个数字后面有b】
SELECT regexp_like('1a 2b 14m', '\d+b');

// 这个sql表示从【table_name】表中查找【field】字段满足正则【pattern】的数据
SELECT * FROM ${table_name} where regexp_like(${field}, pattern);

// regexp_like 函数有两个参数，第一个参数是变量，第二个参数是正则表达式，返回值是true或者false
```

##### 判断是否是中文

```sql
// 判断是否是中文，[\u4e00-\u9fa5] 代表着中文字符，{6}代表6个中文，这里的数字就代表匹配几个
SELECT regexp_like('中文字符串啊', '[\u4e00-\u9fa5]{6}');
```
