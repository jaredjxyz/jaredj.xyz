# Behavioral Cloning: Udacity SDC Nanodegree Term 1 Project 3
## [Github](https://github.com/jaredjxyz/CarND-Behavioral-Cloning)

## Introduction
Behavioral cloning is a machine learning technique used to train an agent (whether that's simulated or a robot) to act by looking at what a human has told the robot to do in similar situations. In this project, we drove a car around a virtual environment, collected data on how I drove, then used a neural network to make the car drive the same way.

## Process
My initial model took in two laps' worth of data around the track in the simulator. With this model, the car would turn left when it needed to turn left and turn right when it needed to turn right, but it would turn at such extreme angles that it couldn't go very fast.

I found two things that helped this: increasing the learning rate, which smoothed out the actions, and changing the optimizer to an Adam optimizer instead of a regular Gradient Descent optimizer.

With these two changes, the car was much smoother, but would not turn sharp enough. It looked as if the car had overfit for straightaways.

I did two things to counteract this. First, I took away 50% of the data where the steering angle was less than 10 degrees. Second, I recorded myself taking some more sharp turns.

Now, instead of retraining the model with the above data, I took the existing model, and extended the training with the new data. The idea behind this was that I liked how smooth the existing model was, I just wanted to make small adjustments to it. It worked well, and after this the car would go full speed around the track. I didn't think that was good enough, though.

The car still seemed to try and go left on the straightways and then correct itself to go right occasionally. This caused me to think that it was overfit going to the left. I flipped all of the training data and added it to the original training data, and then continued training the model on the new doubled data. After 8 epochs, the model now went straight on straightways.

## Conclusion

I ended up very happy with a model that could go around the track at the highest speed the simulator would allow it, since this very much surpassed the requirements for the project. I learned a lot, like when to continue training an already trained network and when to start from scratch, how important training data is, and how hyperparameters affect your neural network.

## Video

#### First attempt
<iframe width="560" height="315" src="https://www.youtube.com/embed/oCCUO0-F_WM" frameborder="0" gesture="media" allow="encrypted-media" allowfullscreen></iframe>

#### Final attempt
<iframe width="560" height="315" src="https://www.youtube.com/embed/hflPGI8BXa4" frameborder="0" gesture="media" allow="encrypted-media" allowfullscreen></iframe>
