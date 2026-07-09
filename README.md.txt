import matplotlib.animation as animation
import matplotlib.pyplot as plt
import numpy as np

# 1. Engineering Parameters (Fluid Mechanics & Geometry)
Q = 10.0  # Constant volumetric flow rate (Q = A * v)
c_s = 2.5  # Constant speed of sound in this fluid medium


def nozzle_area(x):
    """Defines a converging nozzle geometry where area decreases along x."""
    return 6.0 - 0.8 * x


def fluid_velocity(x):
    """Calculates actual fluid velocity based on continuity equation: v = Q/A"""
    A = nozzle_area(x)
    return Q / A


# Theoretical Event Horizon is where v(x) == c_s
# Q / (6 - 0.8*x) = 2.5 -> 6 - 0.8*x = 4 -> 0.8*x = 2 -> x = 2.5
horizon_x = 2.5

# 2. Setup Animation Environment
fig, ax = plt.subplots(figsize=(10, 6))
ax.set_xlim(0, 5)
ax.set_ylim(0, 4)
ax.axvline(
    x=horizon_x,
    color="red",
    linestyle="--",
    linewidth=2,
    label="Sonic Event Horizon ($v = c_s$)",
)

# Initialize 8 sound waves starting at different positions (before and after horizon)
start_positions = [0.5, 1.0, 1.5, 2.0, 2.4, 2.6, 3.0, 3.5]
colors = [
    "blue",
    "blue",
    "blue",
    "blue",
    "blue",
    "black",
    "black",
    "black",
]  # Blue for escaped, Black for trapped

lines = []
wave_data = []

for idx, x_start in enumerate(start_positions):
    line, = ax.plot([], [], color=colors[idx], lw=2)
    lines.append(line)
    # Trackers for (x_history, t_history) for each of the 8 waves
    wave_data.append(([x_start], [0.0]))

# Plot styling (Professional English)
ax.set_title("Fluid Dynamic Analogue of a Black Hole (8-Wave Simulation)", fontsize=12)
ax.set_xlabel("Nozzle Axial Position ($x$)", fontsize=10)
ax.set_ylabel("Time ($t$)", fontsize=10)
ax.legend(loc="upper left")
ax.grid(True, linestyle=":", alpha=0.5)

# 3. Numerical Integration (Euler's Method) inside Animation Loop
dt = 0.02


def update(frame):
    for idx in range(8):
        x_hist, t_hist = wave_data[idx]
        current_x = x_hist[-1]
        current_t = t_hist[-1]

        # Kinematic equation: dx/dt = v(x) - c_s
        # If wave is past x=5 (out of nozzle), we stop updating it
        if current_x < 5.0 and current_x > 0.0:
            v_fluid = fluid_velocity(current_x)
            dxdt = v_fluid - c_s
            next_x = current_x + dxdt * dt
            next_t = current_t + dt

            x_hist.append(next_x)
            t_hist.append(next_t)

        # Update the visual line on the plot
        lines[idx].set_data(x_hist, t_hist)

    return lines


# 4. Run the interactive animation
# frames=200 determines how long the simulation runs
ani = animation.FuncAnimation(
    fig, update, frames=250, interval=30, blit=True, repeat=False
)
plt.show()