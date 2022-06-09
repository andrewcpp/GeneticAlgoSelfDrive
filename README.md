# Self-Driving Simulation with Genetic and Clonal Selection Algorithms

This Unity project is a modified version of [https://github.com/ArztSamuel/Applying_EANNs](https://github.com/ArztSamuel/Applying_EANNs) to simulate clonal selection algorithms for self navigation problems. It also applies different selection schemes for preexisting genetic algorithms. Modified scripts are present in [UnityProject/Assets/Scripts/AI](UnityProject/Assets/Scripts/AI/). For a detailed description of the project, please take a look at [Research/paper.pdf](Research/paper.pdf). Below is ArztSamuel's original README modified accordingly to this research project.

## Introduction: Applying Evolutionary Artificial Neural Networks

A 2D Unity simulation in which cars learn to navigate themselves through different courses. The cars are steered by a feedforward Neural Network. The weights of the network are trained using modified genetic algorithms with various selections methods and clonal selection algorithms.
Short demo video of an early version: https://youtu.be/rEDzUT3ymw4

![](Images/Demo.gif)

## The Simulation

Cars have to navigate through a course without touching the walls or any other obstacles of the course. A car has five front-facing sensors which measure the distance to obstacles in a given direction. The readings of these sensors serve as the input of the car's neural network. Each sensor points into a different direction, covering a front facing range of approximately 90 degrees. The maximum range of a sensor is 10 unity units. The output of the Neural Network then determines the car’s current engine and turning force.

<img src="Images/Car.png" width="250">

If you would like to tinker with the parameters of the simulation, you can do so in the Unity Editor. If you would simply like to run the simulation with default parameters, you can start the built file [Builds/Applying EANNs.exe](Builds/Applying EANNs.exe).

## The Neural Network

The Neural Network used is a standard, fully connected, feedforward Neural Network. It comprises 4 layers: an input layer with 5 neurons, two hidden layers with 4 and 3 neurons respectively and an output layer with 2 neurons.
The code for the Neural Network can be found at [UnityProject/Assets/Scripts/AI/NeuralNetworks/](UnityProject/Assets/Scripts/AI/NeuralNetworks/).

## Training the Neural Network

The weights of the Neural Network are trained using an Evolutionary Algorithm known as the Genetic Algorithm.

At first there are N randomly initialised cars spawned. The best cars are then selected to be recombined with each other, creating new "offspring" cars. These offspring cars then form a new population of N cars and are also slightly mutated in order to inject some more diversity into the population. The newly created population of cars then tries to navigate the course again and the process of evaluation, selection, recombination and mutation starts again. One complete cycle from the evaluation of one population to the evaluation of the next is called a generation.

The generic version of a Genetic Algorithm can be found at [UnityProject/Assets/Scripts/AI/Evolution/GeneticAlgorithm.cs](UnityProject/Assets/Scripts/AI/Evolution/GeneticAlgorithm.cs). This class can be modified in a very easy way, by simply assigning your own methods to the delegate operator methods of the class. Some example code for adapting the Genetic Algorithm to your own needs can be found in the EvolutionManager  [UnityProject/Assets/Scripts/AI/Evolution/EvolutionManager.cs](UnityProject/Assets/Scripts/AI/Evolution/EvolutionManager.cs), which is already able to switch between two differently modified Genetic Algorithms.

The additions of clonal selection algorithm and genetic algorithms implemented with variety of selection methods also exist in the same file at [UnityProject/Assets/Scripts/AI/Evolution/GeneticAlgorithm.cs](UnityProject/Assets/Scripts/AI/Evolution/GeneticAlgorithm.cs). They are added as different methods in the class along with additions of necessary fields for running those methods.

## User Interface

The user interface always displays the data of the current best car. In the top left corner the Neural Network's output (engine and turning) is displayed. Right below the output, the evaluation value is displayed (the evaluation value is equal to the percentage of course completion). In the lower left corner a generation counter is displayed. In the upper right corner the Neural Network of the current best car is displayed. The weights are symbolised by the color and width of the connections between neurons: The wider a connection, the bigger the absolute value of the weight; Green means that the weight is positive, red means that the weight is negative.

The entire UI-code is located at [UnityProject/Assets/Scripts/GUI/](UnityProject/Assets/Scripts/GUI/).

## Courses

There are multiple courses of different difficulties, which are all located in different unity scenes and can be found in the folder [UnityProject/Assets/Scenes/Tracks/](UnityProject/Assets/Scenes/Tracks/).

In order to start the simulation on a specific course, open the Main scene and enter the desired track name (= scene name) in the Inspector of the GameStateManager object. Here are two example courses:

![Two different courses the cars can be trained on.](Images/Courses.png)

## License

Full credit to @ArztSamuel for the [original repository](https://github.com/ArztSamuel/Applying_EANNs), which provided me a groundwork I could work with for this research.
