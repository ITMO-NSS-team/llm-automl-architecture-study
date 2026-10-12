## Specialized library to use — REQUIRED, STRICT
The final model you submit MUST be **LightAutoML** (pre-installed). Start from this
skeleton and adapt only the marked parts:
```python
from lightautoml.automl.presets.tabular_presets import TabularAutoML
from lightautoml.tasks import Task

task = Task('reg')            # 'reg' | 'binary' | 'multiclass' — per the instruction
roles = {'target': TARGET_COLUMN}
automl = TabularAutoML(task=task, timeout=TIME_BUDGET_SECONDS)
oof = automl.fit_predict(train_df, roles=roles)      # train_df includes the target
pred = automl.predict(test_df).data.reshape(-1)
print('MODEL_USED=', type(automl).__name__)          # must print TabularAutoML
```
You MUST print the `MODEL_USED=` line, and it MUST say `TabularAutoML`.
You MUST NOT submit predictions from `RandomForestRegressor`, `GradientBoosting*`,
`Ridge`, `LinearRegression` or any other scikit-learn estimator as the final model —
they are allowed only as a quick sanity reference you print alongside.
If an import or an API call fails, read the error and fix it (check the installed
package, e.g. `help(TabularAutoML)`); do NOT abandon LightAutoML.
For multi-target problems, fit one TabularAutoML per target.
You MAY additionally use the pre-installed **featuretools** / **feature-engine**.
