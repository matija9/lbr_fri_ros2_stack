>[!NOTE]
>This is a fork of the [lbr-stack](https://github.com/lbr-stack/lbr_fri_ros2_stack) modified for the use with the [PRONOBIS project](https://github.com/CRTA-Lab/KUKA_LBRMed_servoing). If you use this plese credit the original autors of the package.


# lbr_fri_ros2_stack
[![License](https://img.shields.io/github/license/lbr-stack/lbr_fri_ros2_stack)](https://github.com/lbr-stack/lbr_fri_ros2_stack/tree/humble?tab=Apache-2.0-1-ov-file#readme) 
[![Documentation Status](https://readthedocs.org/projects/lbr-stack/badge/?version=latest)](https://lbr-stack.readthedocs.io/en/latest/?badge=latest)
[![JOSS](https://joss.theoj.org/papers/c43c82bed833c02503dd47f2637192ef/status.svg)](https://joss.theoj.org/papers/c43c82bed833c02503dd47f2637192ef) 
[![Code Style: Black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)

ROS 2 packages for the KUKA LBR, including communication to the real robot via the Fast Robot Interface ([FRI](https://github.com/lbr-stack/fri)) and [Gazebo](http://gazebosim.org/) simulation support. Included are the `iiwa7`, `iiwa14`, `med7`, and `med14`.

<body>
    <table>
        <tr>
            <th align="left" width="25%">LBR IIWA 7 R800</th>
            <th align="left" width="25%">LBR IIWA 14 R820</th>
            <th align="left" width="25%">LBR Med 7 R800</th>
            <th align="left" width="25%">LBR Med 14 R820</th>
        </tr>
        <tr>
            <td align="center"><img src="https://raw.githubusercontent.com/lbr-stack/lbr_fri_ros2_stack/humble/lbr_fri_ros2_stack/doc/img/foxglove/iiwa7_r800.png" alt="LBR IIWA 7 R800"></td>
            <td align="center"><img src="https://raw.githubusercontent.com/lbr-stack/lbr_fri_ros2_stack/humble/lbr_fri_ros2_stack/doc/img/foxglove/iiwa14_r820.png" alt="LBR IIWA 14 R820"></td>
            <td align="center"><img src="https://raw.githubusercontent.com/lbr-stack/lbr_fri_ros2_stack/humble/lbr_fri_ros2_stack/doc/img/foxglove/med7_r800.png" alt="LBR Med 7 R800"></td>
            <td align="center"><img src="https://raw.githubusercontent.com/lbr-stack/lbr_fri_ros2_stack/humble/lbr_fri_ros2_stack/doc/img/foxglove/med14_r820.png" alt="LBR Med 14 R820"></td>
        </tr>
    </table>
</body>

<!--
## Status
| OS             | ROS Distribution | FRI Version |  Build Status |
| :------------- | :--------------- | :---------- |  :----------- |
| `Ubuntu-22.04` | `humble`         | `1.11`      |  [![build-ubuntu-22.04-fri-1.11](https://github.com/lbr-stack/lbr_fri_ros2_stack/actions/workflows/build-ubuntu-22.04-fri-1.11.yml/badge.svg)](https://github.com/lbr-stack/lbr_fri_ros2_stack/actions/workflows/build-ubuntu-22.04-fri-1.11.yml) |
| `Ubuntu-22.04` | `humble`         | `1.14`      |  [![build-ubuntu-22.04-fri-1.14](https://github.com/lbr-stack/lbr_fri_ros2_stack/actions/workflows/build-ubuntu-22.04-fri-1.14.yml/badge.svg)](https://github.com/lbr-stack/lbr_fri_ros2_stack/actions/workflows/build-ubuntu-22.04-fri-1.14.yml) |
| `Ubuntu-22.04` | `humble`         | `1.15`      |  [![build-ubuntu-22.04-fri-1.15](https://github.com/lbr-stack/lbr_fri_ros2_stack/actions/workflows/build-ubuntu-22.04-fri-1.15.yml/badge.svg)](https://github.com/lbr-stack/lbr_fri_ros2_stack/actions/workflows/build-ubuntu-22.04-fri-1.15.yml) |
| `Ubuntu-22.04` | `humble`         | `1.16`      |  [![build-ubuntu-22.04-fri-1.16](https://github.com/lbr-stack/lbr_fri_ros2_stack/actions/workflows/build-ubuntu-22.04-fri-1.16.yml/badge.svg)](https://github.com/lbr-stack/lbr_fri_ros2_stack/actions/workflows/build-ubuntu-22.04-fri-1.16.yml) |
| `Ubuntu-22.04` | `humble`         | `2.5`      |  [![build-ubuntu-22.04-fri-2.5](https://github.com/lbr-stack/lbr_fri_ros2_stack/actions/workflows/build-ubuntu-22.04-fri-2.5.yml/badge.svg)](https://github.com/lbr-stack/lbr_fri_ros2_stack/actions/workflows/build-ubuntu-22.04-fri-2.5.yml) |
| `Ubuntu-22.04` | `humble`         | `2.7`      |  [![build-ubuntu-22.04-fri-2.7](https://github.com/lbr-stack/lbr_fri_ros2_stack/actions/workflows/build-ubuntu-22.04-fri-2.7.yml/badge.svg)](https://github.com/lbr-stack/lbr_fri_ros2_stack/actions/workflows/build-ubuntu-22.04-fri-2.7.yml) |
/-->

## Documentation
Full documentation available on [Read the Docs](https://lbr-stack.readthedocs.io/en/latest).

## Quick Start
1. Install ROS 2 development tools

    ```shell
    sudo apt install ros-dev-tools
    ```

2. Create a workspace, clone, and install dependencies

    ```shell
    source /opt/ros/humble/setup.bash
    export FRI_CLIENT_VERSION=1.15
    mkdir -p lbr-stack/src && cd lbr-stack
    vcs import src --input https://raw.githubusercontent.com/matija9/lbr_fri_ros2_stack/refs/heads/humble/lbr_fri_ros2_stack/repos-fri-${FRI_CLIENT_VERSION}.yaml
    rosdep install --from-paths src -i -r -y
    ```

> [!NOTE]
> FRI client is cloned from [fri](https://github.com/lbr-stack/fri) and must be available as branch, refer [README](https://github.com/lbr-stack/fri?tab=readme-ov-file#contributing).

3. Build

    ```shell
    colcon build --symlink-install
    ```

4. In terminal 1, launch a mock setup via

    ```shell
    source install/setup.bash
    ros2 launch lbr_bringup mock.launch.py \
        model:=iiwa7 # [iiwa7, iiwa14, med7, med14]
    ```

> [!TIP]
> List all arguments for the launch file via `ros2 launch lbr_bringup mock.launch.py -s`

5. In terminal 2, visualize the setup via

    ```shell
    source install/setup.bash
    ros2 launch lbr_bringup rviz.launch.py \
        rviz_cfg_pkg:=lbr_bringup \
        rviz_cfg:=config/mock.rviz
    ```

Now, run the [demos](https://lbr-stack.readthedocs.io/en/latest/lbr_fri_ros2_stack/lbr_demos/doc/lbr_demos.html). To get started with the real robot, checkout the [Hardware Setup](https://lbr-stack.readthedocs.io/en/latest/lbr_fri_ros2_stack/lbr_fri_ros2_stack/doc/hardware_setup.html).
