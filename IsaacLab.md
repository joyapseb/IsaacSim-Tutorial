# Isaac Lab Installation
You can follow this tutorial and/or continue the official [documentation](https://isaac-sim.github.io/IsaacLab/main/source/setup/installation/pip_installation.html#installing-isaac-lab)

## Cloning Isaac Lab
* HTTPS
```
git clone https://github.com/isaac-sim/IsaacLab.git
```
The following command can be used to manage extensions
```
./isaaclab.sh --help

usage: isaaclab.sh [-h] [-i] [-f] [-p] [-s] [-t] [-o] [-v] [-d] [-n] [-c] -- Utility to manage Isaac Lab.

optional arguments:
   -h, --help           Display the help content.
   -i, --install [LIB]  Install the extensions inside Isaac Lab and learning frameworks (rl_games, rsl_rl, sb3, skrl) as extra dependencies. Default is 'all'.
   -f, --format         Run pre-commit to format the code and check lints.
   -p, --python         Run the python executable provided by Isaac Sim or virtual environment (if active).
   -s, --sim            Run the simulator executable (isaac-sim.sh) provided by Isaac Sim.
   -t, --test           Run all python pytest tests.
   -o, --docker         Run the docker container helper script (docker/container.sh).
   -v, --vscode         Generate the VSCode settings file from template.
   -d, --docs           Build the documentation from source using sphinx.
   -n, --new            Create a new external project or internal task from template.
   -c, --conda [NAME]   Create the conda environment for Isaac Lab. Default name is 'env_isaaclab'.
   -u, --uv [NAME]      Create the uv environment for Isaac Lab. Default name is 'env_isaaclab'.
```

## **Installation**
*Install dependencies using *apt* (Linux only):
```
# these dependency are needed by robomimic which is not available on Windows
sudo apt install cmake build-essential
```
*Run the install command that iterates over all the extensions in source directory and installs them using pip (with --editable flag):
```
./isaaclab.sh --install # or "./isaaclab.sh -i"
```
By default, the above will install all the learning frameworks. These include *rl_games*, *rsl_rl*, *sb3*, *skrl*, *robomimic*.

## **Verifying the Isaac Lab installation**
In your virtual environment run and in the *IsaacLab dir*:
```
# Option 1: Using the isaaclab.sh executable
# note: this works for both the bundled python and the virtual environment
./isaaclab.sh -p scripts/tutorials/00_sim/create_empty.py

# Option 2: Using python in your virtual environment
python scripts/tutorials/00_sim/create_empty.py
```

The above command should launch the simulator and display a window with a black viewport. You can exit the script by pressing *Ctrl+C* on your terminal. On Windows machines, please terminate the process from Command Prompt using *Ctrl+Break* or *Ctrl+fn+B*.
Simulator with a black window.

<img width="1610" height="995" alt="isaaclab1" src="https://github.com/user-attachments/assets/438bec9d-095f-4ec3-8faa-91f0d5ea6470" />



If you see this, then the installation was successful! 🎉

##Train a robot!
You can now use Isaac Lab to train a robot through Reinforcement Learning! 

Execute the following command to quickly train an ant to walk! We recommend adding --headless for faster training.

*Robot dog (Anymal)
```
./isaaclab.sh -p scripts/reinforcement_learning/rsl_rl/train.py --task=Isaac-Velocity-Rough-Anymal-C-v0 --headless
```
To visualize (32 envs)
```
./isaaclab.sh -p scripts/reinforcement_learning/rsl_rl/train.py --task=Isaac-Velocity-Rough-Anymal-C-v0 --num_envs 32
```
<img width="1610" height="995" alt="Anymal" src="https://github.com/user-attachments/assets/9f5b78e4-c256-46fd-bf79-d56e1e8dc9f1" />



# Relevant Links
*[Avaliable Environments](https://isaac-sim.github.io/IsaacLab/main/source/overview/environments.html): From classics (Isaac-Cart-Double-Pendulum-Direct-v0),walking (Isaac-Velocity-Rough-H1-v0), manipulation (Isaac-Lift-Cube-Franka-v0) to Contact-Rich Tasks (Isaac-Factory-PegInsert-Direct-v0) and more

*[RL Scripts](https://isaac-sim.github.io/IsaacLab/main/source/overview/reinforcement-learning/rl_existing_scripts.html): Commands to run Available Envs with *rl_games*, *rsl_rl*, *sb3*, *skrl*

*[General Tutorials](https://isaac-sim.github.io/IsaacLab/main/source/tutorials/index.html): Creating Environments, Interaction with objects, using controllers (Task-space, Operational Space), etc.





