# mouse_test_6

 Smart mouse

## Purpose

mouse_test_5 had shown some indications that the model is not complex enough to learn current conditions. In this test, I am going to check if that was the problem.

## Lessons from last experiment

Just running the test longer does not help much. Think once more before trying some more millions of steps.

## TODO (From mouse_test_5)

1. Add TD to tensorboard scalars. Run a short test with the last model to see if TD remains large and do not converge.

2. Try more complex model. In particular, the eye model should be changed a bit. Conventional multiple convolution layers tend to lower the size of inputs, but increase in the number of filters. That is not the case with current model. The number of filter also decreases as layer gets deeper. Change filter numbers first.

## Plan

1. Add temporal difference to tensorboard scalars. Run a short test in sanity_check environment, comparing a no-hidden-layer model with current model to see if TD fluctuation occurs in the simpler model.

2. If 1. result comes out as expected, make the eye part of the model more complex.

## Other changes

1. Add a scalar recording rewards and scores which takes total_steps as step parameter.

## Tests

1. Recorded Loss, as loss stands for TD. Ran 10k steps each. (Simple linear vs Original model)
    -__Result__: As expected, linear model's loss increases as steps proceeds, while original model did not grow higher after about 3k steps. *(The result log is in local computer.)*

2. More complex model test. For accurate comparison, the model starts without pre-learned model, and the apple reward is 1.01. (Movement punishment is set to -0.01)

## Diagnosis
