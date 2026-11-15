# Dipoles and Oscillating Dipoles

[TOC]

## Conventions and scope

This note uses SI units in vacuum,

$$
c=\frac{1}{\sqrt{\mu _0\varepsilon _0}},
\qquad
\eta _0=\sqrt{\frac{\mu _0}{\varepsilon _0}}=\mu _0c,
$$

and focuses on an electric dipole whose size $a$ is small compared with both the observation distance and, when it oscillates, the reduced wavelength:

$$
r\gg a,
\qquad
ka=\frac{\omega a}{c}\ll1.
$$

For harmonic quantities the convention is

$$
\mathbf p(t)=\operatorname{Re}\!\left[\mathbf p_0e^{-i\omega t}\right].
$$

Consequently an outgoing retarded wave has spatial factor $e^{ikr}$, where $k=\omega/c$. The symbol $\mathbf n=\mathbf r/r$ denotes the direction from the dipole to the observation point, and brackets $[\;]_{t_r}$ mean evaluation at the retarded time $t_r=t-r/c$.

## Dipole quantities at a glance

| Property | Electric dipole | Magnetic dipole |
|---|---|---|
| Moment of a small two-pole source | $\mathbf p=q\mathbf d$, from $-q$ to $+q$ | $\mathbf m=I\mathbf A$, with direction fixed by the right-hand rule |
| Moment of a localized continuous source | $\displaystyle \mathbf p=\int \mathbf r'\rho(\mathbf r')\,\mathrm d^3r'$ | $\displaystyle \mathbf m=\frac12\int \mathbf r'\times\mathbf J(\mathbf r')\,\mathrm d^3r'$ |
| SI unit | $\mathrm{C\,m}$ | $\mathrm{A\,m^2}$ |
| Static interaction energy in an applied field | $U=-\mathbf p\cdot\mathbf E$ | $U=-\mathbf m\cdot\mathbf B$ |
| Static torque | $\boldsymbol\tau=\mathbf p\times\mathbf E$ | $\boldsymbol\tau=\mathbf m\times\mathbf B$ |
| Static force in a curl-free, nonuniform field | $\mathbf F=\nabla(\mathbf p\cdot\mathbf E)$ | $\mathbf F=\nabla(\mathbf m\cdot\mathbf B)$ |
| Far static field | $\displaystyle \mathbf E=\frac{3\mathbf n(\mathbf n\cdot\mathbf p)-\mathbf p}{4\pi\varepsilon _0r^3}$ | $\displaystyle \mathbf B=\frac{\mu _0}{4\pi r^3}\left[3\mathbf n(\mathbf n\cdot\mathbf m)-\mathbf m\right]$ |

The magnetic formula is the exterior field of a localized current loop; its contact term at the source is not displayed. The remainder of this note treats the electric dipole.

## Static electric dipole

### Definition and origin dependence

For charges $q_a$ at positions $\mathbf r_a$,

$$
Q=\sum_aq_a,
\qquad
\mathbf p=\sum_aq_a\mathbf r_a.
$$

Under a shift of origin by $\mathbf a$, so that $\mathbf r'_a=\mathbf r_a-\mathbf a$,

$$
\mathbf p'=\sum_aq_a(\mathbf r_a-\mathbf a)
=\mathbf p-Q\mathbf a.
$$

Thus the dipole moment of a neutral system is independent of the origin. For a pair $+q$ and $-q$ separated by the vector $\mathbf d$ pointing from the negative to the positive charge,

$$
\boxed{\mathbf p=q\mathbf d.}
$$

### Potential and field: derivation

The potential of a localized charge distribution is

$$
\phi(\mathbf r)
=\frac{1}{4\pi\varepsilon _0}
\int\frac{\rho(\mathbf r')}{|\mathbf r-\mathbf r'|}\,\mathrm d^3r'.
$$

For $r\gg r'$, the first two terms of the multipole expansion are

$$
\frac{1}{|\mathbf r-\mathbf r'|}
=\frac1r+\frac{\mathbf n\cdot\mathbf r'}{r^2}
+O\!\left(\frac{r'^2}{r^3}\right).
$$

Therefore

$$
\phi(\mathbf r)
=\frac{1}{4\pi\varepsilon _0}
\left(\frac Qr+\frac{\mathbf p\cdot\mathbf n}{r^2}+\cdots\right).
$$

For a neutral source, the monopole term vanishes and

$$
\boxed{
\phi_{\mathrm{dip}}(\mathbf r)
=\frac{\mathbf p\cdot\mathbf n}{4\pi\varepsilon _0r^2}
=\frac{\mathbf p\cdot\mathbf r}{4\pi\varepsilon _0r^3}.
}
$$

Using $\mathbf E=-\nabla\phi$ and differentiating $r_i/r^3$ gives

$$
\partial_j\!\left(\frac{r_i}{r^3}\right)
=\frac{\delta_{ij}-3n_in_j}{r^3}.
$$

Hence, away from the source,

$$
\boxed{
\mathbf E_{\mathrm{dip}}(\mathbf r)
=\frac{1}{4\pi\varepsilon _0r^3}
\left[3\mathbf n(\mathbf n\cdot\mathbf p)-\mathbf p\right].
}
$$

For $\mathbf p=p\,\hat{\mathbf z}$,

$$
E_r=\frac{2p\cos\theta}{4\pi\varepsilon _0r^3},
\qquad
E_\theta=\frac{p\sin\theta}{4\pi\varepsilon _0r^3},
\qquad
E_\phi=0.
$$

The field falls as $r^{-3}$, whereas a monopole field falls as $r^{-2}$.

### Energy, torque, and force

The work required to rotate a permanent dipole through $\mathrm d\boldsymbol\theta$ is $\mathrm dU=-\boldsymbol\tau\cdot\mathrm d\boldsymbol\theta$. This gives

$$
\boxed{U=-\mathbf p\cdot\mathbf E,}
\qquad
\boxed{\boldsymbol\tau=\mathbf p\times\mathbf E.}
$$

In a slowly varying electrostatic field,

$$
\boxed{
\mathbf F=\nabla(\mathbf p\cdot\mathbf E)
=(\mathbf p\cdot\nabla)\mathbf E,
}
$$

where the second equality uses $\nabla\times\mathbf E=0$ and assumes that $\mathbf p$ is spatially fixed. A freely rotating dipole tends to align with the field and move toward stronger field magnitude.

For an induced linear dipole $\mathbf p=\alpha\mathbf E$, the field does work while building the moment. Its potential energy contains an important factor of one half:

$$
U_{\mathrm{ind}}
=-\int_{\mathbf 0}^{\mathbf E}\mathbf p(\mathbf E')\cdot\mathrm d\mathbf E'
=-\frac12\alpha E^2,
\qquad
\mathbf F=\frac12\alpha\nabla E^2
$$

for a real, isotropic static polarizability $\alpha$.

### Dipole-dipole interaction

Let $\mathbf R=R\mathbf n$ point from $\mathbf p_1$ to $\mathbf p_2$. Substitution of the field of dipole 1 into $U=-\mathbf p_2\cdot\mathbf E_1$ gives

$$
\boxed{
U_{12}
=\frac{1}{4\pi\varepsilon _0R^3}
\left[
\mathbf p_1\cdot\mathbf p_2
-3(\mathbf p_1\cdot\mathbf n)(\mathbf p_2\cdot\mathbf n)
\right].
}
$$

Taking $\mathbf F_2=-\nabla_{\mathbf R}U_{12}$ yields

$$
\boxed{
\mathbf F_2
=\frac{3}{4\pi\varepsilon _0R^4}
\left[
(\mathbf p_1\cdot\mathbf n)\mathbf p_2
+(\mathbf p_2\cdot\mathbf n)\mathbf p_1
+(\mathbf p_1\cdot\mathbf p_2)\mathbf n
-5(\mathbf p_1\cdot\mathbf n)(\mathbf p_2\cdot\mathbf n)\mathbf n
\right].
}
$$

Parallel dipoles are attractive in the head-to-tail configuration and repulsive when they are parallel side by side.

### Polarized matter

If $\mathbf P(\mathbf r)$ is the electric dipole moment per unit volume, a small volume has moment $\mathrm d\mathbf p=\mathbf P\,\mathrm d^3r$. Integration by parts in the potential of this dipole distribution identifies the bound charges:

$$
\boxed{\rho_b=-\nabla\cdot\mathbf P,}
\qquad
\boxed{\sigma_b=\mathbf P\cdot\hat{\mathbf n}.}
$$

Uniform polarization therefore produces no bound volume charge, but it generally produces bound surface charge.

## Time-dependent point-dipole fields

### Retarded potentials

For a localized neutral source at the origin, charge conservation relates its total current to its dipole moment:

$$
\int\mathbf J(\mathbf r,t)\,\mathrm d^3r
=\frac{\mathrm d}{\mathrm dt}\int\mathbf r\rho(\mathbf r,t)\,\mathrm d^3r
=\dot{\mathbf p}(t).
$$

Indeed, in components,

$$
\int J_i\,\mathrm d^3r
=\int\partial_j(r_iJ_j)\,\mathrm d^3r
-\int r_i\partial_jJ_j\,\mathrm d^3r
=\int r_i\dot\rho\,\mathrm d^3r,
$$

where the surface term vanishes for a localized current and $\dot\rho+\nabla\cdot\mathbf J=0$ was used.

To electric-dipole order, the Lorenz-gauge retarded potentials are

$$
\boxed{
\phi(\mathbf r,t)
=\frac{1}{4\pi\varepsilon _0}
\left[
\frac{\mathbf n\cdot\mathbf p}{r^2}
+\frac{\mathbf n\cdot\dot{\mathbf p}}{cr}
\right]_{t_r},
}
$$

$$
\boxed{
\mathbf A(\mathbf r,t)
=\frac{\mu _0}{4\pi r}
[\dot{\mathbf p}]_{t_r}.
}
$$

The $r^{-1}$ term in $\phi$ is required by retardation and the Lorenz-gauge condition; it must not be discarded when deriving the fields.

### Exact fields in the point-dipole approximation

Apply

$$
\mathbf E=-\nabla\phi-\frac{\partial\mathbf A}{\partial t},
\qquad
\mathbf B=\nabla\times\mathbf A,
\qquad
\nabla t_r=-\frac{\mathbf n}{c}.
$$

After differentiating both the powers of $r$ and the retarded time,

$$
\boxed{
\begin{aligned}
\mathbf E(\mathbf r,t)
=\frac{1}{4\pi\varepsilon _0}
\Bigg\{&
\frac{3\mathbf n(\mathbf n\cdot\mathbf p)-\mathbf p}{r^3}
+\frac{3\mathbf n(\mathbf n\cdot\dot{\mathbf p})-\dot{\mathbf p}}{cr^2}\\
&+\frac{\mathbf n\times(\mathbf n\times\ddot{\mathbf p})}{c^2r}
\Bigg\}_{t_r},
\end{aligned}
}
$$

$$
\boxed{
\mathbf B(\mathbf r,t)
=\frac{\mu _0}{4\pi}
\left[
\frac{\dot{\mathbf p}\times\mathbf n}{r^2}
+\frac{\ddot{\mathbf p}\times\mathbf n}{cr}
\right]_{t_r}.
}
$$

These expressions contain the near, induction, and radiation fields without assuming $kr\gg1$. They are exact outside the source only within the ideal point-dipole approximation $a/r\to0$ and $ka\to0$.

### Field terms and physical regimes

For a harmonic dipole, each time derivative contributes a factor of order $\omega$. Relative to the electrostatic field, the three electric-field terms therefore scale as $1:kr:(kr)^2$.

| Region | Condition | Dominant field behavior | Geometry and energy flow |
|---|---|---|---|
| Quasistatic near zone | $a\ll r\ll k^{-1}$ | $E\sim p/(\varepsilon _0r^3)$; $B\sim\mu _0\omega p/r^2$ | Field resembles a static dipole; energy is mainly stored and returned to the source |
| Induction zone | $kr\sim1$ | $r^{-3}$, $r^{-2}$, and $r^{-1}$ terms are comparable | Electric and magnetic fields need not be in phase; radial and reactive power flow coexist |
| Radiation or far zone | $r\gg k^{-1}$ and $r\gg a$ | $E,B\sim r^{-1}$ | Fields are transverse and in phase; finite outward power survives as $r\to\infty$ |

The boundary scale is the reduced wavelength $k^{-1}=\lambda/(2\pi)$; statements using $r\ll\lambda$ or $r\gg\lambda$ are looser versions of the same classification.

## Harmonic dipole

### Phasor fields

Let $\mathbf p(t)=\operatorname{Re}[\mathbf p_0e^{-i\omega t}]$. Replacing $\dot{\mathbf p}$ by $-i\omega\mathbf p_0$ and $\ddot{\mathbf p}$ by $-\omega^2\mathbf p_0$ gives

$$
\boxed{
\begin{aligned}
\widetilde{\mathbf E}(\mathbf r)
=\frac{e^{ikr}}{4\pi\varepsilon _0}
\Bigg[&
\left(\frac1{r^3}-\frac{ik}{r^2}\right)
\left(3\mathbf n(\mathbf n\cdot\mathbf p_0)-\mathbf p_0\right)\\
&+\frac{k^2}{r}
\mathbf n\times(\mathbf p_0\times\mathbf n)
\Bigg],
\end{aligned}
}
$$

$$
\boxed{
\widetilde{\mathbf B}(\mathbf r)
=\frac{\mu _0e^{ikr}}{4\pi}
\left(-\frac{i\omega}{r^2}-\frac{\omega^2}{cr}\right)
(\mathbf p_0\times\mathbf n).
}
$$

For $\mathbf p_0=p_0\hat{\mathbf z}$, the nonzero spherical components are

$$
\widetilde E_r
=\frac{2p_0\cos\theta}{4\pi\varepsilon _0}
\left(\frac1{r^3}-\frac{ik}{r^2}\right)e^{ikr},
$$

$$
\widetilde E_\theta
=\frac{p_0\sin\theta}{4\pi\varepsilon _0}
\left(\frac1{r^3}-\frac{ik}{r^2}-\frac{k^2}{r}\right)e^{ikr},
$$

$$
\widetilde B_\phi
=\frac{\mu _0p_0\sin\theta}{4\pi}
\left(-\frac{i\omega}{r^2}-\frac{\omega^2}{cr}\right)e^{ikr}.
$$

The signs of the imaginary induction terms reverse if the $e^{+i\omega t}$ convention is used.

### Radiation field and polarization

Keeping only terms proportional to $r^{-1}$ gives

$$
\boxed{
\mathbf E_{\mathrm{rad}}(\mathbf r,t)
=\frac{1}{4\pi\varepsilon _0c^2r}
\left[\mathbf n\times(\mathbf n\times\ddot{\mathbf p})\right]_{t_r},
}
$$

$$
\boxed{
\mathbf B_{\mathrm{rad}}
=\frac1c\mathbf n\times\mathbf E_{\mathrm{rad}}.
}
$$

Thus

$$
\mathbf E_{\mathrm{rad}}\cdot\mathbf n=0,
\qquad
\mathbf B_{\mathrm{rad}}\cdot\mathbf n=0,
\qquad
E_{\mathrm{rad}}=cB_{\mathrm{rad}}.
$$

The radiated electric field is the projection of $-\ddot{\mathbf p}$ onto the plane of the sky. A dipole oscillating along a fixed real axis produces linearly polarized radiation; a dipole with two phase-shifted components can produce elliptical or circular polarization.

## Radiated energy, momentum, and angular pattern

### Differential power: derivation

In the far zone,

$$
\mathbf S
=\frac1{\mu _0}\mathbf E_{\mathrm{rad}}\times\mathbf B_{\mathrm{rad}}
=\varepsilon _0cE_{\mathrm{rad}}^2\mathbf n.
$$

If $\theta$ is the angle between $\ddot{\mathbf p}$ and $\mathbf n$, then

$$
\left|\mathbf n\times(\mathbf n\times\ddot{\mathbf p})\right|^2
=|\ddot{\mathbf p}|^2\sin^2\theta.
$$

Multiplication by $r^2\mathrm d\Omega$ gives the instantaneous angular distribution

$$
\boxed{
\frac{\mathrm dP}{\mathrm d\Omega}(t)
=\frac{|\ddot{\mathbf p}(t_r)|^2}{16\pi^2\varepsilon _0c^3}
\sin^2\theta.
}
$$

It has two broad lobes normal to the dipole axis and nulls on the axis. Since

$$
\int\sin^2\theta\,\mathrm d\Omega
=2\pi\int_0^\pi\sin^3\theta\,\mathrm d\theta
=\frac{8\pi}{3},
$$

the total instantaneous power is

$$
\boxed{
P(t)=\frac{|\ddot{\mathbf p}(t_r)|^2}{6\pi\varepsilon _0c^3}
=\frac{\mu _0}{6\pi c}|\ddot{\mathbf p}(t_r)|^2.
}
$$

For $\mathbf p(t)=\mathbf p_0\cos\omega t$, where $\mathbf p_0$ is a real peak amplitude,

$$
\left\langle|\ddot{\mathbf p}|^2\right\rangle
=\frac12\omega^4p_0^2.
$$

Therefore

$$
\boxed{
\left\langle\frac{\mathrm dP}{\mathrm d\Omega}\right\rangle
=\frac{\omega^4p_0^2}{32\pi^2\varepsilon _0c^3}\sin^2\theta,
}
$$

$$
\boxed{
\langle P\rangle
=\frac{\omega^4p_0^2}{12\pi\varepsilon _0c^3}.
}
$$

For a general complex vector amplitude $\mathbf p_0$, including a rotating or elliptically oscillating dipole, the corresponding results are

$$
\boxed{
\left\langle\frac{\mathrm dP}{\mathrm d\Omega}\right\rangle
=\frac{\omega^4}{32\pi^2\varepsilon _0c^3}
\left(|\mathbf p_0|^2-|\mathbf n\cdot\mathbf p_0|^2\right),
}
$$

$$
\boxed{
\langle P\rangle
=\frac{\omega^4|\mathbf p_0|^2}{12\pi\varepsilon _0c^3}.
}
$$

The radiation grows as $\omega^4$ at fixed dipole amplitude. Although the field amplitude falls as $1/r$, the area of a sphere grows as $r^2$, so the total radiated power is independent of radius.

### Radiation-pattern properties

| Property | Ideal linearly oscillating electric dipole |
|---|---|
| Normalized power pattern | $f(\theta)=\sin^2\theta$ |
| Field-amplitude pattern | $\lvert F(\theta)\rvert=\lvert\sin\theta\rvert$ |
| Null directions | $\theta=0,\pi$ |
| Maximum directions | $\theta=\pi/2$ |
| Beam solid angle | $\displaystyle \Omega_A=\int f\,\mathrm d\Omega=8\pi/3$ |
| Directivity | $\displaystyle D=4\pi/\Omega_A=3/2$ |
| Far-zone wave impedance | $E/H=\eta _0$ |
| Momentum flux | $\mathrm d\dot{\mathbf P}_{\mathrm{em}}=(\mathbf n/c)\,\mathrm dP$ |
| Net radiated linear momentum for the symmetric pattern | $\displaystyle \int(\mathbf n/c)(\mathrm dP/\mathrm d\Omega)\,\mathrm d\Omega=0$ |

The vanishing net momentum is a consequence of the inversion-symmetric $\sin^2\theta$ pattern, not a statement that the radiation carries no local momentum.

## Driven dipole and Rayleigh scattering

### Lorentz oscillator

A simple microscopic model treats a charge $q$ of mass $m$ bound harmonically and driven by a local electric field:

$$
m\ddot{\mathbf x}+m\gamma\dot{\mathbf x}+m\omega _0^2\mathbf x
=q\mathbf E_0e^{-i\omega t}.
$$

Writing $\mathbf p_0=q\mathbf x_0=\alpha(\omega)\mathbf E_0$ gives the dynamic polarizability

$$
\boxed{
\alpha(\omega)
=\frac{q^2/m}{\omega _0^2-\omega^2-i\gamma\omega}.
}
$$

| Frequency range | Response of the ideal damped oscillator |
|---|---|
| $\omega\ll\omega_0$ | $\alpha\simeq q^2/(m\omega_0^2)$; dipole nearly in phase with the field |
| $\omega\simeq\omega_0$ | Large resonant response limited by damping; phase changes rapidly |
| $\omega\gg\omega_0$ | $\alpha\simeq-q^2/(m\omega^2)$; response is approximately out of phase |

The time-averaged power delivered by the driving field to a dipole is

$$
\boxed{
\langle P_{\mathrm{ext}}\rangle
=\frac{\omega}{2}\operatorname{Im}\!\left(\mathbf p_0\cdot\mathbf E_0^*\right).
}
$$

A passive response therefore has $\operatorname{Im}\alpha\ge0$ under the present $e^{-i\omega t}$ convention. The extracted power is divided between radiation and internal absorption.

### Scattering cross section

For an isotropic induced dipole $\mathbf p_0=\alpha\mathbf E_0$, divide its mean radiated power by the incident plane-wave intensity

$$
I_{\mathrm{inc}}=\frac12\varepsilon _0c|\mathbf E_0|^2.
$$

The result is

$$
\boxed{
\sigma_{\mathrm{sca}}
=\frac{k^4|\alpha|^2}{6\pi\varepsilon _0^2}.
}
$$

If $\theta$ is measured from the induced-dipole axis,

$$
\boxed{
\frac{\mathrm d\sigma}{\mathrm d\Omega}
=\frac{k^4|\alpha|^2}{16\pi^2\varepsilon _0^2}\sin^2\theta.
}
$$

When $\alpha$ is approximately independent of frequency, $\sigma_{\mathrm{sca}}\propto\omega^4\propto\lambda^{-4}$. This is the Rayleigh law.

The optical theorem gives the extinction and absorption cross sections of the same point dipole:

$$
\boxed{
\sigma_{\mathrm{ext}}
=\frac{k}{\varepsilon _0}\operatorname{Im}\alpha,
\qquad
\sigma_{\mathrm{abs}}
=\sigma_{\mathrm{ext}}-\sigma_{\mathrm{sca}}.
}
$$

Passivity requires $\sigma_{\mathrm{abs}}\ge0$, and hence

$$
\operatorname{Im}\alpha
\ge\frac{k^3}{6\pi\varepsilon _0}|\alpha|^2.
$$

Equality holds for a lossless dipolar scatterer, whose extracted energy is entirely reradiated. Thus even a material with no internal absorption must have a positive imaginary part of its *dynamic* polarizability because of radiation damping.

Radiation itself contributes damping. For a nonrelativistic charge, the Abraham-Lorentz radiation-reaction force may be written

$$
\mathbf F_{\mathrm{rad}}
=\frac{q^2}{6\pi\varepsilon _0c^3}\,\dddot{\mathbf x}.
$$

Its mechanical power differs from $-q^2|\ddot{\mathbf x}|^2/(6\pi\varepsilon _0c^3)$ by a total time derivative, so its cycle average exactly accounts for the Larmor radiation loss. The third-order equation has well-known runaway-solution subtleties and is normally used perturbatively.

## Connection with a short antenna

For a uniform-current element with vector effective length $\boldsymbol\ell$, charge conservation gives the dipole-amplitude relation

$$
\boxed{\mathbf p_0=\frac{I_0\boldsymbol\ell}{-i\omega}.}
$$

Substitution into the dipole power gives

$$
\langle P\rangle
=\frac{\eta _0k^2|I_0|^2\ell^2}{12\pi}.
$$

Defining the radiation resistance by $\langle P\rangle=\tfrac12R_{\mathrm{rad}}|I_0|^2$ for peak phasor amplitude,

$$
\boxed{
R_{\mathrm{rad}}
=\frac{\eta _0}{6\pi}(k\ell)^2
=80\pi^2\left(\frac{\ell}{\lambda}\right)^2\ \Omega.
}
$$

This coefficient is for a Hertzian element with uniform current. A physically short center-fed wire has an approximately triangular current distribution and therefore a different effective length and numerical coefficient.

## Summary of scaling laws

| Quantity | Scaling for a fixed harmonic dipole amplitude $p_0$ |
|---|---|
| Quasistatic electric field | $E_{\mathrm{near}}\sim p_0/(\varepsilon _0r^3)$ |
| Induction electric field | $E_{\mathrm{ind}}\sim\omega p_0/(\varepsilon _0cr^2)$ |
| Radiation electric field | $E_{\mathrm{rad}}\sim\omega^2p_0/(\varepsilon _0c^2r)$ |
| Radiation magnetic field | $B_{\mathrm{rad}}=E_{\mathrm{rad}}/c$ |
| Mean radiated power | $\langle P\rangle\propto\omega^4p_0^2$ |
| Rayleigh scattering, fixed $\alpha$ | $\sigma_{\mathrm{sca}}\propto k^4\lvert\alpha\rvert^2\propto\lambda^{-4}$ |
| Static dipole-dipole energy | $U_{12}\propto R^{-3}$ |
| Static dipole-dipole force | $F_{12}\propto R^{-4}$ |

## Validity and common pitfalls

1. The point-dipole fields require $r\gg a$ and $ka\ll1$; they do not describe the internal structure of the source.
2. Radiation is produced by $\ddot{\mathbf p}$, not merely by a nonzero dipole moment or a constant $\dot{\mathbf p}$.
3. Only the $r^{-1}$ fields transport nonzero time-averaged power to infinity. Near fields can have oscillatory Poynting flux without representing net radiation loss.
4. Peak phasor amplitudes introduce a factor $1/2$ in cycle-averaged quadratic quantities.
5. The permanent-dipole energy is $-\mathbf p\cdot\mathbf E$, whereas the energy of a linearly induced static dipole is $-\tfrac12\alpha E^2$.
6. The sign of each imaginary phasor term depends on the chosen time convention; measurable real fields and powers do not.

