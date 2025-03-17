---
tags:
  - Wireless_Communication
---
# 1. Propagation Mechanisms
## 1.1 Free Space Attenuation
a TX and an RX antenna in **free space**
received power as a function of **LoS propagation distance** and transmit power

> [!NOTE] [[Friis' Law]]
> $P_{RX}(d)=P_{TX}G_{TX}G_{RX}\left( \frac{\lambda}{4\pi d} \right)^2$
> $\left( \frac{\lambda}{4\pi d} \right)^2$: free space loss factor
> 
> on logarithmic scale(dB)
> $P_{RX|dBm}(d)=P_{TX|dBm}+G_{TX|dB}+G_{RX|dB}+20\log\left( \frac{\lambda}{4\pi d} \right)$
 Friis’ law cannot hold for arbitrarily small d(in the [[Far field(Fraunhofer region)]])


> [!NOTE] [[The $d^4$ Power Law]]
> 

## 1.2 Reflection and transmission
> [!NOTE] [[Snell's Law]]
> 

## 1.3 Diffraction
![[diffraction.png]]
$$
\theta_{d}=\arctan\left( \frac{{h_{s}-h_{Tx}}}{d_{Tx}} \right)+\arctan\left( \frac{h_{s}-h_{Rx}}{d_{{Rx}}} \right)
$$
$$
E_{total}(x)=e^{-jk_{0}x}\left( \frac{1}{2}-\frac{e^{j\pi/4}}{\sqrt{2}}F(\upsilon_{F}) \right)
$$
$$
F(\upsilon_{F})=\int_{0}^{\upsilon_{F}}e^{-j\pi t^2/2}dt
$$
$$
\upsilon_{F}=\theta_{d}\sqrt{ \frac{{2d_{Tx}d_{Rx}}}{\lambda(d_{Tx}+d_{Rx})} }
$$
Bullington’s Method: replaces the multiple screens by a single, “equivalent” screen.
![[Bullington’s Method.png]]

## 1.4 Scattering
![[Scattering.png]]
## 1.5 Waveguiding
lower propagation exponent $n$
lower path loss along certain street corridors
higher power along the street

## 1.6 Deterministic Channel Modeling
Due to issues of computational complexity, it is common to use the high-frequency approximation (also known as ray approximation) for the computation. In this approximation, electromagnetic waves are modeled as rays that follow the laws of geometrical optics (Snell’s laws for reflection and transmission); further refinements allow inclusion of diffraction and diffuse scattering in an approximate way. 

The goal is then to find the characteristics of each MPC, namely
 - amplitude, phase shift 
 - delay(or equivalently, the pathlength the MPC covers)
 - DoP(direction of departure from the TX)
 - DoA(direction of arrival at the RX)
 - polarization

The characteristics of all of these MPCs constitute a complete description of the channel. It can be converted to the double-directional impulse response $h_{l}(t,\overrightarrow{r_{Tx}},\overrightarrow{r_{Rx}}, \tau, \Omega, \Psi)=|\alpha_{l}|e^{j\phi_{l}}\delta(\tau-\tau_{l})\delta(\Phi-\Phi_{l})\delta(\Psi-\Psi_{l})$

### 1.6.1 Ray Launching
In the ray-launching (aka shoot-and-bounce) approach, the transmit antenna sends out (launches) rays into different directions.

The algorithm follows the propagation of each ray until it either 
- hits the RX
- becomes too weak to be significant (e.g., drops belowthe noise level)

When following a ray, a number of effects have to be taken into account:
- Free space attenuation
- Reflections change the direction of a ray and cause an additional attenuation
- Diffraction and diffuse scattering are included in more advanced models

### 1.6.2 Ray Tracing
Classical ray tracing determines all rays that can go from one TX location to one RX location. The method operates in two steps:

- First, all rays that can transfer energy from the TX location to the RX location are determined. 
- In a second step, attenuations (due to free space propagation and finite reflection coefficients) are computed

### 1.6.3 Geographical Databases
The foundation of all deterministic methods is the information about the geography and morphology of the environment.

# 2. Statistical Description of the Wireless Channel
However, in many circumstances, it is too **complicated**, and not necessary, to describe all reflection, diffraction, and scattering processes that determine the different Multi-Path Components (MPCs).

Rather, it is preferable to describe the **statistics** of the propagation channel, e.g., the probability that a channel parameter attains a certain value, without worrying at exactly what location this parameter is attained.

The most important parameter is **channel gain**, as it determines received power or field strength; it will be at the center of our interest in this chapter.

![[Types of received power variations..png]]
## 2.1 [[Small-Scale Fading]]
1. The Time-Invariant Two-Path Model:
we consider the simplest possible case – two MPCs whose properties do not change with time.
If the runlength between TX and RX is $d$, the received signal can be described as:
$$
E(t)=E_{0}\cos(2\pi f_{c}t-k_{0}d)
$$
where $k_{0}$ is the wavenumber $\frac{2\pi}{\lambda}$, and $E_{0}$ is the amplitude at the RX. Using complex baseband notation($s_{BP}(t)=\mathrm{Re}\left\{ s_{LP}(t)e^{j2\pi f_{c}t} \right\}$)
$$
E=E_{0}e^{-jk_{0}d}
$$
Now consider the case that the transmit signal gets to the RX via two different propagation paths, created by two different Interacting Objects (IOs)
$$
E(\vec{r})=E_{1}e^{-j \vec{k_{1}}\vec{r}}+E_{2}e^{-j \vec{k_{2}}\vec{r}}
$$
where $\vec{k_{1}}$ is the wave vector (i.e., has the absolute magnitude $k_{0}$, and is pointing into the direction of propagation) of wave 1. Note that due to our assumptions, the location vector $\vec{r}$ impacts the phase, but not the amplitude, of each of the two MPCs.
2. The Time-Variant Two-Path Model
In general, the runtime (path length) difference between the different propagation paths changes with time. This change can be due to movements of the TX, the RX, the IOs, or any combination thereof; to simplify discussion, we henceforth assume only movement of the RX.

The movement of the RX also leads to a shift of the received frequency, called the Doppler shift. If the RX moves away from the TX with speed v, then the distance d between TX and RX increases with that speed.
$$
E(t)=E_{0}\cos(2\pi f_{c}t-k_{0}[d_{0}+vt])=E_{0}\cos\left( 2\pi t\left[ f_{c}-\frac{v}{\lambda}-k_{0}d_{0} \right] \right)
$$
the Doppler shift is given by:
$$
\upsilon =-\frac{v}{\lambda}\cos(\gamma)=-\frac{f_{c}v}{c_{0}}\cos(\gamma)
$$
Different MPCs have different Doppler shifts. This leads to a **Doppler spreading**, i.e., **frequency dispersion**.

The superposition of several Doppler-shifted waves creates the sequence of fading dips. Again, this can be demonstrated using the two-path model. As the RX moves, it receives two waves that are each Doppler shifted, but by different amounts.

Summarizing, we can obtain the fading rate in the two-path model by two equivalent considerations:
1. We superimpose two incident waves, plot the resulting interference pattern (field strength “mountains and valleys”), and count the number of fading dips per second that an RX sees when moving through that pattern.
2. Alternatively, we can think of superimposing two signals with different Doppler shifts at the receive antenna, and determine the fading rate from the beat frequency – i.e., the difference of the Doppler shifts of the two waves.
### 2.1.1 Small-Scale Fading Without a Dominant Component
we now investigate a more general case of multipath propagation. We consider a radio channel with many IOs and a moving RX.
![[Rayleigh fading channel.png]]![[Pdf of rayleigh channel.png]]
Properties of the [[Rayleigh Distribution]]
$$
\begin{align}
 & \text{Mean value} & \bar{r}=\sigma \sqrt{ \frac{\pi}{2} } \\
 & \text{Mean square value} & \bar{r^2}=r^2_{{rms}}=2\sigma^2 \\ \\
 & \text{Variance} & \bar{r^2}-(\bar{r}^2 )=2\sigma^2-\frac{\pi}{2}\sigma \\
 & \text{Median value} & r_{50}=1.18\sigma \\
 & \text{Variance} & \sigma^2
\end{align}
$$
$$
pdf(r)=\frac{1}{\sqrt{ 2\pi }\sigma}e^{(-r^2/2\sigma^2)}
$$
$$
cdf(r)=1-e^{(-r^2/2\sigma^2)}=1-e^{(P_{min}/\bar{P})}
$$
Fading Margin: $M=\frac{r_{rms}^2}{r_{min}^2}$

The task is therefore to answer the following question: “Given a minimum receive power required for successful communications, how large does the mean power have to be in order to ensure that communication fails in no more than $x\%$ of all situations?” 
In other words, how large does the fading margin have to be?

The cdf gives by definition the probability that a certain field strength level is not exceeded. In order to achieve an x% outage probability, it follows that:
$$
x=cdf(P_{min})\approx \frac{P_{min}}{\bar{P}}
$$
$$
\bar{P}=2\sigma^2
$$
### 2.1.2 Small-Scale Fading with a Dominant Component
Fading statistics change when a dominant MPC – e.g., a LOS component or a dominant specular component – is present.

![[Small-Scale Fading with a Dominant Component.png]]It is clear that the probability of deep fades is much smaller than in the Rayleigh-fading case. The stronger the LOS component, the rarer the occurrence of deep fades.

$$
pdf_{r}(r)=\frac{r}{\sigma^2}e^{[-{r^2+A^2}/2\sigma^2]}I_{0}\left( \frac{{rA}}{\sigma^2} \right)
$$
$$
cdf(r)=1-Q_{M}\left( \frac{A}{\sigma}, {\frac{r_{min}}{\sigma}} \right)
$$
$I_{0}(x)$ is the modified Bessel function of the first kind, zero order. $A$ is the amplitude of the dominant component.
$$
\bar{r^2}=2\sigma^2+A^2
$$
The ratio of the power in the LOS component $A$ to the power in the diffuse component $2\sigma^2$, $\frac{A^2}{2\sigma^2}$, is called the Rice factor $K_{r}$

For $K_{r}\to0$, the [[Rice Distribution]] becomes a Rayleigh distribution, while for large $K_{r}$ it approximates a Gaussian distribution with mean value $A$
![[Rice distribution for three different.png]]

### 2.1.3 [[Doppler Spectra]] and Statistics of Temporal Channel Variations
If the UE is moving, then different directions of the MPCs arriving at the UE give rise to different frequency shifts. This leads to a broadening of the received spectrum. The goal of this section is to derive this spectrum

the Doppler effect leads to a shift of the received frequency $f$ by the amount $\upsilon$, so that the received frequency is given by:
$$
f=f_{c}+\upsilon=f_{c}\left[ 1-\frac{v}{c_{0}}\cos(\gamma) \right]
$$
Obviously, the frequency shift depends on the direction of the wave, and must lie in the range $f_{c} − \upsilon_{max}\dots f_{c} + \upsilon_{max}$, where $\upsilon_{max}= f_{c}\frac{v}{c}$.

If there are multiple MPCs, we need to know the distribution of power of the incident waves as a function of $\gamma$.  As we are interested in the statistical distribution of the received signal, we consider the pdf of the received power.
we call it the pdf of the incident waves $pdf_{\gamma}(\gamma)$.  It describes the power density coming from the angular range $[\gamma,\gamma+d\gamma]$, which depends both on the density of MPCs (how many MPCs per unit angle) and the powers of those MPCs.

A very popular model for the angular spectrum at the UE is that the waves are incident uniformly from all azimuthal directions, and all arrive in the horizontal plane, so that:
$$
pdf_{\gamma}(\gamma)=\frac{1}{2\pi} \text{ for } -\pi<\gamma\leq \pi 
$$
This situation corresponds to the case when there is no LOS connection, and a large number of IOs are distributed uniformly around the UE.
Assuming furthermore that the antenna is a vertical short dipole, with an antenna pattern $G(\gamma) = 1.5$, the Doppler spectrum becomes
$$
S_{D}(\upsilon)={\frac{1.5\bar{\Omega}}{\pi \sqrt{ \upsilon_{max}^2-\upsilon^2 }}}
$$
![[Jakes Doppler spectrum..png]]
This spectrum, known as the classical or Jakes spectrum, is depicted in Figure 5.23. It has the characteristic “bathtub” shape

### 2.1.4 Temporal Fading Characterization

#### 2.1.4.1 [[Level Crossing Rate (LCR)]]
The Doppler spectrum is a complete characterization of the temporal statistics of fading. 

However, it is often desirable to have a different formulation that allows more direct insights into system behavior. A quantity that allows immediate interpretation is the occurrence rate of fading dips – this occurrence rate is known as the [[Level Crossing Rate (LCR)]].

Obviously, it depends on which level we are considering (i.e., how a fading dip is defined): falling below a level that is 30 dB below the mean happens more rarely than falling 3 dB below this mean. As the admissible depth of fading dips depends on the mean-field strength, as well as on the considered system, we want to derive the LCR for arbitrary levels (i.e., depth of fading dips).

Providing a mathematical formulation, the LCR is defined as the expected value of the rate at which the received field strength crosses a certain level r in the positive direction. This can also be written as:
$$
N_{R}(r)=\sqrt{ \frac{{\Omega_{2}}}{\pi\Omega_{0}}} \frac{{r}}{\sqrt{ 2\Omega_{0} }}e^{(-{r^2}/2\Omega_{0})}
$$
Note that $2\Omega_{0}$ is the root-mean-square value of amplitude.

#### 2.1.4.2 [[Average Duration of Fades(ADF)]]
Another parameter of interest is the Average Duration of Fades (ADF). 

In the previous sections, we have already derived the rate at which the field strength goes below the considered threshold (i.e., the LCR), and the total percentage of time the field strength is lower than this threshold (i.e., the cdf of the field strength).

The ADFs can be simply computed as the quotient of these two quantities:
$$
ADF(r)=\frac{{cdf_{r}(r)}}{N_{R}(r)}
$$
## 2.2 [[Large-Scale Fading]]
[[Small-Scale Fading]], created by the superposition of different MPCs, changes rapidly over the spatial scale of a few wavelengths. If the field strength is averaged over a small area (e.g., ten by ten wavelengths), we obtain the Small Scale Averaged (SSA) field strength. In the previous sections, we treated the SSA field strength as a constant.

However, as explained in the introduction, it varies when considered on **a larger spatial scale**, due to **shadowing** of the MPCs by IOs.

Many experimental investigations have shown that the SSA field strength $F$, plotted on a logarithmic scale, shows a [[Gaussian Distribution]] around a mean $\mu$. Such a distribution is known as lognormal, and its pdf is given by:
$$
pdf_{F}(F)=\frac{{\frac{20}{\ln(10)}}}{F\sigma_{F}\sqrt{ 2\pi }}\exp \left[ -{\frac{(20\log_{10}(F)-\mu_{{F,dB}})^2}{2\sigma_{F}^2}} \right] 
$$
where $\sigma_{F}$ is the standard deviation of F, and $\mu_{F,dB}$ is the mean of the values of F expressed in dB.

Also, power is distributed lognormally. However, there is an important fine point: when fitting the logarithm of SSA power to a normal distribution, we find that the median value of this distribution,$\mu_{P,dB}$, is related to the median of the field strength distribution $\mu_{F,dB}$ as $\mu_{P,dB}=\mu_{P,dB}+10\log_{10}\left( \frac{4}{\pi} \right)$ if the small-scale fading is Rayleigh. The pdf for the power thus reads

$$
pdf_{P}(P)=\frac{{\frac{10}{\ln(10)}}}{P\sigma_{P}\sqrt{ 2\pi }}\exp \left[-{\frac{(10\log_{10}(P)-\mu_{{P,dB}})^2}{2\sigma_{P}^2}} \right] 
$$
where $\sigma_{P}=\sigma_{F}$. Typical values of σF are $4-10dB$.
$$
P_{SSA}=\frac{1}{N+1}\sum_{x=i-\frac{N}{2}}^{i+\frac{N}{2}}|RxSignal_{amp}|^2
$$

$$
P|_{LSF, dB}=P_{SSA}-\bar{P}(d)
$$
Where $\bar{P}(d)$ is the pass loss $\bar{P(d)}=P(d_{0})-10n\log_{10}\left( \frac{d}{d_{9}} \right)$

The lognormal variations of $F$ have commonly been attributed to shadowing effects.
![[Shadowing by a building.png]]

# 3 Channel Characterization

The impact of multi-path propagation in wideband systems can be interpreted in two different ways: 
- (i) the transfer function of the channel varies over the bandwidth of interest (this is called the **[[Frequency Selectivity]]** of the channel)
- (ii) the impulse response of the channel is not a delta function; in other words, the arriving signal has a longer duration than the transmitted signal (this is called **[[Delay Dispersion]]**). 
These two interpretations are equivalent, as can be shown by performing Fourier transformations between the delay domain and the frequency domain.

Systems operating in **wideband channels** have some important properties:
- They suffer from [[Inter Symbol Interference (ISI)]]. This can be most easily understood from the interpretation of [[Delay Dispersion]]. If we transmit a symbol of length $T_{s}$, the arriving signal corresponding to that symbol has a longer duration, and therefore interferes with the subsequent symbol.
- They can reduce the detrimental effect of fading. This effect can be most easily understood in the frequency domain: even if some part of the transmit spectrum is strongly attenuated, there are other frequencies that do not suffer from attenuation. Appropriate coding and signal processing can exploit this fact

## 3.1 Characterization of Deterministic Linear Time-Invariant Systems

the scenario is static, so that neither TX, RX, nor IOs move.

First, consider the situation in the frequency domain. At a given frequency the (complex) MPCs add up coherently, i.e., according to their phases. For the case that there are many MPCs and none of them are dominant, the transfer function can be interpreted as a realization of **Rayleigh fading**, adding up the different MPC amplitudes with random complex weights

$$
H(f)=\sum_{l}|a_{l}|e^{j\phi_{l}}e^{-j 2\pi f\tau_{l}}
$$

How strict must this “single ellipse” condition be fulfilled so that the channel is still “effectively” nondispersive? The answer depends on the system bandwidth. 

We now draw the ellipses that are defined by their focal points – TX and RX – and the eccentricity determining the runtime. All rays that undergo a single interaction with an object on a specific ellipse arrive at the RX at the same time. Signals that interact with objects on different ellipses arrive at different times. Thus, the channels are delay-dispersive if the IOs in the environment are not all located on a single ellipse.

An RX with bandwidth W cannot distinguish between echoes arriving at $\tau$ and $\tau+\Delta \tau$, if $\Delta \tau\ll \frac{1}{W}$(for many qualitative considerations, it is sufficient to consider the above condition with $\Delta \tau=\frac{1}{W}$). Thus echoes that are reflected in the donut-shaped region corresponding to runtimes between τ and $\tau+\Delta \tau$ arrive at “effectively” the same time
![[Scatterers located on the same ellipses lead to the same delays.png]]
The above considerations also lead us to a mathematical formulation for narrowband and wideband from a time domain point of view: a system is narrowband if the inverse of the system bandwidth 1/W is much larger than the maximum excess delay $\tau_{max}$. In that case, all echoes fall into a single delay bin, and the amplitude of this delay bin is $\alpha(t)$. A system is wideband in all other cases.

![[Narrowband and wideband systems.png]]

## 3.2 Characterization of Deterministic Linear Time-Variant Systems

a wireless channel can be described by an impulse response; it thus can be interpreted as a
linear filter. In general, however, wireless channels are time variant, with an [[Impulse Response]] $h(t,\tau)$ that changes with time; we have to distinguish between the absolute time $t$ and the delay $\tau$. Thus, the theory of the Linear Time-Variant (LTV) system must be used.

An intuitive interpretation is possible if the impulse response changes only slowly with time – more exactly, the duration of the impulse response (and the signal) should be much shorter than the time over which the channel changes significantly. Then we can consider the behavior of the system at one time t like that of an Linear Time-Invariant(LTI) system. Such a system is also called quasi-static.

Fourier transforming the impulse response with respect to the variable τ results in the time-variant [[Transfer Function]] $H(t,f)$:
$$
H(t,f)=\int_{-\infty}^{\infty}h(t,\tau)e^{-j 2\pi f\tau}d\tau
$$
the [[Doppler-variant Impulse Response]], better known as [[Spreading Function]] $s(\upsilon,\tau)$:
$$
s(\upsilon,\tau)=\int_{-\infty}^{\infty}h(t,\tau)e^{-j 2\pi \upsilon t}dt
$$
This function describes the spreading of the input signal in the delay and Doppler domains.

[[Doppler-variant Transfer Function]] $B(\upsilon,f)$
$$
B(\upsilon,f)=\int_{-\infty}^{\infty}s(\upsilon,\tau)e^{-j 2\pi f \tau}d\tau
$$

![[Interrelation between deterministic system functions.png]]

## 3.3The WSSUS Model

We now return to the stochastic description of wireless channels. Interpreting them as time-variant stochastic systems, a complete description requires the multi-dimensional pdf of the impulse response. 

However, this is usually much too complicated in practice. Instead, we restrict our attention to a second-order description – namely, the [[AutoCorrelation Function (ACF)]].

The ACF of a stochastic process y is defined as:
$$
R_{yy}(t,t')=E\left\{ y^*(t)y(t') \right\} 
$$
where the expectation is taken over the ensemble of possible realizations. The ACF describes the relationship between the second-order moments of the amplitude pdf of the signal $y$ at different times.

Let us now revert to the problem of giving a stochastic description of the channel. The ACF of the received signal is given by:
$$
\begin{align}
 R_{yy}(t,t') & = E\left\{ \int_{-\infty}^{\infty}x^*(t-\tau)h^*(t,\tau)d\tau \int_{-\infty}^{\infty}x(t'-\tau')h(t',\tau')d\tau' \right\}  \\
 & =\int_{-\infty}^{\infty} \int_{-\infty}^{\infty}  R_{x x}(t-\tau,t'-\tau')R_{h}(t,t',\tau,\tau')d\tau d\tau'
\end{align}
$$

i.e., a combination of the ACF of the transmit signal and the ACF of the channel:
$$
R_{h}(t,t',\tau,\tau')=E\left\{ h^*(t,\tau)h(t,\tau) \right\} 
$$
Note that the ACF of the channel depends on four variables since the underlying stochastic process is two-dimensional.

The correlation functions depend on four variables and are thus a rather complicated form for the characterization of the channel. Further assumptions about the physics of the channel can lead to a simplification of the correlation function. The most frequently used assumptions are the so-called [[Wide-Sense Stationary (WSS)]] assumption and the [[Uncorrelated Scatterers (US)]] assumption.

### 3.3.1 [[Wide-Sense Stationary (WSS)]]


> [!NOTE] [[Wide-Sense Stationary (WSS)]]
> The mathematical definition of wide-sense stationarity is that the ACF depends not on the two variables $t$, $t'$ separately, but only on their difference $t-t'$ . Consequently, second-order amplitude statistics do not change with time.
   $$R_{h}(t,t',\tau,\tau')=R_{h}(t,t+\Delta t,\tau,\tau')=R_{h}(\Delta t,\tau,\tau')$$
   Physically speaking, WSS means that the statistical properties of the channel do not change with time.
   
This must not be confused with *a static channel*, where fading realizations do not change with time. For the simple case of a flat Rayleigh-fading channel, WSS means that the mean power and the ACF do not change with time, while the instantaneous amplitude can change.

In practice, this is not possible: as the UE moves over larger distances, the mean received power changes because of shadowing and variations in path loss. Rather, WSS is typically fulfilled over an area of about 10λ diameter (compare also Figure). We can thus define quasi-stationarity over a stationarity time, i.e., a finite time interval (associated with a movement distance of the UE) over which statistics do not change noticeably.
  ![[Types of received power variations..png]]


WSS also implies that components with different Doppler shifts undergo uncorrelated fading.










