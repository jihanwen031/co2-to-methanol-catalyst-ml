# Machine learning for CO₂ hydrogenation to methanol

This workflow starts with `SI-dataset.xlsx` and reproduces the analyses for oxide-supported Cu catalysts. Start the notebooks from this folder so their relative paths resolve correctly.

## Environment

```sh
conda env create -f environment.yml
conda activate methanol-catalyst-ml
jupyter lab
```

The `qiao` environment can also be used if it has the listed packages. The equilibrium notebooks use the supplied AramcoMech 3.0 Cantera file under `thermo/`.

## Run order

| Step | File | Purpose and paper outputs |
| --- | --- | --- |
| 01 | [Generate input](01_generate_input.ipynb) | Extract the source features and record identifiers to `derived/intermediate/dataset.xlsx`. |
| 02 | [Prepare data](02_prepare_data.ipynb) | Screen records and retain calcination-missingness flags in `derived/intermediate/prepared_dataset.xlsx`. |
| 03 | [Distribution and encoding](03_distribution_and_encoding.ipynb) | Generate Fig. 2a–f and display Table S2. Write the modeling input to `derived/dataset.xlsx`. |
| 04 | [Model comparison](04_compare_models.ipynb) | Compare eight STY models with training-fold imputation. Generate Figs. 3, 4, and S1a–b. |
| 05 | [STY XGBoost model](05_fit_sty_model.ipynb) | Tune and fit the STY model. Generate Figs. 5, 6a–j, and S2–S4, and save the tuned parameters for Table S3. |
| 06 | [Conversion and selectivity](06_conversion_selectivity.ipynb) | Generate Figs. S6, S8, and S9a–h. Save the conversion–selectivity rows for Table S4. |
| 07 | [CO-only equilibrium reference](07_equilibrium_co_only.ipynb) | Recalculate the CO-only equilibrium conversion. |
| 08 | [Equilibrium by-product sensitivity](08_equilibrium_byproducts.ipynb) | Compare the admitted species sets and the resulting conversions, ATE values, and clusters. |
| 09 | [ATE and selectivity](09_ate_selectivity.ipynb) | Generate Figs. 7, 8a–h, and S7. Save the ATE–selectivity rows for Table S4. |
| 10 | [ZnO and Cu surface area](10_zno_cu_surface_area.ipynb) | Generate Fig. S5a–b using source-reported N₂O measurements. |
| 11 | [Synthesis encoding sensitivity](11_synthesis_encoding_sensitivity.ipynb) | Compare integer and one-hot representations. |
| 12 | [Calcination imputation sensitivity](12_calcination_imputation_sensitivity.ipynb) | Print Table S1 after step 05 has saved the STY results. |

Steps 01 and 02 protect their outputs from accidental overwrites. For a clean rerun, move the old `derived/` directory aside. Steps 07 and 08 save independent equilibrium checks. Step 09 uses the equilibrium-conversion column already in the curated data.

Run all cells in step 12 from this folder after step 05 has saved the STY results.

Fig. 1, Table 1, and Table S5 are prepared in the manuscript and supplementary documents.
