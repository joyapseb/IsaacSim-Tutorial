<img width="1609" height="530" alt="image" src="https://github.com/user-attachments/assets/b0ab6e6c-fc52-4dd6-918b-2d22dd49c750" /># Examples section
**Let's get familiar with the GUI using an example**

Follow the following route: ***Window->Examples->Robotics Examples***

<img width="1080" height="484" alt="route" src="https://github.com/user-attachments/assets/004c7ff5-3abd-4a7a-95e6-8ea8b096867f" />

A tab (*Robotics Examples*) in the lower part will appear.

Please select an example of your interest and *Load the Scene*

<img width="1136" height="441" alt="example_robot" src="https://github.com/user-attachments/assets/8295dffc-c46a-4657-bc30-0b1f4607cb73" />


## Example using *Manipulation -> Follow Target Task*

<img width="1609" height="530" alt="target1" src="https://github.com/user-attachments/assets/81d8b23a-abd7-4d9f-bf09-f7b86805dcd7" />

### Important sections
* **Stage**: Shows all the objects in the Stage. In this case, the ones interacting are the TargetCube and Franka (Robot).
* **Stage Lights**: Enables changing the lightning for visualization purposes.
*  **Perspective** If a camera is enabled, it is possible to change the perspective
*  **Left bar**: Change position & Orientation, Start & Stop simulation


Depending on the selected example, select the appropriate options to run the simulation
(In Task Control -> Start)
   <img width="1609" height="530" alt="Run" src="https://github.com/user-attachments/assets/c50e8693-70cf-41c0-8f28-4b7c67b993b0" />

[Follow_video.webm](https://github.com/user-attachments/assets/0a9d37d1-6f08-49e9-a33f-be10674943d5)

As seen in the video, the example shows how to follow a target using Franka robot in Isaac Sim.

### Access the code
<img width="384" height="354" alt="source" src="https://github.com/user-attachments/assets/63ae7891-d8ad-4fe3-a9a1-603500667822" />

To access the code, select the icon with the square and pencil -> Your default code editor will be opened.

The following code is for reference*

```
# Copyright (c) 2021-2024, NVIDIA CORPORATION. All rights reserved.
#
# NVIDIA CORPORATION and its licensors retain all intellectual property
# and proprietary rights in and to this software, related documentation
# and any modifications thereto. Any use, reproduction, disclosure or
# distribution of this software and related documentation without an express
# license agreement from NVIDIA CORPORATION is strictly prohibited.
#

from isaacsim.examples.interactive.base_sample import BaseSample
from isaacsim.robot.manipulators.examples.franka.controllers.rmpflow_controller import RMPFlowController
from isaacsim.robot.manipulators.examples.franka.tasks import FollowTarget as FollowTargetTask


class FollowTarget(BaseSample):
    def __init__(self) -> None:
        super().__init__()
        self._controller = None
        self._articulation_controller = None

    def setup_scene(self):
        world = self.get_world()
        world.add_task(FollowTargetTask())
        return

    async def setup_pre_reset(self):
        world = self.get_world()
        if world.physics_callback_exists("sim_step"):
            world.remove_physics_callback("sim_step")
        self._controller.reset()
        return

    def world_cleanup(self):
        self._controller = None
        return

    async def setup_post_load(self):
        self._franka_task = list(self._world.get_current_tasks().values())[0]
        self._task_params = self._franka_task.get_params()
        my_franka = self._world.scene.get_object(self._task_params["robot_name"]["value"])
        self._controller = RMPFlowController(name="target_follower_controller", robot_articulation=my_franka)
        self._articulation_controller = my_franka.get_articulation_controller()
        return

    async def _on_follow_target_event_async(self, val):
        world = self.get_world()
        if val:
            await world.play_async()
            world.add_physics_callback("sim_step", self._on_follow_target_simulation_step)
        else:
            world.remove_physics_callback("sim_step")
        return

    def _on_follow_target_simulation_step(self, step_size):
        observations = self._world.get_observations()
        actions = self._controller.forward(
            target_end_effector_position=observations[self._task_params["target_name"]["value"]]["position"],
            target_end_effector_orientation=observations[self._task_params["target_name"]["value"]]["orientation"],
        )
        self._articulation_controller.apply_action(actions)
        return

    def _on_add_obstacle_event(self):
        world = self.get_world()
        current_task = list(world.get_current_tasks().values())[0]
        cube = current_task.add_obstacle()
        self._controller.add_obstacle(cube)
        return

    def _on_remove_obstacle_event(self):
        world = self.get_world()
        current_task = list(world.get_current_tasks().values())[0]
        obstacle_to_delete = current_task.get_obstacle_to_delete()
        self._controller.remove_obstacle(obstacle_to_delete)
        current_task.remove_obstacle()
        return

    def _on_logging_event(self, val):
        world = self.get_world()
        data_logger = world.get_data_logger()
        if not world.get_data_logger().is_started():
            robot_name = self._task_params["robot_name"]["value"]
            target_name = self._task_params["target_name"]["value"]

            def frame_logging_func(tasks, scene):
                return {
                    "joint_positions": scene.get_object(robot_name).get_joint_positions().tolist(),
                    "applied_joint_positions": scene.get_object(robot_name)
                    .get_applied_action()
                    .joint_positions.tolist(),
                    "target_position": scene.get_object(target_name).get_world_pose()[0].tolist(),
                }

            data_logger.add_data_frame_logging_func(frame_logging_func)
        if val:
            data_logger.start()
        else:
            data_logger.pause()
        return

    def _on_save_data_event(self, log_path):
        world = self.get_world()
        data_logger = world.get_data_logger()
        data_logger.save(log_path=log_path)
        data_logger.reset()
        return
```

# Hands-on Example

To get familiar with Isaac Sim, I recommend to follow this [documentation](https://docs.isaacsim.omniverse.nvidia.com/5.1.0/robot_setup_tutorials/index.html). It spans from Beginner, Intermediate and Advanced Tutorials.

In this occasion, we will follow Tutorials 1-4
* [Tutorial 1: Stage Setup](https://docs.isaacsim.omniverse.nvidia.com/5.1.0/robot_setup_tutorials/tutorial_intro_environment_setup.html)
* [Tutorial 2: Assemble a Simple Robot](https://docs.isaacsim.omniverse.nvidia.com/5.1.0/robot_setup_tutorials/tutorial_intro_assemble_robot.html)
* [Tutorial 3: Articulate a Basic Robot](https://docs.isaacsim.omniverse.nvidia.com/5.1.0/robot_setup_tutorials/tutorial_gui_simple_robot.html)
* [Tutorial 4: Add Camera and Sensors to a Robot](https://docs.isaacsim.omniverse.nvidia.com/5.1.0/robot_setup_tutorials/tutorial_gui_camera_sensors.html)

## Thank you for following the Tutorial

#Important Links
*[Tutorial Reference Tables](https://docs.isaacsim.omniverse.nvidia.com/5.1.0/introduction/tutorial_list.html)
*[Isaac Sim Conventions](https://docs.isaacsim.omniverse.nvidia.com/5.1.0/reference_material/reference_conventions.html)
*[Sensors](https://docs.isaacsim.omniverse.nvidia.com/5.1.0/sensors/index.html)

