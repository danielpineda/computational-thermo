# First Law of Thermodynamics

## Closed system

:::{figure} ../../images/piston_cylinder_cv.svg
:name: fig:cylinder-closed-cv
:alt: Cylinder with a weight and closed control volume of fluid

Closed system with mass $m_{\text{CV}}$.
:::

[](#fig:cylinder-closed-cv) shows a cylinder with a weight on top,
enclosing a fluid. We define our control volume as the interior boundary,
with fluid mass $m_{\text{CV}}$.

The first law of thermodynamics, which expresses conservation of energy,
can be expressed as

$$
\begin{align}
\frac{dE}{dt} &= \dot{E}_{\text{in}} - \dot{E}_{\text{out}} \\
\frac{dE}{dt} &= \dot{Q} - \dot{W} \;, \label{eq:first-law-rate}
\end{align}
$$

where $\frac{dE}{dt}$ is the rate of change of energy in a system,
$\dot{Q}$ is the rate of heat transfer *into* the system,
and $\dot{W}$ is the rate of work done *by* the system.
(This sign convention follows that of Rudolf Clausius; 
you might encounter alternative conventions.)

The energy of a fluid system is
$$
\label{eq:energy}
E = U + \text{KE} + \text{PE} \;,
$$
where $U$ is the total internal energy, 
$\text{KE} = \frac{1}{2} m V^2$ is the kinetic energy 
(based on a bulk velocity $V$ in some frame of reference),
and $\text{PE} = mgz$, with $m$ being the system mass, $g$ acceleration due to gravity,
and $z$ the height relative to some baseline.
We will keep PE and KE in our expressions, but these terms are often neglected
in thermodynamic analyses.

Expanding Eq. [](#eq:energy) into [](#eq:first-law-rate) and then integrating:

$$
\begin{align}
\int \left( \dot{Q} - \dot{W} \right) &= \int \left(\frac{dU}{dt} + \frac{d\text{KE}}{dt} + \frac{d\text{PE}}{dt} \right) \\
Q - W &= \Delta U + \Delta\text{KE} + \Delta\text{PE} \;,
\end{align}
$$

or, the common expression when kinetic and potential energy changes play no role:

$$
\Delta U = Q - W \;,
\label{eq:first-law}
$$
where $\Delta U = U_2 - U_1$ for a process that takes the system 
from thermodynamic state 1 to state 2.

## Internal energy

What is internal energy, $U$? This property represents the energy associated
with a system's internal state, coming from thermal, nuclear, magnetic, and/or chemical effects.
The thermal energy, or the kinetic energy of consituent molecules, depends on the molecular structure.

The intensive internal energy (i.e., per unit mass) is

$$
u = \frac{U}{m} \;,
$$

and is a thermodynamic property, a function of the system's thermodynamic state.
We must define $u = 0$ at some reference state, and while the absolute value of $u$
depends on this reference state definition, differences do not:

$$
\Delta u = u_2 - u_1 = (u_2 - u_{\text{ref}}) - (u_1 - u_{\text{ref}}) \;.
$$

So, how to we determine $u$? First, we need to understand how to 
define the thermodynamic state.

### Phase rule

The **phase rule** gives the number of degrees of freedom, 
or the internal, intensive properties needed
to fix the thermodynamic state of a system in equilibrium:

$$
\label{eq:phase-rule}
F = C - \Pi + 2 \;,
$$

where $C$ is the number of chemical species (e.g., water) and
$\Pi$ is the number of phases.

For a pure substance $C = 1$, and with a single phase $\Pi = 1$,
so $F = 2$, or any two intensive properties define the thermodynamic state.
For internal energy, this means

$$
u = f(T, p)
$$

(for example).

### Internal energy for ideal gases

In general, $u = f(T, v)$ (or any other two intensive properties).
If we take the differential:

$$
du = \left(\frac{\partial u}{\partial T}\right)_v dT + \left(\frac{\partial u}{\partial v}\right)_T dv \;.
$$

We define the specific heat at constant volume as

$$
c_v \equiv \left(\frac{\partial u}{\partial T}\right)_v \;,
$$

meaning

$$
du = c_v dT + \left(\frac{\partial u}{\partial v}\right)_T dv 
$$

for all fluids.

If a gas behaves as an **ideal gas**, then its temperature $T$, 
pressure $P$, and specific volume $v$ can be related with:

$$
\label{eq:ideal-gas-law}
P v = R T \;.
$$

The ideal gas approxmation assumes that intermolecular forces in the gas
are negligible. As a consequence, internal energy does not vary with specific volume:

$$
\left(\frac{\partial u}{\partial v}\right)_T \equiv 0
$$

for an *ideal gas only*. This approximation is most valid for gases at 
reasonably high temperatures and reasonable low pressures—near room temperature.
[](#fig:internal-energy) shows the internal energy of water vapor at 250°C, 
for a range of specific volume values. We can see that past a certain point, 
the gas begins behaving as an ideal gas with a constant $u$ for varying $v$.

:::{figure} ../../images/ideal-gas-internal-energy.svg
:name: fig:internal-energy
:alt: Plot of internal energy with specific volume for water vapor

Internal energy as a function of specific volume for water vapor at 250°C,
using Cantera's `Water()` pure fluid model.
:::

As a result, for an ideal gas, internal energy only depends on temperature:

$$
u = f(T) \;.
$$

:::{warning}
Remember that ideal gas is an approximation only—no gases truly behave as ideal gases.
But, it is a convenient model to use in some cases.
:::

Then, $du = c_v dT$, which we can integrate:

$$
u - u_{\text{ref}} = \int_{T_{\text{ref}}}^T c_v (T) dT \;.
$$

If $c_v$ is constant, then $u - u_{\text{ref}} = c_v (T - T_{\text{ref}})$,
and if $u_{\text{ref}} = 0$ at $T_{\text{ref}} = $ 0 K, then  $u = c_v T$.
However, assuming constant specific heat is not very accurate over a wide range of temperatures,
as [](#fig:specific-heat) shows, $c_v$ varies quite a bit for water vapor with temperature.

:::{figure} ../../images/ideal-gas-specific-heat.svg
:name: fig:specific-heat
:alt: Variation of water specific heat with temperature

Constant volume specific heat of water vapor as a function of temperature, at 1 atm.
:::

In practice, for ideal gases, we commonly represent specific heat using a high-order polynomial.
One popular representation is the NASA seven-coefficient polynomial {cite:p}`McBride1993`:

$$
\label{eq:nasa7}
\frac{c_p (T)}{R} = a_0 + a_1 T + a_2 T^2 + a_3 T^3 + a_4 T^4 \;,
$$
where coefficients $a_0$ through $a_4$ come from fits to experimental or computed data.
(Coefficients $a_5$ and $a_6$ are used for $h$ and $s$ polynomials, 
arising from integrating [](#eq:nasa7).)
In the field of combustion chemical kinetics, thermodynamic properties of gases are
typically modeled using two sets of these parameters, for a low and high temperature ranges.
However, current versions of NASA's chemical equilibrium solver and thermodynamic databases
actually use a nine-coefficient polynomial parameterization {cite:p}`McBride2002` and 
as many temperature ranges as needed.


## Open system

Let's now consider open systems. For simplicity, [](#open-cv) shows a system with 
one inlet and one outlet; let's assume $\dot{Q} = 0$ (no heat transfer) and the only
work being done is pressure-volume work by the flow.

:::{figure} ../../images/cv_cm_diagram.svg
:name: fig:open-cv
:alt: Open system showing control volume and control mass of fluid

Open system with one inlet and one outlet, showing mass of control volume (CV) and 
control mass (CM) at times $t$ (left) and $t + \Delta t$ (right).
:::
