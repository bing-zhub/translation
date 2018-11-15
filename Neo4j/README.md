Cypher是一种声明式图数据库查询语言, 类似关系型数据库中的SQL
1. MATCH: 匹配图模式
2. WHERE: 过滤条件
3. RETURN: 定义返回的结果

基本语法:
1. 增(CREATE)
2. 删(DELETE)
3. 改(SET)
4. 查(MATCH)

eg: 小猪佩奇

## 创建基础节点
`create (:pig{name:"猪爷爷", age:12}), (:pig{name:"猪奶奶", age:11})`
## 基于现有节点创建关系
`match (a:pig{name:"猪爷爷"}) match(b:pig{name:"猪奶奶"}) create (a)-[r:夫妻]->(b)`
## 创建关系和节点
`create (:pig{name:"猪爸爸",age:12}) -[:夫妻]->(:pig{name:"猪妈妈", age:9})`
## 修改属性
`match (a:pig{name:"猪爸爸",age:12}) set a.age=5;`
## 创建多标签节点
`create (a:pig:die{name:"猪祖宗", age:16}) return a.name;`
## 删除节点
`match (n:die) delete n;`

