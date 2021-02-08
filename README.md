## What is TensorBase
TensorBase is a modern engineering effort for building a high performance and cost-effective bigdata warehouse in an open source culture. 

## News
* [Status of this project](https://github.com/tensorbase/tensorbase/issues/15)

More infos would be uncovered in recent weeks. Stay tuned!

* [TensorBase joins Rust China Conf 2020!](https://2020conf.rustcc.cn/schedule.html)

Let's do a year summary for Base's 2020 wonderful journey with Rust.

Base has missed the planned 2020.11 milestone, in that I want a solid new release. The backend engine is 80% ready in the early of Nov. But I still fight for the server side. This is the price to make compatibility with the ClickHouse communication protocol. The good news is that an order of magnitude higher (than official CH server) raw packet throughput sever is out in these near days.

Let me see if I could give more infos for wonderful outcomes in Rust China Conf 2020.


* [TensorBase joins Rust Fest Global 2020!](https://rustfest.global/session/18-architect-a-high-performance-sql-query-engine-in-rust/)

The core works and practices of TensorBase will be presented with the Rust context in mind. And more, current progress (a.k.a. TensorBase 2020.11) will be shown as possible.

Let's meet in the talk, all data nerds!


## Status

TensorBase has released **milestone 0** as the developer previewing release for inviting more interesting contributors to join in. 

Current development is active in background and this repo is not synced regularly because it is planned to introduce different editions from m1 and there is no external contribution now.


* **TensorBase is an architectural performance design.** 

[It is demonstrated](https://tensorbase.io/2020/08/04/hello-base.html#benchmark) to **query ~1.5 billion rows of NYC taxi dataset in ~100 milliseconds** for total response time in its milestone 0. This is **6x faster than that of ClickHouse**.

<p></p>
<p align="center">
<img width="500" src="https://tensorbase.io/img/2020-08-04-hello-base/base_m0.png"/>
</p>
<p align="center"">Aggregation results in Base's baseshell (95 - 118ms)</p>

<p></p>
<p align="center">
<img width="500" src="https://tensorbase.io/img/2020-08-04-hello-base/clickhouse_20527.png"/>
</p>
<p align="center">Aggregation result in ClickHouse client (0.642s or 642ms)</p>


* **TensorBase is a highly hackable system** 

TensorBase is written from scratch in Rust language and its friend C. Here with comfortable languages, minimized dependencies and from-scratch architectings, you now can use the most familiar tools to challenge the most difficult problems. 

* **Read more from [launch post](https://tensorbase.io/2020/08/04/hello-base.html)**.


If you like this project, please give a star to help it more grown.

## Roadmap

The coming [m1](https://github.com/tensorbase/tensorbase/milestone/1) will be the first milestone which is targeted to provide a production-friendly release. 

A speicial edition will be shown to the interesting personals and oraganizations. Subscribe to [TensorBase's Newsletter here](https://tensorbase.io/#contact) to get the first time information if you are interesting.

## Try TensorBase
TensorBase is developed for Linux, but should work for any docker enabled system (for example, Windows 10 WSL2).

* from source

TensorBase follows the idiomatic development flow of Rust. Make sure your Rust nightly toolchain works. If you only try to run, just play with [Quick Start](#quick-start). Thanks to the strong rust ecosystem, it is not necessary to run build first. Please check [prerequisites](https://github.com/tensorbase/tensorbase/blob/master/docs/dev.md#prerequisites) before running from soruce.

* docker

This mode is portable (but has some platform dependent resource and performance effects).

Try like this:

```bash
docker pull tensorbase/tensorbase:m0
docker run -ti tensorbase/tensorbase:m0 /bin/bash
>> /base/baseshell
```

then run a sum agg sql with the preshipped data (1MB):
```sql
select sum(trip_id) from nyc_taxi
```
<img width="399" src="https://tensorbase.io/img/2020-08-04-hello-base/base_m0_docker_run.png"/>

## Quick Start
Now TensorBase provides two binaries to enable the following workflow:

* baseops: cli/workbench for devops, including kinds of processes/roles starts/stop

* baseshell: query client (now is a monolithic to include everything), m0 only supports query with single integer column type sum aggregation intentionally.

1. run _baseops_ to create a table definition in Base
```bash
cargo run --bin baseops table create -c samples/nyc_taxi_create_table_sample.sql
```
Base explicitly separates write/mutation behaviors into the cli baseops. the provided sql file is just an ansi-SQL DDL script, which can be seen in the [*samples* directory of repo](samples).

2. run _baseops_ to import [nyc_taxi csv dataset](https://clickhouse.tech/docs/en/getting-started/example-datasets/nyc-taxi/) into Base
```bash
cargo run --release --bin baseops import csv -c /jian/nyc-taxi.csv -i nyc_taxi:trip_id,pickup_datetime,passenger_count:0,2,10:51
```
Base import tool uniquely supports to import csv partially into storage like above. Use help to get more infos.

3. run _baseshell_ to issue query against Base
```bash
cargo run --release --bin baseshell
```

[Dev Docs](/docs/dev.md) provides a little more explanation for why above commands work.


## Engineering Efforts
Find more infos in [dev page](https://github.com/tensorbase/tensorbase/blob/master/docs/dev.md#engineering).

## Communications

Feel free to feedback any problem via [issues](https://github.com/tensorbase/tensorbase/issues).

Free-style discuss: (Discord is recommended currently especially when Slack invite link expired)

[Discord Server](https://discord.gg/jYgmE2zsAG)

[Slack Channel](https://join.slack.com/t/tensorbase/shared_invite/zt-lxr2c0a9-~5gv5nXzPuVJ7JosR6R9iQ)

WeChat Group

![Wechat Group](https://user-images.githubusercontent.com/237573/103256605-d1f95f80-49c8-11eb-8cab-00b0d0bb7992.png)


## Contributing
Thanks for your contributions!

[Dev Docs](/docs/dev.md)


## License
TensorBase is distributed under the terms of the Apache License (Version 2.0).

See [LICENSE](LICENSE) for details.

