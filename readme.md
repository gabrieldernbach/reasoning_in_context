Great number of real world systems can be represented as a set of probabilistic equations structured in a directed acyclic graphs.
As the data generating process can be realized by ancestral sampling, these systems can be considered causal, and have been widely studied in causal effect estimation literature.

In order to steer a given system towards generation of desirable states, we seek to fit a model from observational data to plan suitable interventions.
While fitting a generative model to observational data can tell us which states are more or less likely, it doesn't tell us how the system responds to intervention.
Formally, we need to derive an estimator of the systems jacobian, as it encodes the differential changes in intput/output.

While there exists a large body of work on the identifiability of the casual structure with specific algorithms, we ask, if it is possible for a model to
learn to identify the jacobian in context (not in weight). 

The following experiments aim at presenting such a task.
