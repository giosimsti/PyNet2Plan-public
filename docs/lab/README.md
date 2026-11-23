# Lab handouts

| handout | file | content |
|---|---|---|
| 0 | [`00_installation.pdf`](00_installation.pdf) | installation of Python 3.14, of the lab code and of the required packages on macOS and Windows |
| 1 | [`01_tool_overview.pdf`](01_tool_overview.pdf) | description of the graphical interface, one annotated screenshot per page |
| 2 | [`02_networkx_backend.pdf`](02_networkx_backend.pdf) | representation of networks as NetworkX graphs, with the script `labs/lab1_networkx_tour.py` |
| 3 | [`03_first_ilp.pdf`](03_first_ilp.pdf) | the splittable flow formulation on Spain-7: effect of the capacity, fibre cuts |
| 4 | [`04_unsplittable_flow.pdf`](04_unsplittable_flow.pdf) | Lab 2: completing the unsplittable flow formulation and comparing it with the splittable one (`labs/lab2_unsplittable.py`) |
| 5 | [`05_route_formulation.pdf`](05_route_formulation.pdf) | Lab 2: completing the route formulation and comparing it with the flow formulation (`labs/lab2_route_formulation.py`) |
| 6 | [`06_protection_route_formulation.pdf`](06_protection_route_formulation.pdf) | Lab 3: the route formulation with 1+1 protection, one page (exercise `formulations/protection_route_formulation.py`) |

The folder `screenshots/` contains the screenshots of the handouts with the numbered labels,
and `screenshots/raw/` the same screenshots without them; those of handout 4 are in
`screenshots/lab2/`. The folder `figures/` contains the
figures of the handouts, drawn with TikZ from the data of the scripts in `labs/`
(`tools/lab_docs/tikz_figures.py`); their LaTeX sources and PDF versions, which can be reused
in slides, are in `figures/tikz/`.

## Building the handouts

The handouts 0 to 5 are built from the Markdown files in `src/`, with the screenshots and the
figures, by

```bash
pip install markdown pymdown-extensions playwright pillow
python -m playwright install chromium          # and a TeX installation with PGFPlots (pdflatex)
python tools/lab_docs/build.py all --project ../copy --python ../copy/.venv/bin/python
```

where `../copy` is a clone of this repository with its own environment `.venv` (handout 0), in
which the screenshots are taken. The console outputs and the figures of handouts 4 and 5 show
the completed exercises: the build completes `formulations/unsplittable_flow.py` and
`formulations/route_formulation_vwp.py` with the code of the reference solutions in a
`solutions/` folder, which is not part of this repository, so these two handouts can only be
rebuilt after you add your own solutions there. On Linux without a display the screenshots
are taken inside `xvfb-run`. The address of the repository quoted in handout 0 is set with
`--var repo_url=https://github.com/<owner>/<repo>`.

The values quoted in the handouts are checked by `tests/test_labs.py`. Console outputs and
figures are inserted from the scripts by the directives `{{output ...}}` and `{{figure ...}}`
of the sources, described in `tools/lab_docs/build.py`.
