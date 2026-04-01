# Collision Avoidance for Convex Primitives via Differentiable Optimization Based High-Order Control Barrier Functions

This repository contains the implementation for the paper **"Collision Avoidance for Convex Primitives via Differentiable Optimization Based High-Order Control Barrier Functions"** by Shiqing Wei, Rooholla Khorrambakht, Prashanth Krishnamurthy, Vinicius Mariano Gonçalves, and Farshad Khorrami.

📝 [**IEEE**](https://ieeexplore.ieee.org/document/11124847/) | 📄 [**arXiv**](https://arxiv.org/abs/2410.19159) | 🎥 [**YouTube**](https://youtu.be/uZmM3_wBjGY)

## 🛠️ Prerequisites

To ensure full reproducibility and avoid environment setup headaches, this project relies heavily on **Docker** and **VS Code Dev Containers**.

Make sure you have the following installed on your host machine:

1. [Docker](https://docs.docker.com/get-docker/)
2. [Visual Studio Code (VS Code)](https://code.visualstudio.com/)
3. The [Dev Containers Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) for VS Code.

## 🚀 Installation & Environment Setup

### 1. Enable GUI Display (Linux Host)

Since the simulations use visualizers (like MuJoCo) that require a GUI, you must allow the Docker container to connect to the host's X server. Open your **host terminal** and run:

```bash
xhost +local:root
```

*(Note: You may need to run this command again if you restart your host computer).*

### 2. Clone the Repository

```bash
git clone https://github.com/shiqingw/DiffOpt-HOCBF-Pub.git
cd DiffOpt-HOCBF-Pub
```

### 3. Build the Dev Container

We use VS Code's Dev Container feature to automatically build the environment, install all dependencies (including PyTorch, OSQP, and MuJoCo), and configure user permissions.

1. Open the cloned directory in VS Code:
   ```bash
   code .
   ```

2. Press `Ctrl + Shift + P` to open the Command Palette.
3. Type and select: **`Dev Containers: Rebuild Container without Cache`**
4. Wait for the image to build. Once finished, your VS Code terminal will be running seamlessly inside the isolated, fully configured environment.

## 🏃‍♂️ Running the Simulations

Once inside the Dev Container, you can run the experiments directly from the integrated terminal.

### 1. Pick and Place

#### 1. The case without circulation
```bash
python3 eg1_fr3_circulation/polytope3_cpp_thread_osqp.py
```

#### 2. The case with circulation
```bash
python3 eg1_fr3_circulation/polytope3_cpp_thread_smooth_min_osqp.py
```

### 2. Avoiding a Flying Ball
```bash
python3 eg2_fr3_flying_ball/flying_ball_relaxation_osqp.py
```

## 📑 Citation

If you find this code or our paper useful in your research, please consider citing:

```bibtex
@article{wei2025collision,
  author={Wei, Shiqing and Khorrambakht, Rooholla and Krishnamurthy, Prashanth and Mariano Gonçalves, Vinicius and Khorrami, Farshad},
  journal={IEEE Transactions on Control Systems Technology}, 
  title={Collision Avoidance for Convex Primitives via Differentiable Optimization-Based High-Order Control Barrier Functions}, 
  year={2026},
  volume={34},
  number={1},
  pages={3-18},
  keywords={Collision avoidance;Robots;Safety;Optimization;Torque control;Vectors;Planning;Symmetric matrices;Shape;Euclidean distance;Collision avoidance;quadratic programming (QP);robot control},
  doi={10.1109/TCST.2025.3595751}}

}
```

## 📄 License

This project is open-sourced under the [MIT License](LICENSE).