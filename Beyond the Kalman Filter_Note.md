# Preface

>Fundation of a tracking system: filter/recrusive target state estimation

* Chap 1~4: Theory for nonlinear/non-Gaussian filtering
  * Chap 1: The problem of nonlinear/non-Gaussian filtering and its conceptual recursive Bayesian solution
  * Chap 2: Techniques for nonlinear filtering: analytic methods/numerical methods/Gaussian sum approaches/sampling methods
  * Chap 3: Partical filters
  * Chap 4: Cramer-Rao lower bounds for nonlinear filtering
* Chap 5~12: Target tracking applications
  * Chap 5: Tracking a ballistic object
  * Chap 6: Bearings-only tracking
  * Chap 7: Range-only tracking
  * Chap 8: Bistatic radar tracking using bearings and Dopplar measurements
  * Chap 9: Partical filter-based tracking technique for tracking in blind Dopplar of a radar
  * Chap 10: GMTI tracking
  * Chap 11: Partical filter-based technique for GMTI tracking
  * Chap 12: Group & extended object tracking 

# Chap 1

## Introduction

### 1. Nonlinear Filtering
* Method: The *state-space* approch to time-serise modeling
* Two models to analyze a dynamic system: 
  * a. **System model**: describing the evolution of the state with time
  * b. **Measurement model**: relating the noisy measurements to the state
* A *recursive filtering* approach: processes data sequentially; consists two stages: **Prediction & Update**
  * **Predition stage**: uses system model to predict the state pdf forward from one measurement time to next
  * **Update stage**: uses the latest measurement to modigy the prediction pdf---Bayes theorem

### 2. Model & Solution
#### State space model:
* Target state vector: $x_k\in R^{n_x}$  
* System model: $x_k=f_{k-1}(x_{k-1},v_{k-1})$, where $f_{k-1}$ is a known, possibly non-linear function of state $x_{k-1}$, $v_{k-1}$ is *process* noise sequence
* Measurement model: $z_k=h_k(x_k,w_k)$ to recursively estimate $x_k$ from measurements $z_k\in R^{n_x}$, where $h_k$ is a known, possibly non-linear function of state $x_k$, $w_k$ is *measurement* noise sequence
* Noise sequence $w_k$ and $v_k$ will be assumed to be **white**, with known pdf and mutually independent
* The initial target state is assumed to have a known pdf $p(x_0)$, independent of noise
#### The optimal Bayesian solution:
* To recursively construct the posterior pdf $p(x_k|Z_{k})$: 
1. **Prediction stage**: at time $k-1$, required pdf $p(x_{k-1}|Z_{k-1})$ is available, obtain the *prediction density* of the state via Chapman-Kolmogorov equation.
$$
\large p(x_k|Z_{k-1})=\int p(x_k|x_{k-1})p(x_{k-1}|Z_{k-1})dx_{k-1} \tag {1.1}
$$ 
>in (1.1), $p(x_k|x_{k-1},Z_{k-1})=p(x_k|x_{k-1})$ decribes a Markov process of order one. The *transitional density* $p(x_k|x_{k-1})$ is defined by system model
2. **Update stage**: at time $k$, use measurement $z_k$ to modify the *prior density* to obtain the required *posterior density* of current state.
$$
p(x_k|Z_k)=p(x_k|z_k,Z_{k-1}) \tag {1.2}\\
=\frac{p(z_k|x_k,Z_{k-1})p(x_k|Z_{k-1})}{p(z_k|Z_{k-1})}\\
=\frac{p(z_k|x_k)p(x_k|Z_{k-1})}{p(z_k|Z_{k-1})}
$$
with
$$
\large {p(z_k|Z_{k-1})=\int p(z_k|x_k)p(x_k|Z_{k-1})dx_k} \tag {1.3}
$$
>in (1.2), the *likelihood function* $p(z_k|x_k)$ is defined by measurement model 

>Recursive method given by (1.1) and (1.2) is only a conceptual solution requires the storge of entire pdf, and analytic solution of (1.2) and (1.3) is often intractable

### 3. Optimal algorithms:

#### a. The Kalman Filter
* Assumes the posterior density at every time step is Gaussian(characterized by mean and covariance)
* $p(x_{k-1}|Z_{k-1})$ is Gaussian, so $p(x_k|Z_k)$ is also Gaussian:
  * $v_{k-1}$ and $w_{k-1}$ are drawn from Gaussian densities of known parameters
  * $f_{k-1}$ is linear
  * $h_k$ is linear
  
  The two models can be written as:
  $$
  x_k=F_{k-1}x_{k-1}+v_{k-1} \tag{1.5}
  $$
  $$
  z_k=H_kx_k+w_k \tag{1.6}
  $$
  $F_{k-1}$ and $H_k$ define the linear functions, $v_{k-1}$ and $w_{k-1}$ are mutually independent zero-mean white Gaussian. with covariances $Q_{k-1}$ and $R_k$, all these parameters can be time-variant.
* using (1.1) and (1.2):
  $$
  p(x_{k-1}|Z_{k-1})=N(x_{k-1};\hat{x}_{k-1|k-1},P_{k-1|k-1})\\
  p(x_k|Z_{k-1})=N(x_k;\hat{x}_{k|k-1},P_{k|k-1})\\
  p(x_k|Z_k)=N(x_k;\hat{x}_{k|k-1},P_{k|k})
  $$
  >$N(x;m,P)$ is Gaussian density with argument x, mean m and covariance P
  $$
  \hat{x}_{k|k-1}=F_{k-1}\hat{x}_{k-1|k-1}\\
  P_{k|k-1}=Q_{k-1}+F_{k-1}P_{k-1|k-1}F^T_{k-1}\\
  \hat{x}_{k|k}=\hat{x}_{k|k-1}+K_k(z_k-H_k\hat{x}_{k|k-1})\\
  P_{k|k}=P_{k|k-1}-K_kS_kK^T_k
  $$
  Notice $S_k=H_kP_{k|k-1}H_k^T+R_k$ is the covariance of the innovation term $\nu_k=z_k-H_k\hat{x}_{k|k-1}$  
  and $K_k=P_{k|k-1}H^T_kS^{-1}_k$ is the **Kalman gain**  
  also
  $$
  P_{k|k}=[I-K_kH_k]P_{k|k-1}
  $$
