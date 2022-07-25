# Opensourced projects

来自页面: https://www.treasuredata.com/opensource/

Treasuredata 的开源项目, 都是肤浅理解:

- [fluentd](https://www.fluentd.org/): log collector, logstash?
  - Ruby
- [embulk](https://github.com/embulk/embulk): 通过已有的/自己编写的插件处理 input/output, embulk 用来大批量导出导入数据
  - Java
- [hivemall](http://hivemall.incubator.apache.org/): 基于 Hive user defined functions(UDFs)的可扩展机器学习
  - Java, 最新代码: https://github.com/apache/incubator-hivemall
- [MessagePack](https://msgpack.org/): 将 JSON 二进制序列化的一种方法
  - 人肉测试了下压缩程度, 对比原始数据 ~ 60% - 70%
- [digdag](https://www.digdag.io/): pipeline/task runner
  - 能从任务失败的点重新开始(有历史记忆), 能定义任务的分支, 依赖关系
  - Java, 且有 Python Ruby 的 api 支持
- [fluent-bit](https://fluentbit.io/): log collector
  - C, repo: https://github.com/fluent/fluent-bit
  - CNCF 的一篇 blog: [Logstash, Fluentd, Fluent Bit, or Vector? How to choose the right open-source log collector](https://www.cncf.io/blog/2022/02/10/logstash-fluentd-fluent-bit-or-vector-how-to-choose-the-right-open-source-log-collector/)
  - fluentd 的 C 版, 系统开销更小, 但是插件更少, 牺牲了灵活性换取效能.
- [monkey](http://monkey-project.com/): http server, 应该是和 nginx 相同的定位, 但是功能更少更轻量
  - C, repo: https://github.com/monkey/monkey
- [jeromq](https://github.com/zeromq/jeromq): zeromq in pure Java
- [pyenv](https://github.com/pyenv/pyenv): Simple Python version management
  - 作者介绍了实现原理, 可能值得学习: https://github.com/pyenv/pyenv#how-it-works
- [snappy-java](https://github.com/xerial/snappy-java): compressor/decompressor
  - Java, port from [google/snappy](https://github.com/google/snappy)
    - repo 内有与其他 lib 的比较
  - Snappy 并不追求极致压缩, 而是在快速压缩的基础上达到合理的压缩率
- [norikra](http://norikra.github.io/): 'Stream Processing Server with SQL'
  - norikra 能存储事件(JSON document?), 并基于事件做实时查询, 且不需要定义 schema.
  - Ruby, on jRuby (Ruby on Java Virtual Machine)
  - 'SQL' is actually Esper's EPL, 事件处理语言
    - EPL 简单介绍: https://juejin.cn/post/6844903923350765582
  - Ruby, repo: https://github.com/norikra/norikra
- [httpclient](github.com/nahi/httpclient): http client, 类似 axios to nodejs
  - Ruby
  - 说是与 [`libwww-perl`](https://metacpan.org/dist/libwww-perl) 功能相符
