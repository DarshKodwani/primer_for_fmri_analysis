# Math Behind MRI Relaxation and the BOLD Signal

This note summarizes the core mathematics used in MRI contrast (T1, T2, T2*) and how the BOLD fMRI signal arises from changes in transverse relaxation. It is concise but includes the key equations and practical notes.

## 1. Bloch equations (basis)

Magnetization M = (Mx, My, Mz) evolves under a static field B0 and RF fields according to the Bloch equations:

\begin{align}
\frac{dM_x}{dt} &= \gamma (\mathbf{M} \times \mathbf{B})_x - \frac{M_x}{T_2}, \\
\frac{dM_y}{dt} &= \gamma (\mathbf{M} \times \mathbf{B})_y - \frac{M_y}{T_2}, \\
\frac{dM_z}{dt} &= \gamma (\mathbf{M} \times \mathbf{B})_z - \frac{M_z - M_0}{T_1},
\end{align}

where \(\gamma\) is the gyromagnetic ratio and \(M_0\) is the equilibrium longitudinal magnetization.

Working in a rotating frame and ignoring the explicit precession term when convenient yields the simple relaxation forms below.

## 2. Longitudinal relaxation (T1)

Longitudinal recovery after an RF excitation is governed by

\[
\frac{dM_z}{dt} = -\frac{M_z - M_0}{T_1}.
\]

Solution with initial value \(M_z(0)=M_{z0}\):

\[
M_z(t) = M_0 - (M_0 - M_{z0}) e^{-t/T_1}.
\]

Common special case: after a 90° pulse (\(M_{z0}=0\))

\[
M_z(t) = M_0(1 - e^{-t/T_1}).
\]

T1 (longitudinal relaxation time) describes how quickly spins return to thermal equilibrium along the main field \(B_0\).

## 3. Transverse relaxation (T2)

The coherent transverse magnetization decays as

\[
\frac{dM_{xy}}{dt} = -\frac{M_{xy}}{T_2},
\]

with solution

\[
M_{xy}(t) = M_{xy}(0) e^{-t/T_2}.
\]

T2 (spin–spin relaxation) arises from microscopic interactions that irreversibly dephase spins.

## 4. T2* (T2-star) and field inhomogeneity

Measured transverse decay in gradient-echo sequences is faster than intrinsic T2 because of additional dephasing from static and macroscopic field inhomogeneities (\(\Delta B_0\)). Define rates:

\[
R_2 = 1/T_2, \quad R_2^* = 1/T_2^*.
\]
# Math Behind MRI Relaxation and the BOLD Signal

This note summarizes the core mathematics used in MRI contrast (T1, T2, T2*) and how the BOLD fMRI signal arises from changes in transverse relaxation. It is concise but includes the key equations and practical notes.

## 1. Bloch equations (basis)

Magnetization M = (Mx, My, Mz) evolves under a static field B0 and RF fields according to the Bloch equations:

$$
\begin{aligned}
\frac{dM_x}{dt} &= \gamma (\mathbf{M} \times \mathbf{B})_x - \frac{M_x}{T_2}, \\
\frac{dM_y}{dt} &= \gamma (\mathbf{M} \times \mathbf{B})_y - \frac{M_y}{T_2}, \\
\frac{dM_z}{dt} &= \gamma (\mathbf{M} \times \mathbf{B})_z - \frac{M_z - M_0}{T_1},
\end{aligned}
$$

where \(\gamma\) is the gyromagnetic ratio and \(M_0\) is the equilibrium longitudinal magnetization.

Working in a rotating frame and ignoring the explicit precession term when convenient yields the simple relaxation forms below.

## 2. Longitudinal relaxation (T1)

Longitudinal recovery after an RF excitation is governed by

$$
\frac{dM_z}{dt} = -\frac{M_z - M_0}{T_1}.
$$

Solution with initial value \(M_z(0)=M_{z0}\):

$$
M_z(t) = M_0 - (M_0 - M_{z0}) e^{-t/T_1}.
$$

Common special case: after a 90° pulse (\(M_{z0}=0\))

$$
M_z(t) = M_0(1 - e^{-t/T_1}).
$$

T1 (longitudinal relaxation time) describes how quickly spins return to thermal equilibrium along the main field \(B_0\).

## 3. Transverse relaxation (T2)

The coherent transverse magnetization decays as

$$
\frac{dM_{xy}}{dt} = -\frac{M_{xy}}{T_2},
$$

with solution

$$
M_{xy}(t) = M_{xy}(0) e^{-t/T_2}.
$$

T2 (spin–spin relaxation) arises from microscopic interactions that irreversibly dephase spins.

## 4. T2* (T2-star) and field inhomogeneity

Measured transverse decay in gradient-echo sequences is faster than intrinsic T2 because of additional dephasing from static and macroscopic field inhomogeneities (\(\Delta B_0\)). Define rates:

$$
R_2 = 1/T_2, \quad R_2^* = 1/T_2^*.
$$

The additive approximation is commonly used:

$$
R_2^* = R_2 + R_{2,\text{inhom}},
$$

so that the observed transverse decay is

$$
M_{xy}(t) = M_{xy}(0) e^{-t/T_2^*} = M_{xy}(0) e^{-R_2^* t}.
$$

Gradient-echo (GE) acquisitions do not refocus static inhomogeneities and therefore are T2*-weighted; spin-echo (SE) refocuses static inhomogeneity at the echo time and is closer to T2-weighted.

## 5. Simple signal equations

- Spin-echo (approximate steady-state for classic 90°–180° SE):

$$
S_{SE}(TR,TE) \propto M_0 (1 - e^{-TR/T_1}) e^{-TE/T_2}.
$$

- Gradient-echo (GRE / EPI) — steady-state dependence with flip angle \(\alpha\):

Let \(E_1 = e^{-TR/T_1}\). The steady-state transverse magnetization magnitude (small-relaxation approximation) is proportional to

$$
M_{xy}^{ss} \propto \frac{M_0 \sin\alpha\ (1 - E_1)}{1 - E_1 \cos\alpha}.
$$

The observed GRE signal at echo time TE (including T2* decay) is

$$
S_{GRE}(TR,TE,\alpha) \propto M_{xy}^{ss} \; e^{-TE/T_2^*}.
$$

In many fMRI regimes (small flip angle, TR not extremely short) one often approximates the time-series baseline signal as

$$
S(TE) \approx S_0 e^{-TE/T_2^*}.
$$

## 6. BOLD: relation between ΔR2* and percent signal change

BOLD contrast arises because deoxyhemoglobin is paramagnetic and increases local field inhomogeneity, i.e. it increases \(R_2^*\). Activation typically *decreases* local deoxyhemoglobin (more oxy-Hb) so \(R_2^*\) decreases.

If baseline rate is \(R_2^*\) and activation changes it by \(\Delta R_2^*\), then

$$
S_{act} = S_0 e^{-TE (R_2^* + \Delta R_2^*)} = S_0 e^{-TE R_2^*} e^{-TE \Delta R_2^*} = S_{base} e^{-TE \Delta R_2^*}.
$$

For small changes (\(|TE \Delta R_2^*| \ll 1\)) we linearize:

$$
\frac{\Delta S}{S} \equiv \frac{S_{act} - S_{base}}{S_{base}} \approx -TE \, \Delta R_2^*.
$$

Thus BOLD percent signal change scales approximately with echo time TE and the change in relaxation rate \(\Delta R_2^*\) (activation typically gives \(\Delta R_2^* < 0\), so \(\Delta S / S > 0\)). This is why TE is chosen near tissue \(T_2^*\) to maximize sensitivity.

## 7. Spin-echo vs gradient-echo BOLD (brief)

- Gradient-echo BOLD (GE-BOLD): sensitive to extravascular susceptibility around vessels of many sizes; very sensitive (large percent signal change) but includes contributions from large veins (reduced spatial specificity). Uses TE near T2*.
- Spin-echo BOLD (SE-BOLD): SE refocuses static inhomogeneity so large-vessel static susceptibility effects are reduced; SE-BOLD emphasizes microvascular (capillary-level) contributions and can have better spatial specificity but lower sensitivity.

Mathematically, SE-BOLD percent change relates to \(\Delta R_2\) (intrinsic transverse rate) and the SE signal decays with \(e^{-TE/T_2}\) instead of \(e^{-TE/T_2^*}\).

## 8. Typical 3T example values (approximate)

- Gray matter: \(T_1 \approx 1300\\,\\mathrm{ms}\), \(T_2 \approx 80\\,\\mathrm{ms}\), \(T_2^* \approx 30\\,\\mathrm{ms}\).
- White matter: \(T_1 \approx 800\\,\\mathrm{ms}\), \(T_2 \approx 60\\,\\mathrm{ms}\), \(T_2^* \approx 25\\,\\mathrm{ms}\).
- Typical fMRI choice: \(TE\) ≈ 25–35 ms at 3T (close to gray-matter T2*), TR commonly 0.8–3 s depending on sequence.

## 9. Further notes and extensions

- The simple linearization \(\Delta S/S \approx -TE \Delta R_2^*\) is useful for intuition and sequence optimization but omits intravascular/extravascular separation, diffusion effects, and vessel-size dependencies. More detailed biophysical models (e.g., the balloon model, or models separating intravascular/extravascular compartments) produce nonlinear relationships between neuronal activity, cerebral blood flow (CBF), cerebral blood volume (CBV), oxygen extraction fraction (OEF) and \(\Delta R_2^*\).
- At ultra-high field (7T+), T2* shortens and susceptibility effects increase; sequences, TE selection and artifact mitigation must be adjusted accordingly.

---

If you want, I can also add a short Python example that plots exponential T1/T2/T2* decays and shows expected BOLD percent-change vs TE for a chosen \(\Delta R_2^*\).
