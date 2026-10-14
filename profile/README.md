<p align="center">
  <img src="assets/mullet.svg" width="720" alt="MULLET">
</p>

<p align="center">
  <strong>SkyMule · an open drone stack on PX4 + ROS 2</strong><br>
  Multi-drone autonomy for Jetson, from operator browser to flight controller.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/PX4-1.17-FFB547?style=flat-square" alt="PX4 1.17">
  <img src="https://img.shields.io/badge/ROS%202-Jazzy-3DDC97?style=flat-square" alt="ROS 2 Jazzy">
  <img src="https://img.shields.io/badge/NVIDIA-Jetson%20Orin%20Nano-76B900?style=flat-square" alt="Jetson Orin Nano">
  <img src="https://img.shields.io/badge/languages-C%2B%2B%20%C2%B7%20Python%20%C2%B7%20TypeScript-4CC2FF?style=flat-square" alt="C++ · Python · TypeScript">
</p>

---

## 🚁 What we build

**MULLET** is the SkyMule drone stack: a set of small, single-purpose repositories that together
fly PX4 multicopters under ROS 2 Jazzy on NVIDIA Jetson companion computers.

The design rule is a hard control boundary:

- **PX4** owns real-time flight: attitude, motors, failsafes.
- **`mullet_core`** is a deterministic offboard supervisor: arming, takeoff, land, hold, command validation.
- **Mission frameworks** (e.g. ergodic coverage) plan; they never talk to PX4 directly.
- **Operators** drive everything through semantic actions, not raw setpoints.

```text
Browser UI ─► gateway ─► mullet_interfaces ─► mullet_core ─► PX4
                                  ▲                │
                      mission frameworks ──────────┘
```

## 🧩 The stack

| | Repo | What it does |
|---|---|---|
| 🎛️ **Operator** | [`mullet-paddock`](https://github.com/skymule-ai/mullet-paddock) | Web control center: React UI + FastAPI/ROS 2 gateway |
| 📜 **Contract** | [`mullet-interfaces`](https://github.com/skymule-ai/mullet-interfaces) | Shared ROS 2 actions, messages and services, the wire contract of the stack |
| 🧠 **Onboard** | [`mullet-core`](https://github.com/skymule-ai/mullet-core) | C++ offboard supervisor and state machine for PX4 |
| | [`ergodic_mppi`](https://github.com/skymule-ai/ergodic_mppi) | Ergodic coverage mission framework (JAX MPPI) |
| | [`mullet-localization`](https://github.com/skymule-ai/mullet-localization) | Pins sensor/estimator images, calibration, and the EKF2 external-vision bridge |
| 👁️ **Perception** | [`mullet_ros_drivers`](https://github.com/skymule-ai/mullet_ros_drivers) | RealSense D435i and Livox MID-360 driver images |
| | [`mullet_ros_vio`](https://github.com/skymule-ai/mullet_ros_vio) | Visual-inertial odometry (OpenVINS) |
| | [`mullet_ros_lio`](https://github.com/skymule-ai/mullet_ros_lio) | LiDAR-inertial odometry |
| 📦 **Images & sim** | [`mullet_ros_base`](https://github.com/skymule-ai/mullet_ros_base) | ARM64 ROS 2 Jazzy + CUDA base image for Jetson Orin |
| | [`sitl_builder`](https://github.com/skymule-ai/sitl_builder) | Ready-to-run PX4 SITL + Gazebo Docker image |
| | [`mullet_sitl_sim`](https://github.com/skymule-ai/mullet_sitl_sim) | Multi-vehicle PX4 SITL fleet from one YAML file |
| 🧰 **Extras** | [`mullet-mavsdk`](https://github.com/skymule-ai/mullet-mavsdk) | Python MAVSDK framework for single drones and swarms |
| | [`px4_state_machine`](https://github.com/skymule-ai/px4_state_machine) | ROS 2 PX4 offboard state machines (VTOL, quad) and fleet TF |
| 📚 **Docs** | [`mullet-wiki`](https://github.com/skymule-ai/mullet-wiki) | Stack documentation, served locally |

## 🚀 Get started

No drone needed: spin up a simulated fleet and fly it from the control center.

1. Start PX4 + Gazebo vehicles with [`mullet_sitl_sim`](https://github.com/skymule-ai/mullet_sitl_sim).
2. Open the operator UI from [`mullet-paddock`](https://github.com/skymule-ai/mullet-paddock).
3. Read how the pieces fit in [`mullet-wiki`](https://github.com/skymule-ai/mullet-wiki).

---

<p align="center">
  <sub>Built by SkyMule · issues and pull requests welcome in any repo</sub>
</p>
