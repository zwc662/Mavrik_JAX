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
    control = np.array([
        0.0, 0.0, 0.0,  # wing_tilt, tail_tilt, aileron
        0.0, 0.0, 0.0,  # elevator, flap, rudder
        7500.0, 7500.0,  # RPM_tailLeft, RPM_tailRight
        7500.0, 7500.0,  # RPM_leftOut1, RPM_left2
        7500.0, 7500.0,  # RPM_left3, RPM_left4
        7500.0, 7500.0,  # RPM_left5, RPM_left6In
        7500.0, 7500.0,  # RPM_right7In, RPM_right8
        7500.0, 7500.0,  # RPM_right9, RPM_right10
        7500.0, 7500.0   # RPM_right11, RPM_right12Out
    ])
   
    state = np.array([
        0.0000, 0.0000, 0.0000,  # VXe, VYe, VZe
        30.0000, 0, 0,  # Xe Ye Ze
        29.9269, 0, 2.0927, # u v w
        0, 0.0698, 0,   # roll, pitch, yaw 
        0.0, 0.0, 0.0,   # p, q, r
        0.0, 0.0, 0.0,   # Fx, Fy, Fz
        0.0, 0.0, 0.0    # L, M, N
    ])
 
    mavrik = Mavrik()

    num_steps = int(0.1 / 0.01)
    states = [state]
    tot_runtime = 0.0
    for i in range(num_steps):
        start_time = time.time()
        state, info = mavrik.step(state, control)
        end_time = time.time()
        runtime = end_time - start_time
        tot_runtime += runtime
        states.append(state)
        print(f">>>>>>>>>>>>>>>>>>>> Iteration: {i} <<<<<<<<<<<<<<<<<<<<<<")
        print(f"Runtime: {runtime:.6f} | Tot: {tot_runtime:.6f} seconds | Avg: {tot_runtime / num_steps:.6f} seconds | State: {state}")
    
```
 
## Acknowledge
This project is based on the Mavrik Tilt Wing model from [BechamoNasaModels](https://github.com/Bechamo/BechamoNasaModels).
 
## Citations
If you use this code in your research, please cite:
```bibtex
@misc{zhou2024jaxmavrik,
    author = {Weichao Zhou},
    title = {Jax Mavrik Tilt-wing Vehicle Dynamics},
    year = {2024},
    publisher = {GitHub},
    journal = {GitHub repository},
    howpublished = {\url{https://github.com/zwc662/MAVRIK_Tilt_Wing_VTOL_JAX}},
}
```
