The Oren–Nayar reflection model is a diffuse reflectance model for rough surfaces. It generalizes Lambertian reflection by accounting for surface microfacets with varying orientations.

Let $\omega_i$ be the incident light direction, $\omega_o$ the outgoing view direction, and $n$ the surface normal. The reflected radiance is

$$
L_o(\omega_o)
=
\frac{\rho}{\pi}
L_i(\omega_i)
\max(0, n \cdot \omega_i)
\left(
A + B \max(0, \cos(\phi_i - \phi_o)) \sin \alpha \tan \beta
\right)
$$

where

$$
A
=
1
-
\frac{1}{2}
\frac{\sigma^2}{\sigma^2 + 0.33}
$$

and

$$
B
=
0.45
\frac{\sigma^2}{\sigma^2 + 0.09}
$$

The angular terms are defined as

$$
\alpha = \max(\theta_i, \theta_o),
\qquad
\beta = \min(\theta_i, \theta_o)
$$

- $\theta_i$ and $\theta_o$ are the angles between the normal $n$ and the directions $\omega_i$ and $\omega_o$, respectively.
- The azimuthal angles $\phi_i$ and $\phi_o$ describe the directions of $\omega_i$ and $\omega_o$ after projection onto the tangent plane of the surface.
- The parameter $\rho \in [0,1]$ is the diffuse albedo of the material.
- $\sigma$ is the surface roughness, usually measured in radians. When $\sigma = 0$, the model reduces approximately to Lambertian reflection.

The set of valid directions is commonly written as

$$
\omega_i, \omega_o \in \left\{ \omega \in \mathbb{S}^2 \mid n \cdot \omega > 0 \right\}
$$

- $\mathbb{S}^2$ is the unit sphere and the condition $n \cdot \omega > 0$ restricts directions to the visible hemisphere above the surface.
- $L_o(\omega_o)$: outgoing radiance in the viewing direction.
- $L_i(\omega_i)$: incoming radiance from the light direction.
- $\rho / \pi$: Lambertian diffuse scaling term.
- $\max(0, n \cdot \omega_i)$: cosine attenuation due to incident angle.
- $A$: base diffuse correction caused by roughness.
- $B$: directional correction caused by correlation between illumination and viewing directions.
- $\cos(\phi_i - \phi_o)$: azimuthal alignment between light and view directions.
- $\sin \alpha \tan \beta$: angular factor that increases retroreflection on rough surfaces.
- $\sigma$: roughness parameter controlling deviation from ideal Lambertian reflection.

Thus, the Oren–Nayar model describes rough diffuse reflection by modifying the Lambertian term with angular corrections dependent on surface roughness and the relative geometry of the light and view directions.