# Digestible Intro to Cory Shain's CDRNN
## Excerpt from Shain's CDR Github Page
"In many real world time series, events trigger "ripples" in a dependent variable that unfold slowly and overlap in time (temporal diffusion). Recovering the underlying dynamics of temporally diffuse effects is challenging when events and/or responses occur at irregular intervals. Continuous-time deconvolutional regression (CDR) is a regression technique for time series that directly models temporal diffusion of effects (Shain & Schuler, 2018, 2021) as a function of continuous time. CDR uses machine learning to estimate continuous-time impulse response functions (IRFs) that mediate between predictors (event properties) and responses. Given data and a model template specifying the functional form(s) of the IRF kernel(s), CDR finds IRF parameters that optimize some objective function. CDR is a form of distributional regression: it can model continuous-time influences of predictors on all parameters of arbitrary predictive distributions, not just on the mean of a normal predictive distribution. This approach can be generalized to account for non-stationarity, non-linearity, non-additivity, and context-dependence by incorporating deep neural network components (Shain, 2021)."

TL;DR:
In cases where previous events (ERPs, prior words read, etc) may have an impact on the results of future events, it is useful to have a model that accounts for these spill-over effects when trying to isolate the effects of specific predictors. CDR is a module that uses neural networks to tune models that account for spill-over effects.

## Installation instructions(Windows)

Before you begin, make sure that you have [Anaconda](https://www.anaconda.com/) installed on your system.

Then, download the CDR repository from here by clicking the green <>Code button on the top left and clicking "Download Zip."

Unzip the Zip file once downloaded. The unzipped folder "cdr-master" will be your root directory.

Once Anaconda is installed, hit the Windows key and run "Anaconda Prompt". A terminal window should appear.

In the terminal, type `cd <path_to_cdr_root>`, where <path_to_cdr_root> is replaced with the file path to the unzipped "cdr-master" folder. The path should look something like:
`C:\Users\name\sub-folder\sub-folder\cdr-master`

Then enter the following sequence of code, pressing Enter after each line.
```
conda env create -f conda_cdr.yml
conda activate cdr
python setup.py install
```
This will install a virtual environment on your computer called "cdr" and install the CDR toolkit in that environment.

Whenever you want to access the environment and use the CDR toolkit, just enter:
```
conda activate cdr
```
Once the toolkit is installed and the environment created, you will only need to run this one line of code from Anaconda Prompt to enter the environment.

## Using CDR (Reading-time data)
Once you've entered the cdr environment, your terminal should look something like this, with (cdr) on the left side of your root directory information.
![Make sure (cdr) is present on the left](https://i.imgur.com/mLbV92p.png)
The CDR toolkit uses  a .ini file to get the model configuration. This Github repo has a sample configuration file "example_config.ini" for reading-time data, but if you'd like to generate a fresh config.ini template, you can by typing the following code into the terminal:
```
python -m cdr.bin.create_config > <path_to_config.ini>
```
Where <path_to_config.ini> is the path to the folder that you'd like the template .ini file to be created in. This path should look something like this

    C:\Users\name\sub-folder\sub-folder\name_of_config.ini

Once you have your default .ini, configure the arguments according to the INTRO_TO_INI.md file in this repo.  You only need to modify the arguments in the [data], [global_settings], [irf_name_map], and [model_] categories; arguments in [cdr_settings] are fine for Reading time data models.

After your .ini file is updated according to your specifications, you can run the model by typing this line of code into the terminal.

    python -m cdr.bin.train <path_to_config.ini>

You should see the model begin training. After it is done running, plot the model performance with.

    python -m cdr.bin.plot <path_to_config.ini> -m <model_name>

If you check the directory you specified in [global_settings], you should now see a folder with the plots for your model.
