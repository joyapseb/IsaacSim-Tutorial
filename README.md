# IsaacSim-Tutorial
Basic Tutorial to Install IsaacSim | Examples of use

You can find the official documentation in the following link: [Isaac Sim](https://docs.isaacsim.omniverse.nvidia.com/5.1.0/index.html)

In this tutorial we will follow the installation recommended to use along with [Isaac Lab](https://isaac-sim.github.io/IsaacLab/main/index.html)

#Notes
Isaac Sim is compatible with Windows and Ubuntu 22.04 (recommended) & 24.04.

Isaac Sim is built against a specific Python version, making it essential to use the same Python version when installing Isaac Lab. The required Python version is as follows:
For Isaac Sim 5.X, the required Python version is 3.11.
For Isaac Sim 4.X, the required Python version is 3.10.

Use the latest NVIDIA production branch driver.
On Linux, version 580.65.06 or later is recommended, especially when upgrading to Ubuntu 22.04.5 with kernel 6.8.0-48-generic or newer.


#Installation
In this tutorial we will follow the Local Installation using *pip install*. For more other installation methods, follow ([Installation](https://isaac-sim.github.io/IsaacLab/main/source/setup/installation/index.html))

| Method  | Isaac Sim | Isaac Lab | Best for | Difficulty |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| Recommended  | 📦 pip install  | 💾 source (git) | Beginners, standard use | Easy |
| Binary + Source  | 📥 binary download | 💾 source (git) | Users preferring binary install of Isaac Sim | Easy |
| Full Source Build  | 💾 source (git) | 💾 source (git) | Developers modifying both | Advanced |
| Pip Only  | 📦 pip install | 📦 pip install | External extensions only (no training/examples) | Special case |
| Docker  | 🐳 Docker | 💾 source (git) | Docker users | Advanced |


#Citation
@article{mittal2025isaaclab,
   title={Isaac Lab: A GPU-Accelerated Simulation Framework for Multi-Modal Robot Learning},
   author={Mayank Mittal and Pascal Roth and James Tigue and Antoine Richard and Octi Zhang and Peter Du and Antonio Serrano-Muñoz and Xinjie Yao and René Zurbrügg and Nikita Rudin and Lukasz Wawrzyniak and Milad Rakhsha and Alain Denzler and Eric Heiden and Ales Borovicka and Ossama Ahmed and Iretiayo Akinola and Abrar Anwar and Mark T. Carlson and Ji Yuan Feng and Animesh Garg and Renato Gasoto and Lionel Gulich and Yijie Guo and M. Gussert and Alex Hansen and Mihir Kulkarni and Chenran Li and Wei Liu and Viktor Makoviychuk and Grzegorz Malczyk and Hammad Mazhar and Masoud Moghani and Adithyavairavan Murali and Michael Noseworthy and Alexander Poddubny and Nathan Ratliff and Welf Rehberg and Clemens Schwarke and Ritvik Singh and James Latham Smith and Bingjie Tang and Ruchik Thaker and Matthew Trepte and Karl Van Wyk and Fangzhou Yu and Alex Millane and Vikram Ramasamy and Remo Steiner and Sangeeta Subramanian and Clemens Volk and CY Chen and Neel Jawale and Ashwin Varghese Kuruttukulam and Michael A. Lin and Ajay Mandlekar and Karsten Patzwaldt and John Welsh and Huihua Zhao and Fatima Anes and Jean-Francois Lafleche and Nicolas Moënne-Loccoz and Soowan Park and Rob Stepinski and Dirk Van Gelder and Chris Amevor and Jan Carius and Jumyung Chang and Anka He Chen and Pablo de Heras Ciechomski and Gilles Daviet and Mohammad Mohajerani and Julia von Muralt and Viktor Reutskyy and Michael Sauter and Simon Schirm and Eric L. Shi and Pierre Terdiman and Kenny Vilella and Tobias Widmer and Gordon Yeoman and Tiffany Chen and Sergey Grizan and Cathy Li and Lotus Li and Connor Smith and Rafael Wiltz and Kostas Alexis and Yan Chang and David Chu and Linxi "Jim" Fan and Farbod Farshidian and Ankur Handa and Spencer Huang and Marco Hutter and Yashraj Narang and Soha Pouya and Shiwei Sheng and Yuke Zhu and Miles Macklin and Adam Moravanszky and Philipp Reist and Yunrong Guo and David Hoeller and Gavriel State},
   journal={arXiv preprint arXiv:2511.04831},
   year={2025},
   url={https://arxiv.org/abs/2511.04831}
}
