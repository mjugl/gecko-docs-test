# Performance metrics

Gecko comes with its own benchmark suite to verify its use for the generation of large datasets.
We have tested all built-in generators and corrupts and verified that their processing time scales linearly as the amount of records to generate increases.
This means that if you generate two datasets with 10,000 and 20,000 records, you can expect that the second one will take twice as long as the first one to generate.

In fact, we found that the more records are being generated at once, the processing time per record slightly decreases.
These performance gains are miniscule, but prove Gecko's ability to scale well beyond generating millions of records at a time.

We ran these benchmarks on a virtual server within a containerized environment with the following configuration.

- **vCPU:** 8x Intel Xeon Gold 6240R
- **RAM:** 128 GB
- **OS:** Ubuntu 20.04.6
- **Kernel:** Linux 5.4.0
- **Python:** 3.11.6

| Function                                   |   Records |   Time per call (ms) |   Time per record (ns) |
|:-------------------------------------------|----------:|---------------------:|-----------------------:|
| generator.from_multicolumn_frequency_table |       100 |                 0.32 |                3175.81 |
| generator.from_multicolumn_frequency_table |       500 |                 0.83 |                1669.14 |
| generator.from_multicolumn_frequency_table |      1000 |                 1.35 |                1349.37 |
| generator.from_frequency_table             |       100 |                 0.13 |                1314.26 |
| generator.from_frequency_table             |       500 |                 0.15 |                 296.2  |
| generator.from_frequency_table             |      1000 |                 0.17 |                 172.05 |
| generator.from_normal_distribution         |       100 |                 0.17 |                1743.81 |
| generator.from_normal_distribution         |       500 |                 0.66 |                1324.82 |
| generator.from_normal_distribution         |      1000 |                 1.26 |                1255.27 |
| generator.from_uniform_distribution        |       100 |                 0.16 |                1637.2  |
| generator.from_uniform_distribution        |       500 |                 0.55 |                1103.5  |
| generator.from_uniform_distribution        |      1000 |                 1.04 |                1038.35 |
| generator.to_dataframe                     |       100 |                 1.23 |               12315.7  |
| generator.to_dataframe                     |       500 |                 2.61 |                5220.73 |
| generator.to_dataframe                     |      1000 |                 4.32 |                4315.01 |
| corruptor.with_edit                        |       100 |                39.32 |              393224    |
| corruptor.with_edit                        |       500 |                45.41 |               90819.5  |
| corruptor.with_edit                        |      1000 |                47.5  |               47499.5  |
| corruptor.with_missing_value               |       100 |                 0.06 |                 557.71 |
| corruptor.with_missing_value               |       500 |                 0.08 |                 151.77 |
| corruptor.with_missing_value               |      1000 |                 0.1  |                  99.43 |
| corruptor.with_replacement_table           |       100 |                50.36 |              503625    |
| corruptor.with_replacement_table           |       500 |                59.88 |              119756    |
| corruptor.with_replacement_table           |      1000 |                70.16 |               70160.1  |
| corruptor.with_cldr_keymap_file            |       100 |                26.42 |              264247    |
| corruptor.with_cldr_keymap_file            |       500 |                28.67 |               57338.3  |
| corruptor.with_cldr_keymap_file            |      1000 |                30.95 |               30954.9  |
| corruptor.with_permute                     |       100 |                 0.04 |                 370.24 |
| corruptor.with_permute                     |       500 |                 0.04 |                  88.66 |
| corruptor.with_permute                     |      1000 |                 0.05 |                  51.8  |
| corruptor.with_categorical_values          |       100 |                 2.73 |               27336.8  |
| corruptor.with_categorical_values          |       500 |                 3.51 |                7016.82 |
| corruptor.with_categorical_values          |      1000 |                 4.38 |                4381.57 |