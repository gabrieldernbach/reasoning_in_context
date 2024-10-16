Many real-world systems can be represented as probabilistic equations organised in a directed acyclic graph (DAG). These systems, where the data generating process is modelled by ancestral sampling, are causal in nature and have been extensively studied in the causal effect estimation literature.

Intervening in such systems to achieve desirable states requires more than fitting a generative model from observational data. While generative models reveal which states are more or less likely, they do not provide information about how the system will respond to interventions. To predict these responses, it is necessary to estimate the system's Jacobian, which encodes the sensitivity of outputs to changes in inputs.

Recent advances in in-context learning have demonstrated the ability of a model to perform tasks such as regression and classification without updating its weights. The model adapts dynamically to the task using only the information provided by the input context. Extending this concept to the Jacobian, we propose that a model could learn to estimate the Jacobian in context, allowing it to infer the effects of interventions without relying on pre-programmed algorithms.

Our hypothesis is that in-context learning, already proven in prediction tasks, can be used for intervention planning. By dynamically learning the Jacobian, the model can internally implement reasoning about system responses to change. This approach represents a shift from explicitly identifying causal structures through algorithms to training models to reason about causality as part of their learned context.

The experiments presented here are designed to test the feasibility of this approach.
