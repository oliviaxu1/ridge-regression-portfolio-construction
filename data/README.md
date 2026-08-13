# Data

The dataset was provided through the University of Melbourne course environment. The raw data are not included in this repository.

To reproduce the analysis with an authorised copy, create a `raw` directory and place the file at:

```text
data/raw/factor_and_ret_oos.csv
```

The notebook expects:

- `id`: firm identifier
- `date`: observation date
- `ret_future`: actual future return
- Financial characteristic columns, including:
  - `at_be`: book leverage
  - `ret_6_0`: momentum (0-6 months)
  - `beta_60m`: market beta
  

The repository's `.gitignore` prevents files inside `data/raw/` from being committed. Do not upload the restricted source file to a public repository.

