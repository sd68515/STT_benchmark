# STT benchmark source fork

This fork supports [VelocityBenchmarking](https://github.com/vikkihuangkexin/VelocityBenchmarking) and is based on the `release` branch of [cliffzhou92/STT](https://github.com/cliffzhou92/STT) at commit `1a1e61e4848002bf127670a198844cb11fd067a5`. Please cite the original STT work when using the method.

## Compatibility changes

| File and location | Change | Reason |
| --- | --- | --- |
| `example_notebooks/stt/tl/_dynamical_analysis.py`, imports | Supports the CellRank 1 and CellRank 2 locations of `GPCCA`, `ConnectivityKernel`, and `VelocityKernel`. | Keeps the analysis importable across both CellRank APIs. |
| `example_notebooks/stt/tl/_dynamical_analysis.py`, `dynamical_analysis` gene selection | Raises a clear error when the `r2_test` threshold selects no genes. | Stops before constructing an empty velocity kernel. |
| `example_notebooks/stt/tl/_dynamical_analysis.py`, `dynamical_analysis` transition kernel | Passes `xkey='spliced'` and uses the API's `scheme` or `similarity` argument for the same `dot_product` rule. | Makes the expression layer explicit and adapts to the CellRank 2 argument name. |
| `example_notebooks/stt/tl/_dynamical_analysis.py`, `dynamical_analysis` and `dynamical_iteration` | Adds and forwards an `n_jobs` argument (default `-1`). | Lets callers limit transition-kernel workers. |

STT's tensor estimation and iteration formulas are unchanged. The explicit expression key and CellRank API adaptation can affect transition results.

## Environment

Reference versions: Python 3.9.22 and CellRank 2.0.7. The retained upstream `requirements.txt` is not a lock for this dependency combination.

## Use

The importable package remains at `example_notebooks/stt/`. From the repository root:

```bash
export PYTHONPATH="$PWD/example_notebooks${PYTHONPATH:+:$PYTHONPATH}"
python -c "import stt; print(stt.__file__)"
```

The separate benchmark runner supplies preprocessing, parameters, input data, and result checks. Data, notebooks, and results are not included.

## License

The upstream MIT `LICENSE` is retained unchanged.
