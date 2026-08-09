# skore-ecs-benchmark comparison results

- entities per scenario: 100000
- warm-up runs: 2
- timed runs: 2
- query/system iterations per timed run: 100
- checksum: 18385282514810143344

| scenario | skore_avg(s) | flecs_avg(s) | skore/flecs | skore_ops/s | flecs_ops/s |
| --- | ---: | ---: | ---: | ---: | ---: |
| create_entities | 0.0914173 | 0.00765726 | 11.9386x | 1.09389e+06 | 1.30595e+07 |
| destroy_entities | 0.0169896 | 0.00221998 | 7.65304x | 5.88594e+06 | 4.50454e+07 |
| add_component | 0.101859 | 0.00596927 | 17.0639x | 981748 | 1.67525e+07 |
| remove_component | 0.0775937 | 0.00600247 | 12.927x | 1.28876e+06 | 1.66598e+07 |
| iterate_position | 0.00723569 | 0.00708754 | 1.0209x | 1.38204e+09 | 1.41093e+09 |
| iterate_position_velocity | 0.00845427 | 0.0102004 | 0.828815x | 1.18283e+09 | 9.80351e+08 |
| system_update | 0.0084376 | 0.0082908 | 1.01771x | 1.18517e+09 | 1.20616e+09 |
| deferred_spawn | 0.095231 | 0.0168071 | 5.66612x | 1.05008e+06 | 5.94987e+06 |
