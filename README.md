## Findings & Recommendations

This is based on the work at [this notebook](prompt_II.ipynb).

69% of price variation is captured by a small set of
easy-to-observe attributes. The recommended Ridge model prices a listing within
about **\$7.8k RMSE** and a **median absolute residual error of ~\$3.9k** — good enough
to price and buy inventory competitively.

### The levers that matter most

These are directional Ridge coefficient readouts. The strongest positive and negative category effects come from the coefficient plot above.

**Push price up**

1. **Newer cars**: every extra year of age costs about **\$912**.
2. **Low mileage**: every extra **10,000 miles** costs about **\$716**.
3. **Diesel fuel** has one of the strongest positive fuel coefficients.
4. **Selected premium brands**, especially Tesla, Porsche, Rover, and Lexus, have large positive coefficients.
5. **Offroad body type and high/rare cylinder groups** also appear among the largest positive coefficients.

**Push price down**

* **Number of cylinders**: 3-cylinder and 4-cylinder categories have large negative coefficients.
* **Bus body type** has a large negative coefficient in this retail-price model.
* ** Some manufacturers **, such as Fiat, Mitsubishi, Kia, Hyundai, Nissan, and Volkswagen, appear among the largest negative coefficients.
* ** Electric fuel ** has a negative coefficient in this dataset/model. This might need more investigation.

### Actions for the dealership

*   **Target** newer, lower-mileage vehicles specifically from high-value segments such as diesel, premium-brand (Tesla, Porsche), and offroad listings.
*   **Scrutinize** trade-ins from negative-coefficient groups, particularly small-cylinder vehicles and manufacturers like Fiat or Mitsubishi, as they depreciate faster.
*   **Implement** the model as a automated pricing check; **flag** any listing where the intended price differs by more than $3,000 from the model's prediction for manager review.
*   **Avoid** relying on arbitrary 'gut feel' thresholds (like 200k miles); use the linear depreciation trends provided by the model for more accurate appraisals.

### Limitations and next steps

* **~31% variance ceiling**: real used-car pricing is also driven by cosmetics, mechanical condition, and local demand that this dataset does not include.
* **Heavy-tailed target**: a log-price OLS should tighten residuals at the high end.
* **`model` was dropped** (29k unique values). A target-encoded or grouped version of `model` would be high-value next feature.
* **Further exploration**: 4wd premiums, condition-tier deltas, salvage-title penalties would need more data to back up such claims. We could generate coefficient tables, grouped summaries, or implement nonlinear features.