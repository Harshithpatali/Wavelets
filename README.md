# Wavelets
Comparative study on Sensex forecasting using LSTM and Haar Wavelet Transform. Demonstrates how wavelet-based denoising improves financial time-series prediction accuracy and stability over baseline LSTM models.



# 🧮 Mathematical Foundation: Haar Wavelet Transform

## 1️⃣ Introduction

The **Haar Wavelet Transform** is the simplest and oldest type of wavelet transform, introduced by **Alfréd Haar (1909)**.  
It converts a time-domain signal (like stock prices) into a representation that shows **both time and frequency information**, enabling **noise reduction and trend detection**.

While the **Fourier Transform** gives frequency information but loses time localization,  
**Wavelet Transform** preserves both — making it perfect for *non-stationary financial data* such as Sensex.

---

## 2️⃣ Haar Wavelet Basics

### a) Haar Scaling and Wavelet Functions

The Haar wavelet uses two simple basis functions:

$$
\phi(t) =
\begin{cases}
1, & 0 \le t < 1 \\
0, & \text{otherwise}
\end{cases}
$$

$$
\psi(t) =
\begin{cases}
1, & 0 \le t < \frac{1}{2} \\
-1, & \frac{1}{2} \le t < 1 \\
0, & \text{otherwise}
\end{cases}
$$

Here:
- $\phi(t)$ is the **scaling function** (represents average or trend)  
- $\psi(t)$ is the **wavelet function** (represents detail or noise)

---

## 3️⃣ Discrete Haar Wavelet Transform (DWT)

For a signal $S = [s_1, s_2, s_3, s_4, \ldots]$,  
the DWT computes **average (approximation)** and **difference (detail)** coefficients as:

$$
A_i = \frac{s_{2i-1} + s_{2i}}{\sqrt{2}}
$$

$$
D_i = \frac{s_{2i-1} - s_{2i}}{\sqrt{2}}
$$

- $A_i$ → Approximation coefficients (low frequency → trend)  
- $D_i$ → Detail coefficients (high frequency → noise)

The inverse transform reconstructs the signal:
$$
s_{2i-1} = \frac{A_i + D_i}{\sqrt{2}}, \quad s_{2i} = \frac{A_i - D_i}{\sqrt{2}}
$$

---

## 4️⃣ Application in Financial Time Series

In stock data (like Sensex), high-frequency movements often represent **noise or volatility spikes**,  
while low-frequency components carry **meaningful long-term trends**.

By applying **Haar DWT**, we decompose the closing prices as:

$$
\text{Close}(t) = A_1(t) + D_1(t) + D_2(t) + \ldots + D_n(t)
$$

We can then **filter out** high-frequency components $D_k$ to denoise the data:
$$
\text{Cleaned Signal} = A_1(t)
$$

---

## 5️⃣ Why Haar for LSTM?

✅ **Advantages:**
- Computationally simple (integer operations)  
- Perfect for real-time filtering  
- Reduces overfitting by removing high-frequency noise  
- Keeps key price patterns for trend learning  

🧠 The LSTM then learns from a **smoothed, noise-reduced signal**, improving prediction accuracy and stability.

---

## 6️⃣ Visualization Example

A Haar decomposition separates the Sensex close prices into:

- **Approximation ($A_1$):** Smooth long-term price movement  
- **Detail ($D_1$):** Short-term fluctuations and market noise  

This denoised signal is fed into the Wavelet-LSTM model for superior forecasting results.

---

📘 **Summary:**  
The Haar Wavelet Transform performs multi-resolution analysis, allowing LSTM models to focus on informative long-term structures rather than noisy short-term variations — leading to improved generalization and predictive performance in financial forecasting.

