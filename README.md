import streamlit as st
import numpy as np
import matplotlib.pyplot as plt

# --------------------------------------------------
# App Title and Description
# --------------------------------------------------
st.title("Exponential Speed Model")
st.subheader("Interactive Algebra 2 Exponential Growth & Decay")

st.markdown(
    """
    This app models how a car's speed changes over time using an **exponential equation**.
    
    Students can adjust the **initial speed**, **rate of change**, and **time** to see
    how exponential **growth** or **decay** behaves.
    """
)

# --------------------------------------------------
# Sidebar Controls (Student Interaction)
# --------------------------------------------------
st.sidebar.header("Model Parameters")

# Initial speed slider
initial_speed = st.sidebar.slider(
    "Initial Speed (mph)",
    min_value=30,
    max_value=120,
    value=90,
    step=5
)

# Rate of change slider (percent)
rate_percent = st.sidebar.slider(
    "Rate of Change (% per hour)",
    min_value=-20,
    max_value=20,
    value=8,
    step=1
)

# Convert percent to decimal
rate = rate_percent / 100

# Time slider
time_hours = st.sidebar.slider(
    "Time (hours)",
    min_value=0,
    max_value=24,
    value=2,
    step=1
)

# --------------------------------------------------
# Exponential Model
# --------------------------------------------------
# S(t) = S0 * (1 + r)^t

def speed_model(t, s0, r):
    return s0 * (1 + r) ** t

# Time range for graph
t = np.linspace(0, time_hours, 100)

# Calculate speeds
speeds = speed_model(t, initial_speed, rate)
final_speed = speed_model(time_hours, initial_speed, rate)

# --------------------------------------------------
# Display Results
# --------------------------------------------------
st.markdown("### Results")

st.write(
    f"After **{time_hours} hours**, the car's speed is approximately "
    f"**{final_speed:.2f} mph**."
)

# --------------------------------------------------
# Graph
# --------------------------------------------------
fig, ax = plt.subplots()
ax.plot(t, speeds)

ax.set_xlabel("Time (hours)")
ax.set_ylabel("Speed (mph)")
ax.set_title("Speed vs. Time (Exponential Model)")

st.pyplot(fig)

# --------------------------------------------------
# Interpretation Section
# --------------------------------------------------
st.markdown("### Interpretation")

if rate > 0:
    st.write(
        "- The speed is **increasing exponentially** over time.\n"
        "- This represents exponential **growth**."
    )
elif rate < 0:
    st.write(
        "- The speed is **decreasing exponentially** over time.\n"
        "- This represents exponential **decay**."
    )
else:
    st.write(
        "- The speed remains **constant** over time."
    )

# --------------------------------------------------
# Safety & Model Limitations
# --------------------------------------------------
st.markdown("### Model Limitations")

st.warning(
    "This model is **theoretical only**. Real cars cannot safely or realistically "
    "increase or decrease speed by a constant percentage over long periods of time. "
    "This app is intended for **mathematical learning purposes only**."
)

