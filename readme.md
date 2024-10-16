A large number of real-world systems can be represented as a set of probabilistic equations structured in a directed acyclic graph.
Since the data-generating process can be realized by ancestral sampling, these systems can be considered causal and have been widely studied in the causal effect estimation literature.

To guide a given system toward realizing desirable states, we seek to fit a model from observational data to plan appropriate interventions.
While fitting a generative model to observational data can tell us which states are more or less likely, it doesn't tell us how the system will respond to intervention.
We need to derive an estimator of the system's Jacobian, as it encodes the differential changes in input/output we should expect.

While there is a large body of work on the identifiability of the casual structure with specific algorithms, we ask whether it is possible for a model to
learn to identify the Jacobian in context (not in weight) and internally implement the necessary algorithm (in its weights).

The following experiments aim to present such a task.
