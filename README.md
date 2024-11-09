# Kerbal Space Program Transfer Example

This project demonstrates a simple approach to performing orbital transfers in **Kerbal Space Program**. It includes examples for both transferring to a satellite (direct impact) and performing interplanetary transfers using orbital mechanics equations. The calculations assume ideal conditions with **circular, coplanar orbits** for ease of understanding.

## Key Concepts

- **Transfer Orbits to Satellites**: Calculates transfer parameters to achieve direct impact with a satellite target.
- **Interplanetary Transfers**: Determines the required parameters to transition between planetary orbits.

This example is designed for educational purposes, providing an introduction to orbital transfers under simplified assumptions.

## Requirements

This script uses [KRPC](https://krpc.github.io/krpc/) as the communication interface with Kerbal Space Program. Please ensure KRPC is installed and running before executing the script.


---
# Hohmann transfer
https://orbital-mechanics.space/orbital-maneuvers/hohmann-transfer.html
<p align="center">
     <img src="https://orbital-mechanics.space/_images/hohmann-transfer-orbit.svg" width="30%">
   </p>

* $v$ is the speed of an orbiting body,
* $\mu =GM$ is the standard gravitational parameter of the primary body, assuming $M+m$ is not significantly bigger than M (which makes $v_{M}\ll v$)
* $r$  is the distance of the orbiting body from the primary focus,
* $a$ is the semi-major axis of the body's orbit.
Therefore, the delta-v (Δv) required for the Hohmann transfer can be computed as follows, under the assumption of instantaneous impulses from 1 to 2 only:

$$\Delta v_{1-2} = \sqrt{\frac{\mu}{r_1}} \left(\sqrt{\frac{2*r_2}{r1+r2}}-1\right)$$ 
*Note: This deltaV is used in transfers between Planet and Satellite*

## Angular difference
Aligment between objects:

$$\boxed{\alpha = \pi \left(1-\frac{1}{2\sqrt{2}} \sqrt{\left(\frac{r_1}{r_2}+1\right)^3} \right)}$$


<p align="center">
     <img src="https://orbital-mechanics.space/_images/interplanetary-phase-angle.svg" width="50%">
   </p>

## Current angle
Using the inner producto to get the angle between body and craft.
$$cos(\theta) = \frac{\left<U.V\right>}{\left|\left|U\right|\right|\left|\left|V\right|\right|}$$

---

# Escape angle and DeltaV for interplanetary transfer
https://orbital-mechanics.space/interplanetary-maneuvers/planetary-departure-trajectory.html

<p align="center">
     <img src="https://orbital-mechanics.space/_images/interplanetary-transfer.svg" width="100%">
   </p>


All interplanetary bodies such as comets or asteroids that approach the Kerbin, or any spacecraft we want to send to other planets, must be on a hyperbolic trajectory. Whereas a parabolic trajectory has zero velocity at infinite radius, the hyperbolic trajectory has some non-zero velocity.

<p align="center">
     <img src="https://orbital-mechanics.space/_images/interplanetary-departure.svg" width="50%">
   </p>

* The escape velocity from the parking orbit considere the deltaV from the orbit velocity of the space craft and the velocity of the planet around the Sun as $v_\infty = Δv_t$

* The escape angle from the parking orbit depends on $v_\infty$ an the orbital parameters. $r_p$ is the parking orbit radius and $\mu_{planet}$ is the gravitational pull of the body

#### 1. Semi-major Axis of the Transfer Orbit

For a Hohmann transfer between the origin and target planets (e.g., from Kerbin to Duna), the **semi-major axis** of the transfer orbit is:

$$a_t = \frac{r_{\text{origin}} + r_{\text{target}}}{2}$$

where:
- $r_{\text{origin}}$ is the radius of the origin planet’s orbit around the Sun.
- $r_{\text{target}}$ is the radius of the target planet’s orbit around the Sun.

#### 2. Specific Orbital Energy of the Transfer Orbit

The **specific orbital energy** of the transfer orbit is:

$$\epsilon_t = -\frac{\mu_{\text{Sun}}}{2 a_t}$$

where:
- $\mu_{\text{Sun}} $ is the gravitational parameter of the Sun (\( \mu = GM \), where \( G \) is the gravitational constant and \( M \) is the Sun's mass).
- $a_t $ is the semi-major axis of the transfer orbit.


#### 3. Velocity in the Origin’s Orbit Around the Sun

The orbital velocity of the origin planet in its heliocentric orbit is:

$$v_{\text{origin}} = \sqrt{\frac{\mu_{\text{Sun}}}{r_{\text{origin}}}}$$

where $ r_{\text{origin}} $ is the radius of the origin planet’s orbit around the Sun.


#### 4. Velocity in the Transfer Orbit at the Starting Point

The velocity in the transfer orbit at the radius of the origin planet's orbit is:

$$v_{\text{transfer}} = \sqrt{2 \left( \epsilon_t + \frac{\mu_{\text{Sun}}}{r_{\text{origin}}} \right)}$$

where:
- $\epsilon_t $ is the specific orbital energy of the transfer orbit.
- $\frac{\mu_{\text{Sun}}}{r_{\text{origin}}} $ represents the gravitational potential energy at the origin planet’s orbit radius.


#### 5. Excess Velocity at Infinity

The **excess velocity** \( v_{\infty} \) is the difference between the transfer orbit velocity and the origin planet's orbital velocity:

$$v_{\infty} = |v_{\text{origin}} - v_{\text{transfer}}|$$


#### 6. Velocity at Periapsis of the Hyperbolic Escape Orbit

The velocity at the **periapsis** of the hyperbolic escape orbit is:

$$v_{\text{escape}} = \sqrt{v_{\infty}^2 + \frac{2 \mu_{\text{origin}}}{r_{\text{parking}}}}$$

where:
- $v_{\infty} $ is the excess velocity at infinity.
- $\frac{2 \mu_{\text{origin}}}{r_{\text{parking}}} $ is the velocity due to the origin planet's gravity at the radius of the parking orbit.


#### 7. Delta-v for Escape

The required delta-v for escaping the origin planet is the difference between the velocity at periapsis of the hyperbolic escape orbit and the velocity in the parking orbit:

$$\Delta v_{\text{escape}} = |v_{\text{escape}} - v_{\text{parking}}|$$

where:
$v_{\text{parking}} = \sqrt{\frac{\mu_{\text{origin}}}{r_{\text{parking}}}} $ is the orbital velocity in the parking orbit.


#### 8. Eccentricity of the Escape Orbit and Escape Angle

The **eccentricity** of the hyperbolic escape orbit is:

$$e_{\text{escape}} = 1 + \frac{r_{\text{parking}} \cdot v_{\infty}^2}{\mu_{\text{origin}}}$$

The **escape angle** $\eta$ is:

$$\boxed{\eta = \cos^{-1}\left(-\frac{1}{e_{\text{escape}}}\right)}$$

where:
- $e_{\text{escape}} $ is the eccentricity of the hyperbolic escape orbit.

This escape angle, $\eta$, represents the angle between the tangential vector at periapsis and the direction of departure along the hyperbolic trajectory.
