# Signal rectifier

## The Gaussian with Jumps

### The idea behind the problem
You can imagine the noisy data being the data acquired from a motion capture system and the jump a pause between two actions in this recording. The idea is to replay that recorded data on a robot (hence the filtering for smooth movements), while avoiding jumping between the 2 different part of the action.

### The problem
Some data is provided in the `data` folder (which has been generated using the `utils/generator.py` if you're interested). Each line of the file contains x and y, the y data is noisy. 3 main features of signal_rectifier.py:
 - filter the data so that it is not as noisy
 - detect when the jumps occur (some of the jumps are harder to detect than others, try to detect as many of them as you can). 
 - smoothly join the different parts in order to get rid of those discontinuities. A reasonable part of the end of the trajectory N and the beginning of trajectory N+1 is merged to make them as smoothly as possible. The idea is to bend the data around end of N and beginning of N+1 to have a smooth joining.

## Python
Given code was successfully run on Python 3.9.7.

## Running
To run the signal rectifier program, provide `--path path/to/file` to extract data, which was generated by `generator.py`. By default program will plot 2 graphs: original dataset and modified dataset.

Example:

```bash
python signal_rectifier.py --path data/sample.txt
```

If you'd like to plot graphs separately, set argument `--plot_original` or `--plot_clean`.
You can also output the dataset to the terminal by providing `--print_original` and/or `--print_clean`
There are 2 algorithms available for smoothing the jump areas. By default, more advanced is used. Provide `--simple` to run through simpler algorithm of smoothing.

## Testing

Once samples of datasets are generated, `jumps_test.py` can be run to test if the jump positions are identified correctly. This is vital procedure, before running `signal_rectifier.py`, because if one or more Tests do not PASS, the algorithms for smoothing wouldn't work correctly.

Usage:
```bash
python jumps_test.py data
```
