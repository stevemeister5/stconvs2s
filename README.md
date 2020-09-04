# Weather Forecasting using Deep convolutional models.

![STConvS2S architecture](/image/stconvs2s.png)

## Requirements

To install packages with the same version as we executed our experiments, run the code below:

```
cd config
./create-env.sh
```

## Datasets

All datasets are publicly available at http://doi.org/10.5281/zenodo.3558773. Datasets must be placed in the [data](https://github.com/MLRG-CEFET-RJ/stconvs2s/tree/master/data) folder.


## Experiments

Jupyter notebooks for the first sequence-to-sequence task (given the previous 5 grids, predict the next 5 grids) can be found in the [experiments] folder (see Table 1 in the paper).


Final experiments (see Table 2 in the paper) compare STConvS2S (our architecture) with ConvLSTM architecture and a baseline (ARIMA models). We evaluate the models in two horizons: 5 and 15-steps ahead. This task is performed using [main.py] (for deep learning models) and [baseline.py] (for ARIMA models). Results can be found in the [output] folder.


* `/output/full-dataset` (for deep learning models)
	* `/checkpoints`: pre-trained models that allow you to recreate the training configuration (weights, loss, optimizer).
	* `/losses`: training and validation losses. Can be used to recreate the error analysis plot
	* `/plots`:	error analysis plots from training phase
	* `/results`: evaluation phase results with metric value (RMSE or MAE), training time, best epochs and so on.

* `/output/baseline`: results of baseline models
	

## Usage

First load the conda environment with the installed packages.

```
source activate pytorch
```

Below are examples of how to run each model.

### STConvS2S
```
python main.py -i 10 -v 4 --plot > output/full-dataset/results/chirps-stconvs2s-rmse-v4.out
```

The above command executes STConvS2S in 10 iterations (`-i`), indicating the model version (`-v`), allowing the generation of plots in the training phase (`--plot`).

### ConvLSTM

To run experiments with ConvLSTM architecture, add the `--convlstm` parameter to the above command.


### Baseline

```
python baseline.py > output/baseline/cfsr-arima.out
```

### Additional parameters
* add `--mae`: change the metric to MAE. Default metric: RMSE.
* add `-s 15`: change the horizon. Default horizon: 5.
