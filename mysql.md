````
1. 通常情况下使用varchar(20)和varchar(255)占用的空间都是一样的,但是使用索引长度有所不同。使用变长字段需要额外增加2个字节，使用NULL需要额外增加1个字节，因此对于是索引的字段，最好使用定长和NOT NULL定义，提高性能
2. 表字段的类型其实是有长度限制，int类型最大为255等等。一个表，所有字段的长度加起来不能超过65535字节，是字节不是字符 。不包括text blob类型的字段。
````