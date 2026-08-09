# skore-ecs-benchmark comparison results

- entities per scenario: 100000
- warm-up runs: 2
- timed runs: 5
- query/system iterations per timed run: 100
- checksum: 378703165042278712

| scenario | skore_avg(s) | flecs_avg(s) | skore/flecs | skore_ops/s | flecs_ops/s |
| --- | ---: | ---: | ---: | ---: | ---: |
| create_entities | 0.00670443 | 0.00932831 | 0.718719x | 1.49155e+07 | 1.07201e+07 |
| destroy_entities | 0.00442625 | 0.00210826 | 2.09948x | 2.25925e+07 | 4.74324e+07 |
| add_component | 0.00988212 | 0.00634764 | 1.55682x | 1.01193e+07 | 1.57539e+07 |
| remove_component | 0.0080192 | 0.00563592 | 1.42287x | 1.24701e+07 | 1.77433e+07 |
| iterate_position | 0.011169 | 0.00708693 | 1.576x | 8.95332e+08 | 1.41105e+09 |
| iterate_position_velocity | 0.00899805 | 0.00785995 | 1.1448x | 1.11135e+09 | 1.27227e+09 |
| system_update | 0.00787477 | 0.00633047 | 1.24395x | 1.26988e+09 | 1.57966e+09 |
| deferred_spawn | 0.0070335 | 0.0140021 | 0.502317x | 1.42177e+07 | 7.14178e+06 |
