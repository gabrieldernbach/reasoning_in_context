Many real-world systems can be represented as probabilistic equations organised in a directed acyclic graph (DAG). These systems, where the data generating process is modelled by ancestral sampling, are causal in nature and have been extensively studied in the causal effect estimation literature.

Intervening in such systems to achieve desirable states requires more than fitting a generative model from observational data. While generative models reveal which states are more or less likely, they do not provide information about how the system will respond to interventions. To predict these responses, it is necessary to estimate the system's Jacobian, which encodes the sensitivity of outputs to changes in inputs.

Recent advances in in-context learning have demonstrated the ability of a model to perform tasks such as regression and classification without updating its weights. The model adapts dynamically to the task using only the information provided by the input context. Extending this concept to the Jacobian, we propose that a model could learn to estimate the Jacobian in context, allowing it to infer the effects of interventions without relying on pre-programmed algorithms.

Our hypothesis is that in-context learning, already proven in prediction tasks, can be used for intervention planning. By dynamically learning the Jacobian, the model can internally implement reasoning about system responses to change. This approach represents a shift from explicitly identifying causal structures through algorithms to training models to reason about causality as part of their learned context.

The experiments presented here are designed to test the feasibility of this approach.


## Problem statement and practical approach
In this experiment, we want to test whether a model can learn to predict how a system responds to interventions by processing only observational data in context. While the model sees no intervention during its input phase, the supervisory signal during training includes the results of interventions, which guides the model in learning the causal structure of the system. The hypothesis is that the model can infer the Jacobian of the system through in-context learning, using both observational data and feedback from intervention outcomes.

## Data generation (DAG construction and sampling)
We repeatedly sample systems as Directed Acyclic Graph (DAG), where each node represents a variable and the edges represent probabilistic causal relationships between them. The graph is sampled with edge drop probabilities, ensuring that the links between variables are non-trivial and variable across samples.

For each sample:
* Observation data (X): These are taken from the system without any intervention. This is the only input the model sees during training.
* Intervention (I) and outcome (Y): A random intervention is applied to a node in the very last observed sample and the response of the system to this counter factual sample is captured in the outcome (Y). This data is not provided as input to the model, but serves as a target in the training loss, guiding the model as it learns the dynamics of the system generating the in-context samples.

The key challenge is that the model must learn the relationships between variables and generalise its understanding to predict the effect of interventions using only the observational data for context.

## Model Architecture (Transformer for In-Context Learning)

The architecture is a transformer-based model that processes sequences of observational data. Transformers are chosen for their ability to learn dependencies and relationships within sequences, making them well suited to in-context learning tasks where patterns emerge from the input data.

Key components:

* Input representation: The model receives the observation data (X) as its only input, with no direct knowledge of the interventions.
* Transformer Backbone: The transformer layers use bidirectional attention mechanisms to capture relationships between variables, allowing the model to infer how changes in one variable might propagate through the system.
* Prediction Output: The model predicts how the system would respond to an intervention, even though it does not see the intervention in its input. The output (Y) is used as the target for training.


## Loss function and training process

The loss function calculates the difference between the model's predicted outcomes and the actual post-intervention outcomes (Y). This provides the necessary monitoring signal, even though the interventions themselves are not part of the input data. By minimising this loss, the model is encouraged to learn the causal relationships between variables that determine how interventions affect system outcomes.

The training process involves

* Feeding the model with purely observational data.
* Calculating the model's predictions of how the system would respond to an intervention on the very last sample.
* Comparing the predictions with actual outcomes (Y) and updating the model accordingly.

Over time, the model should improve in its ability to generalise from observational data to predict system behaviour under unseen interventions.

## Role of mixing and visualisation

Before the data is fed into the model, the variables in the observed data are shuffled. This ensures that the model cannot rely on positional biases and instead must learn the underlying relationships between the variables. The unshuff array is provided not to the model but to the user, allowing the user to restore the variables to their original causal order for visualisation purposes. The model remains unaware of the original ordering throughout training.

## Hypothesis testing

The core hypothesis is that the model can learn the Jacobian of the system - its sensitivity to change - by observing only the relationships in the observed data. Although the interventions themselves are not part of the input, the intervention results (Y) are used as a training signal to help the model understand how the system behaves under intervention.

After training, the model is evaluated on its ability to predict intervention outcomes that it has never seen in context, testing whether it has implicitly learned the causal dynamics of the system.
