# skore-ecs-benchmark comparison results

- entities per scenario: 100000
- warm-up runs: 2
- timed runs: 5
- query/system iterations per timed run: 100
- checksum: 119608025529572

| scenario | skore_avg(s) | flecs_avg(s) | skore/flecs | skore_ops/s | flecs_ops/s |
| --- | ---: | ---: | ---: | ---: | ---: |
| create_entities | 0.00759104 | 0.00975929 | 0.777827x | 1.31734e+07 | 1.02466e+07 |
| destroy_entities | 0.0057795 | 0.00236799 | 2.44068x | 1.73025e+07 | 4.22299e+07 |
| add_component | 0.0113339 | 0.00763368 | 1.48472x | 8.82308e+06 | 1.30998e+07 |
| remove_component | 0.0122071 | 0.0067019 | 1.82144x | 8.19196e+06 | 1.49212e+07 |
| iterate_position | 0.0133162 | 0.00650976 | 2.04558x | 7.50962e+08 | 1.53616e+09 |
| iterate_position_velocity | 0.00943958 | 0.00746083 | 1.26522x | 1.05937e+09 | 1.34033e+09 |
| system_update | 0.00913175 | 0.00805081 | 1.13426x | 1.09508e+09 | 1.24211e+09 |
| deferred_spawn | 0.00702934 | 0.014237 | 0.493739x | 1.42261e+07 | 7.02397e+06 |
