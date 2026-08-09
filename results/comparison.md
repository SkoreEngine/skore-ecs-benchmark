# skore-ecs-benchmark comparison results

- entities per scenario: 100000
- warm-up runs: 2
- timed runs: 5
- query/system iterations per timed run: 100
- checksum: 47369306390000

| scenario | skore_avg(s) | flecs_avg(s) | skore/flecs | skore_ops/s | flecs_ops/s |
| --- | ---: | ---: | ---: | ---: | ---: |
| create_entities | 0.164452 | 0.0078132 | 21.048x | 608079 | 1.27988e+07 |
| destroy_entities | 0.0173988 | 0.00181049 | 9.60996x | 5.74754e+06 | 5.52336e+07 |
| add_component | 0.167365 | 0.00671589 | 24.9208x | 597495 | 1.489e+07 |
| remove_component | 0.112912 | 0.00593189 | 19.0347x | 885646 | 1.6858e+07 |
| iterate_position | 0.00689724 | 0.00608349 | 1.13376x | 1.44986e+09 | 1.64379e+09 |
| iterate_position_velocity | 0.00960977 | 0.00679602 | 1.41403x | 1.04061e+09 | 1.47145e+09 |
| system_update | 0.00737107 | 0.00670893 | 1.09869x | 1.35666e+09 | 1.49055e+09 |
| deferred_spawn | 0.174152 | 0.0125477 | 13.8792x | 574212 | 7.96961e+06 |
