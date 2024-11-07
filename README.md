<div align="center">

# Jax Mavrik Tilt-wing Vehicle Dynamics

[Installation](#installation) •
[Quickstart](#quickstart) •
[Citations](#citations) 

</div>
 
This project provides an open-source model for the DARCoproration's subscale tilt-wing aircraft, adapted to run with JAX. It leverages aerodynamic data generated by Bechamo's tools and offers a modifiable and sharable benchmark for controls research.


## Installation
```shell
pip install -e .
```
 
## Quickstart
```python
    from jax_marik.mavrik import Mavrik
    initial_state = np.array([
        10.0, 0.0, 0.0,  # Vx, Vy, Vz
        0.0, 0.0, 0.0,   # X, Y, Z
        0.0, 0.0, 0.0,   # roll, pitch, yaw
        0.0, 0.0, 0.0,   # Vbx, Vby, Vbz
        0.0, 0.0, 0.0,   # wx, wy, wz
        0.0, 0.0, 0.0,   # dwdt_x, dwdt_y, dwdt_z
        0.0, 0.0, 0.0,   # ax, ay, az
        0.0, 0.0, 0.0,   # Fx, Fy, Fz
        0.0, 0.0, 0.0    # L, M, N
    ])

    control = np.array([
        0.0, 0.0, 0.0,  # wing_tilt, tail_tilt, aileron
        0.0, 0.0, 0.0,  # elevator, flap, rudder
        1000.0, 1000.0,  # RPM_tailLeft, RPM_tailRight
        1000.0, 1000.0,  # RPM_leftOut1, RPM_left2
        1000.0, 1000.0,  # RPM_left3, RPM_left4
        1000.0, 1000.0,  # RPM_left5, RPM_left6In
        1000.0, 1000.0,  # RPM_right7In, RPM_right8
        1000.0, 1000.0,  # RPM_right9, RPM_right10
        1000.0, 1000.0   # RPM_right11, RPM_right12Out
    ])

    mavrik = Mavrik()
    mavrik.reset(initial_state)

    num_steps = 10
    states = [initial_state]
    start_time = time.time()
    for _ in range(num_steps):
        state = mavrik.step(control)
        states.append(state)
    end_time = time.time()
    runtime = end_time - start_time
    print(f"[Iteration runtime] Tot: {runtime:.6f} seconds | Avg: {runtime / num_steps:.6f} seconds")

    print("States:", states)
```
 
## Acknowledge
This project is based on the Mavrik Tilt Wing model from [BechamoNasaModels](https://github.com/Bechamo/BechamoNasaModels).
 
## Citations
If you use this code in your research, please cite:
```bibtex
@misc{zhou2023jax,
    author = {Weichao Zhou},
    title = {Jax Mavrik Tilt-wing Vehicle Dynamics},
    year = {2024},
    publisher = {GitHub},
    journal = {GitHub repository},
    howpublished = {\url{https://github.com/zwc662/mavrik_jax}},
}
```
