# Project model card

### Overview

This is the model card for the Machine Learning and AI certiciate of Imperial College capstone project, a black-box optimization challenge.

### Intended use

The model or models used in this project are to be used for the selection of the next query point of an unknown underlying functions with an arbitrary number of inputs and one single output.

### Details

The project contains several models as it is intended to be an experimentation sheet.

The main model used is a TuRBO (trust region Bayesian optimization) algorithm where the unknown function is approximated by a surrogate Gaussian process. Different kernels can be used to approximate the function. Once computed, and based on that approximation, a _next query point_ is selected. 

For this an acquisition function ought to be chosen. Also for this different ones can be selected, with EI (expected improvement) being the most common one. 

Finally, if the _next query point_ does not yield a better result, then it is considered that the trust region around the known best query point is to be reduced and only a point inside that trust region can be queried. Please note that even though the model present in this project admits modifications to the trust region mechanism by setting different parameters, only the algorithm of reducing inmediately after a worse point is applied.

### Performance

Based on the results available in week 10, this is a performance table for the 8 functions on which this is applied:

| Function | Baseline Best | Improved Value | % Improvement | Samples Improved |
|----------|---------------|----------------|---------------|------------------|
| 1 | 7.710875114502849e-16 | 2.6752879910742468e-09 | +347,031,616.55% | 1 |
| 2 | 0.6112052157614438 | 0.6669887774564723 | +9.13% | 1 |
| 3 | -0.034835313350078584 | -0.0014942495830570148 | +95.71% | 1 |
| 4 | -4.025542281908162 | 0.640155190044084 | +115.90% | 3 |
| 5 | 1088.8596181962705 | 8662.4825 | +695.40% | 3 |
| 6 | -0.714264947820240 | -0.168848797153551 | +76.36% | 3 |
| 7 | 1.364968304499199 | 2.299734497234645 | +68.48% | 5 |
| 8 | 9.598482002566342 | 9.981242508794001 | +3.99% | 5 |

As the querying process depends on the capstone project portal, I have not applied this to any other arbitrary functions although the model should e generalizable. 

### Assumptions and limitations

The model works unders the assumption that all inputs have been normalized and are bounded between 0 and 1, taking any decimal value in between. 

For expected improvement, only 256 random candidates are considered.

### Ethical considerations

The model is completely agnostic of the functions being queried. Ethical considerations must be applied to the way the functions behave, what factors they are using and any potential risk of bias. The 8 sample functions used througout the project are "black boxes" and no further determination can be made.

