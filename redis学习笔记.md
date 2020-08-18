HGETALL HASHKEY //获取所有的key/value

hdel hashkey //删除key对应的hash

hexists  haskey key  //判断是否含有该key,有则返回1无则返回0

hkeys hashkey //查询所有的key

hvals hashkey //查询所有的value

HINCRBY/HINCRBYFLOAT  hashkey key  num //增值步长

hsetex  hashkey key //设置过期   

hsetnx hashkey key val //如果不存在则插入，存在返回0啥也不做





Zset:

zadd zset01 zsetkey k1 score1 v1 k2 score2 v2   //插入zset

zrange zsetkey  0  -1 //拿到的是key

 zrange zsetkey  0  -1  withscore //拿到的是key,score

zrangebyscore zetkey  60  90 //60到90的

60  {90   //大于等于60小于90

{60  {90  //大于60小于90

zrangebyscore zetkey  60  90 limit index  num //60到90的,从index开始截取num个

zrem zsetkey key //删除该key

zcard zsetkey //获取数量

zcount zsetkey 60 80  //60到80分的数量

zrank zsetkey v4 //返回该key的下标

zscore zsetkey v  //返回该key的分数

zrevrank zsetkey key //逆序获得下标

zrevrange zsetkey 0 -1 //逆序获得zset

zrevrangebyscore zsetkey end_index start_index //从后面的下标到前面的下标 



log日志级别：debug verbose notice warning

