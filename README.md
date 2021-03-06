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

### sanity_linear & sanity_original

1. Recorded Loss, as loss stands for TD. Ran 10k steps each. (Simple linear vs Original model)

    -__Result__: As expected, linear model's loss increases as steps proceeds, while original model did not grow higher after about 3k steps. *(The result log is in local computer.)*
    
- Blue : Original model
- Orange : Linear model
    
> Loss (smoothing 0.95)
![image](https://user-images.githubusercontent.com/45917844/90638358-36145600-e268-11ea-9163-67cd8df93adf.png)

> Reward (smoothing 0.95)
![image](https://user-images.githubusercontent.com/45917844/90638425-462c3580-e268-11ea-8900-0e3ba5c31aa7.png)

> MaxQ (smoothing 0.95)
![image](https://user-images.githubusercontent.com/45917844/90638531-66f48b00-e268-11ea-8529-d33e7a9fc225.png)



### new_model
2. More complex model test. For accurate comparison, the model starts without pre-learned model, and the apple reward is 1.01. (Movement punishment is set to -0.01)

> Loss (smoothing 0.95)
![image](https://user-images.githubusercontent.com/45917844/90637903-8f2fba00-e267-11ea-879a-456ae3708a86.png)

> Reward (smoothing 0.95)
![image](https://user-images.githubusercontent.com/45917844/90637955-9f479980-e267-11ea-83bb-dd0d01a6e55c.png)

> Score (smoothing 0.95)
![image](https://user-images.githubusercontent.com/45917844/90638066-c8682a00-e267-11ea-9bd8-562d922aa25c.png)

> MaxQ (smoothing 0.95)
![image](https://user-images.githubusercontent.com/45917844/90638011-b4242d00-e267-11ea-8619-055947c0263f.png)


## Diagnosis

1. Did not change much. Making the model more complex does not help in terms of learning.

2. While comparing with the past test, which was giving rewards to the mouse per movement, I realized that giving reward per movement may seem to accomplish task well, it was not learning the 'actual target'.
    - The model learned that 'moving toward' the apple is good, not 'the apple' is good.
    - Thus, the q value was fluctuating even though the mouse was eating the apple well.
    - The mouse was 'surprised' getting the big reward by eating the apple everytime.

3. Therefore, the results show that current learning algorithm is not suitable with sparse rewards.

## TODO

1. Study about sparse rewards.
