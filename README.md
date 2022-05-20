# Trained-ML-Agents-Actors
Trained ML-Agent Actors on PPO and SAC algorithms in the following scenes and tasks: 3DBall, 3DBallHard, Basic, Crawler, Hallway, PushBlock, Walker, WallJump, and Worm. All the actors have been trained using the default configurations and assets provided by the [Unity ML-Agent Toolkit](https://github.com/Unity-Technologies/ml-agents). This repo contains both the trained model files (.onnx) and the logs of the training for comparing both algorithms.

## Installations
- Follow installation instructions from: [ML-Agent Toolkit - Installation](https://github.com/Unity-Technologies/ml-agents/blob/main/docs/Installation.md) 
	- For "Install the com.unity.ml-agents Unity package" and "Install the com.unity.ml-agents.extensions Unity package (Optional)" follow instructions on "Setting Up Unity Environment with ML-Agent" in this readMe

## Setting Up Unity Environment with ML-Agent
1. Download ML-Agent from: [ML-Agent Toolkit - Source](https://github.com/Unity-Technologies/ml-agents#releases--documentation) and extract it to any desired location.
2. Create a New Project with 3D Core Template as base in Unity Hub.
3. Open the project.
4. Add `com.unity.ml-agents` package to Unity your Project.
    - Navigate to the menu `Window` -> `Package Manager`.
    - In the **Package Manager** window click on the `+` button on the top left of the packages list.
    - Select `Add package from disk...`
    - Navigate into the `com.unity.ml-agents` folder from Step 1.
    - Select the `package.json` file.
	  - Wait for compilation.
5. Add `com.unity.ml-agents.extensions` package to your Unity Project using the same steps as in 4).
6. Add `Input System` package to your Unity Project
    - Navigate to the menu `Window` -> `Package Manager`.
    - In the **Package Manager** window click on `Packages:` "Unity Registry" and in the search bar, input "Input System"
    - Select the `Input System package` and click Install
7. Using **File Explorer** *(outside Unity)*, go to `<ProjectFolder>/Packages/manifest.json` and add the following dependency: `"com.unity.nuget.newtonsoft-json": "2.0.0"`
8. From the folder created in Step 1), copy `Project/Assets/ML-Agents` into `<ProjectFolder>/Assets`
9. In the **Project Console**, open any of the scenes in `Assets/ML-Agents/Examples/<Environment>/Scenes/<EnvironmentGame>`
10. Go to `Edit` -> `Project Settings` -> `Player` -> (Under) `Other Settings` -> (Under) `Configuration` -> `Active Input Handling`, Select the Option `"Both"` and wait for Unity to Restart.
11. At this point, the Scene should be able to run.

## How to Train Agents
[Example Video](https://www.youtube.com/watch?v=iF6p9d7CFC0) 
1. Open the desired environment scene in your Unity Project
2. Open a python terminal and move to the main folder containing ML-Agent extracted in ''Setting Up Unity Environment with ML-Agent''
3. Run `mlagents-learn config/<actor>/<environment>.yaml --run-id=<any_name>`
4. Click `Play` in Unity
5. At this point, the Actor should be training
	
## Loading a Trained Model into the Scene Agents.
[Example Video](https://www.youtube.com/watch?v=MBxbIt1HCzs)   
1. The trained models are provided in `Results/<Environment>-<actor>/<Environment>-<actor>.onnx`. i.e., the model for `3D Ball` trained on `SAC` algorithm can be found in `results/3DBall-sac/3DBall-sac.onnx`.
2. Copy model into `Assets/ML-Agents/Examples/<Environment>/TFModels/`
3. Inside the scene of *Unity*, go to the **Hierarchy** and select any of the models named as the environment.
4. Search and select the child with the name "Agent", "BaseAgent", or variants of it and go to it's `inspector` -> (under) `Behaviour Parameters` -> `Model` -> (drag and drop onnx model into pane or select it from the search option)
5. Right click on the `Model` Text Bar and click on `Apply to Prefab` to effectuate the changes to all agents.
6. Run scene
  
## Observing Training Statistics
[Example Video](https://www.youtube.com/watch?v=y5D_AYjQiAA)    
1. Follow installation instructions for the python packages from: [ML-Agent Toolkit - Installation - Python Package](https://github.com/Unity-Technologies/ml-agents/blob/main/docs/Installation.md#install-the-mlagents-python-package)
2. Open a python terminal and move to the folder containing `/results/`
3. Run the following command: 
```
tensorboard --logdir results
```
4. Using a browser, open `localhost:6006`.
5. You now have access to the TensorBoard summary of the stastistics!

Note: For more information on training models and their statisctics, refer to [ML-Agent Toolkit - Getting Started](https://github.com/Unity-Technologies/ml-agents/blob/main/docs/Getting-Started.md)
