# imperial-ml-capstone
This is part of the capstone project for the Professional Certificate in Machine Learning and AI from Imperial College Business School.

The project has been set up in a way that real-world conditions are simulated. Results can only be submitted once a week, and the results are back in a few days. This means that any brute force strategy is out of the quesiton and they we are given enough time to reflect on an approach for the following week.

## Black-box optimization goal
The goal of this project is the optimization of 8 black-box functions. For each of the functions 10 initial data points are given and each week I must submit a new data point to evaluate. This simulates a costly process of actual evaluation.

All variables range from 0 to 1 and vary from 2-dimensional to 8-dimensional.

In a **black-box optimization** problem, you have a function  

``f(x): R^d → R``

that you can **evaluate** (possibly at high cost), but:

- You don’t know its analytic form  
- You can’t compute gradients  
- Each evaluation is expensive or noisy  

The goal is to find the input `x*` that minimizes (or maximizes) the function:

``x* = argmin_x f(x)``

In other words, the goal is to to optimize `f(x)` **without access to derivatives or internal structure** — we can only treat it as a black box that takes an input and returns an output. The number of trials is limited and they are separated in time with only weekly sampling windows.


## Tools and libraries used
In terms of libraries, the backbone of my project is built around **scikit-learn** (and therefore **NumPy**) for scaling, Gaussian Process models, Support Vector Machines and evaluation metrics. These libraries form the numerical core of the workflow: **NumPy**provides efficient vectorised operations for manipulating arrays and evaluating candidate points, while scikit-learn offers a stable API for experimenting with different kernels, surrogate models and preprocessing steps. The trade-off is that scikit-learn’s Gaussian Process implementation can become slow or unstable in higher dimensions, and NumPy requires careful handling of array shapes and broadcasting rules.

I also use **SciPy**, specifically its optimization, distance and statistics modules. These tools allow me to run local optimizations, compute distances between candidate points and evaluate statistical properties of the sampled results. SciPy fits the workflow because it bridges the gap between numerical methods and machine learning models, though it can require more low-level parameter tuning and may not scale well to very large datasets.

To complement the scikit-learn models, I experimented with **TensorFlow** through its **Keras** interface to build a simple neural network. This allowed me to benchmark how a deep-learning–based surrogate behaves compared to Gaussian Processes. **Keras** is easy to prototype with, but neural networks introduce higher computational cost, require more careful hyperparameter tuning and tend to be less interpretable—important trade-offs compared to classical surrogate models.

All results are stored in a Pandas DataFrame (results_df), which provides an organised, human-readable structure for comparing weekly outcomes across functions. This makes it easier to review progress, validate assumptions and identify potential mistakes. The trade-off is that Pandas can become memory-heavy for large intermediate datasets, and maintaining consistent data types across weeks requires discipline.

Finally, I have documented the entire workflow chronologically in a Jupyter Notebook. This format allows me to interleave code, reasoning and intermediate observations, making the exploration process transparent. The downside is that notebooks can become difficult to reproduce unless cells are executed in a controlled order.

Overall, these libraries were the right choices for this project because they are industry-standard tools, widely used in both machine learning research and applied workflows. Using them strengthens my understanding of common ML tooling and ensures that the methods I develop are compatible with existing codebases. 

## Files and reproducibility

### Inputs
The input files first received at the beginning of the challenge are inside the "initial_data" folder, with one folder per function.

### Outputs
For each weekly submission, the platform has generated one "inputs.txt" and one "outputs.txt" file. Both contain the full history of submitted queries and the results. I have stored all of these inside the "submissions" folder

### Reproducing the work
The Jupyter notebook can be reexecuted with all the files from "submissions" and "initial_data" downloaded. It is important that the cells are executed in order because data is added to the arrays gradually from the Pandas "results_df" dataframe to simulate partial knowledge.

## Functions overview
More details of each function including boundaries and plots when appropiate can be found in the notebook.

### Function 1
This function is a function with a 1D output and a 2D input. 

This is the description of the function: Detect likely contamination sources in a two-dimensional area, such as a radiation field, where only proximity yields a non-zero reading. The system uses Bayesian optimisation to tune detection parameters and reliably identify both strong and weak sources.

### Function 2
This function is a function with a 1D output and a 2D input. 

This is the description of the function: Imagine a black box, or a mystery ML model, that takes two numbers as input and returns a log-likelihood score. Your goal is to maximise that score, but each output is noisy, and depending on where you start, you might get stuck in a local optimum. 

To tackle this, you use Bayesian optimisation, which selects the next inputs based on what it has learned so far. It balances exploration with exploitation, making it well suited to noisy outputs and complex functions with many local peaks.

### Function 3
This function is a function with a 1D output and a 3D input. 

This is the description of the function: you’re working on a drug discovery project, testing combinations of three compounds to create a new medicine.

Each experiment is stored in initial_inputs.npy as a 3D array, where each row lists the amounts of the three compounds used. After each experiment, you record the number of adverse reactions, stored in initial_outputs.npy as a 1D array.

Your goal is to minimise side effects; in this competition, it is framed as maximisation by optimising a transformed output (e.g. the negative of side effects). 

### Function 4

This function is a function with a 1D output and a 4D input. 

This is the description of the function: Address the challenge of optimally placing products across warehouses for a business with high online sales, where accurate calculations are costly and only feasible biweekly. To speed up decision-making, an ML model approximates these results within hours. The model has four hyperparameters to tune, and its output reflects the difference from the expensive baseline. Because the system is dynamic and full of local optima, it requires careful tuning and robust validation to find reliable, near-optimal solutions. 

Your goal is to find the optimal combination of chemical inputs that delivers the highest possible yield, using systematic exploration and optimisation methods.

### Function 5
This function is a function with a 1D output and a 4D input. 

This is the description of the function: You’re tasked with optimising a four-variable black-box function that represents the yield of a chemical process in a factory. The function is typically unimodal, with a single peak where yield is maximised. 

Your goal is to find the optimal combination of chemical inputs that delivers the highest possible yield, using systematic exploration and optimisation methods.
### Function 6
This function is a function with a 1D output and a 5D input. 

This is the description of the function: You’re optimising a cake recipe using a black-box function with five ingredient inputs, for example flour, sugar, eggs, butter and milk. Each recipe is evaluated with a combined score based on flavour, consistency, calories, waste and cost, where each factor contributes negative points as judged by an expert taster. This means the total score is negative by design. 

To frame this as a maximisation problem, your goal is to bring that score as close to zero as possible or, equivalently, to maximise the negative of the total sum.

### Function 7
This function is a function with a 1D output and a 6D input. 

This is the description of the function: You’re tasked with optimising an ML model by tuning six hyperparameters, for example learning rate, regularisation strength or number of hidden layers. The function you’re maximising is the model’s performance score (such as accuracy or F1), but since the relationship between inputs and output isn’t known, it’s treated as a black-box function. 

Because this is a commonly used model, you might benefit from researching best practices or literature to guide your initial search space. Your goal is to find the combination of hyperparameters that yields the highest possible performance.

### Function 8
This function is a function with a 1D output and a 8D input. 

This is the description of the function: You’re optimising an eight-dimensional black-box function, where each of the eight input parameters affects the output, but the internal mechanics are unknown. 

Your objective is to find the parameter combination that maximises the function’s output, such as performance, efficiency or validation accuracy. Because the function is high-dimensional and likely complex, global optimisation is hard, so identifying strong local maxima is often a practical strategy.

For example, imagine you’re tuning an ML model with eight hyperparameters: learning rate, batch size, number of layers, dropout rate, regularisation strength, activation function (numerically encoded), optimiser type (encoded) and initial weight range. Each input set returns a single validation accuracy score between 0 and 1. Your goal is to maximise this score.

