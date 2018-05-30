# id-service
分布式环境下的ID生成器
  0          41     51          64
  +-----------+------+------------+
  |timestamp  | node |increment   |
  +-----------+------+------------+

前面0-41位为时间戳偏移值， 选择一个基准时间戳  基准时间戳约接近当前时间生成的ID值约小，长度也越短
42-51 位为机器码 生成的方式可以有多种，这儿使用本机IP地址的hashcode对1024去摸得到，一个集群中要保证每台机器的node值不一样，否则可能出新重复ID
 最后12位递增数字  增长到4095就归零， 如果同一台服务器上同一毫秒生成的ID数量超过 4096则会重复  （个人认为这样的情况实际中不会出现）