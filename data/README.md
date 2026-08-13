# Data

The original dataset is not redistributed because it was supplied through a restricted University of Melbourne course environment and its public reuse rights have not been established.

To reproduce the analysis with an authorised copy, create a `raw` directory and place the file at:

```text
data/raw/factor_and_ret_oos.csv
```

The notebook expects:

- `id`: firm identifier
- `date`: observation date
- `ret_future`: forward return target
- financial characteristic columns, including `at_be`, `ret_6_0` and `beta_60m`

The repository's `.gitignore` prevents files inside `data/raw/` from being committed. Do not upload the restricted source file to a public repository.

