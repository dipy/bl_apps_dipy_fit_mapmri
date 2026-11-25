<h1 align="center">Fit MAPMRI</h1>

<p align="center">
  Fits the MAPMRI diffusion model to DWI with DIPY 1.1.1 dipy_fit_mapmri (Laplacian and/or positivity regularisation) and outputs RTOP, RTAP, RTPP, MSD, QIV, Laplacian norm and non-Gaussianity maps.
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/bl.app.67"><img src="https://img.shields.io/badge/Brainlife-bl.app.67-blue.svg" alt="Run on brainlife.io"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-see_LICENSE-lightgrey.svg" alt="License"></a>
</p>

## At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Fits the MAPMRI diffusion model to DWI with DIPY 1.1.1 dipy_fit_mapmri (Laplacian and/or positivity regularisation) and outputs RTOP, RTAP, RTPP, MSD, QIV, Laplacian norm and non-Gaussianity maps.**

Wraps the DIPY dipy_fit_mapmri workflow (Mean Apparent Propagator MRI) on a DWI with its bvals and bvecs, inside the brainlife/dipy:1.1.1 container. Use it to compute propagator-based microstructure scalars from multi-shell DWI. At least one of laplacian or positivity must be enabled; small_delta and big_delta (diffusion timing) are passed to the workflow to build the gradient table.

| | |
|---|---|
| **Inputs** | `neuro/dwi` |
| **Outputs** | `raw` |
| **Container** | `brainlife/dipy:1.1.1` |
| **Resources** | 6 CPUs |
| **Run it** | [doi.org/10.25663/bl.app.67](https://doi.org/10.25663/bl.app.67) |

#### Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `input` | `neuro/dwi` | yes | Path to the input volume/bvals/bvecs. |

#### Outputs

| Output | Datatype | Description |
|---|---|---|
| `output` | `raw` | Output folder of dipy_fit_mapmri with the scalar maps (rtop, lapnorm, msd, qiv, rtap, rtpp, ng, parallel ng, perpendicular ng). |

<details>
<summary><b>Parameters</b> (9)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `command` | string | `dipy_fit_mapmri` | DIPY workflow to run; only dipy_fit_mapmri is accepted. |
| `small_delta` | number |  | Small delta value used in generation of gradient table of provided bval and bvec. |
| `big_delta` | number |  | Big delta value used in generation of gradient table of provided bval and bvec. |
| `b0_threshold` | number | `50` | Threshold used to find b=0 directions (default 0.0) |
| `bval_threshold` | number | `2000` | Sets the b-value threshold to be used in the scale factor estimation. In order for the estimated non-Gaussianity to have meaning this value should set to a lower value (b<2000 s/mm^2) such that the scale factors are estimated on signal points that reasonably represent the spins at Gaussian diffusion |
| `laplacian_weighting` | number | `0.05` | Weighting value used in fitting the MAPMRI model in the laplacian and both model types. (default: 0.05) |
| `radial_order` | number | `6` | Even value used to set the order of the basis (default: 6) |
| `laplacian` | boolean | `true` | Regularize using the Laplacian of the MAP-MRI basis (default True) |
| `positivity` | boolean | `true` | Constrain the propagator to be positive. (default True) |

</details>

<!-- brainlife-app:end -->

## Running the App

### On brainlife.io

Open the App at [doi.org/10.25663/bl.app.67](https://doi.org/10.25663/bl.app.67), choose `neuro/dwi` from your project, set the parameters and press **Execute**. The results are saved to your project as `raw`.

### Locally

You need [Singularity/Apptainer](https://apptainer.org/) (the App runs in `brainlife/dipy:1.1.1`), [`jq`](https://jqlang.github.io/jq/).

1. Clone this repository.
2. Create `config.json` with the paths to your inputs and the parameters:

   ```json
   {
       "dwi": "/path/to/input/dwi",
       "bvals": "/path/to/input/bvals",
       "bvecs": "/path/to/input/bvecs",
       "command": "dipy_fit_mapmri",
       "small_delta": "<number>",
       "big_delta": "<number>",
       "b0_threshold": 50,
       "bval_threshold": 2000,
       "laplacian_weighting": 0.05,
       "radial_order": 6,
       "laplacian": true,
       "positivity": true
   }
   ```

3. Run `./main`.

## Troubleshooting

- **invalid command**: Set command to dipy_fit_mapmri.

## DIPY

- This is a Brainlife wrapper App stemming from the [`dipy_fit_mapmri`](https://dipy.org/documentation/latest/reference_cmd/dipy_fit_mapmri/) workflow.
- This single wrapper is exposed through an apps registered on [Brainlife.io](https://brainlife.io).
- More information about DIPY : [https://dipy.org/](https://dipy.org/).
- More information about the command line `dipy_fit_mapmri`: [Command line Reference](https://dipy.org/documentation/latest/reference_cmd/dipy_fit_mapmri/).

## Citing

If you use this App, please cite it, the software it builds on and brainlife.io:

- Fit MAPMRI. brainlife.io App. [doi:10.25663/bl.app.67](https://doi.org/10.25663/bl.app.67)
- Garyfallidis E. et al. Dipy, a library for the analysis of diffusion MRI data. Frontiers in Neuroinformatics 8, 8 (2014).
- Garyfallidis, E., Brett, M., Amirbekian, B., Rokem, A., van der Walt, S., Descoteaux, M., Nimmo-Smith, I., & Dipy Contributors (2014). Dipy, a library for the analysis of diffusion MRI data. Frontiers in neuroinformatics, 8, 8. [https://doi.org/10.3389/fninf.2014.00008](https://doi.org/10.3389/fninf.2014.00008)
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## Authors

- Serge Koudoro
- Javier Ricardo Guaje Guerra

**Contributors**

- Soichi Hayashi

## Funding

[![Wellcome-226486/Z/22/Z](https://img.shields.io/badge/Wellcome-226486%2FZ%2F22%2FZ-purple.svg)](https://wellcome.org/)
[![NIH-NINDS-U24NS140384](https://img.shields.io/badge/NIH_NINDS-U24NS140384-green.svg)](https://reporter.nih.gov/project-details/11261037)
[![NIH-NINDS-UM1NS132207](https://img.shields.io/badge/NIH_NINDS-UM1NS132207-green.svg)](https://reporter.nih.gov/project-details/11411328)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://reporter.nih.gov/project-details/10262925)
[![NIH-NIBIB-R01EB030896](https://img.shields.io/badge/NIH_NIBIB-R01EB030896-green.svg)](https://reporter.nih.gov/project-details/10428625)
[![NIH-NIMH-R01MH126699](https://img.shields.io/badge/NIH_NIMH-R01MH126699-green.svg)](https://reporter.nih.gov/project-details/10460628)
[![NIH-NIDCD-R01DC020088](https://img.shields.io/badge/NIH_NIDCD-R01DC020088-green.svg)](https://reporter.nih.gov/project-details/11140284)
[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-2203524](https://img.shields.io/badge/NSF_BCS-2203524-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2203524)
[![NSF-IIS-1636893](https://img.shields.io/badge/NSF_IIS-1636893-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-OAC-2148729](https://img.shields.io/badge/NSF_OAC-2148729-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148729)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NSF-IIS-2148700](https://img.shields.io/badge/NSF_IIS-2148700-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148700)
[![NSF-OAC-1916518](https://img.shields.io/badge/NSF_OAC-1916518-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1916518)

<sub>brainlife.io, which runs this App, is publicly funded by Wellcome, the U.S. National Institutes of Health and the U.S. National Science Foundation; acknowledging that support helps keep it running.</sub>

## License

See [LICENSE](LICENSE).
