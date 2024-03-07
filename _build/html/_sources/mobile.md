# Mobile errors

We now want to shift $x$ by a constant speed such that in 1 step the GPS true evaluation point has moved by $s$. Assume Gaussian errors for $x$ and $y$ both of standard deviation $\sigma$; i.e., the probability measure for the end-point is:

$$p'(x,y)dx'dy'=\exp[-((x'-s)^2+y'^2)/2]dx'dy'/2\pi$$

We scale distance in units of the standard deviation, $\sigma=1$.

The start point probability is as before:

$$p(x,y)dxdy=\exp[-(x^2+y^2)/2]dxdy/2\pi$$

The average distance between two determinations, $\mathbf r$ and $\mathbf r'$, is given by:

$$\left<|\mathbf r'-\mathbf r|\right>=\int d^2\mathbf rd^2\mathbf r' |\mathbf r'-\mathbf r|p(\mathbf r)p'(\mathbf r')$$

We can tranform as before to $\mathbf R$ and $\Delta\mathbf r$:

$$\left<|\Delta\mathbf r|\right>=\int d^2\mathbf Rd^2\Delta\mathbf r |\Delta\mathbf r|p(\mathbf R-\Delta\mathbf r/2)p'(\mathbf R+\Delta\mathbf r/2)$$

We can vectorize the step $\mathbf s$, and now substitute the distributions:

$$\left<|\Delta\mathbf r|\right>=\int d^2\mathbf Rd^2\Delta\mathbf r |\Delta\mathbf r|\exp\left[-(\mathbf R-\Delta\mathbf r/2)^2/2-(\mathbf R+\Delta\mathbf r/2-\mathbf s)^2/2\right]/(2\pi)^2$$

We want to remove the $\mathbf R$ dependence by completing the square in the exponent:

$$(\mathbf R-\Delta\mathbf r/2)^2+(\mathbf R+\Delta\mathbf r/2-\mathbf s)^2&=2\mathbf R^2-2\mathbf R.\mathbf s+(\Delta\mathbf r/2)^2+(\Delta\mathbf r/2-\mathbf s)^2 \\
&=2(\mathbf R-\mathbf s/2)^2-\mathbf s^2/2+(\Delta\mathbf r/2)^2+(\Delta\mathbf r/2-\mathbf s)^2$$

and then integrating out:

$$\left<|\Delta\mathbf r|\right>&=\int d^2\Delta\mathbf r |\Delta\mathbf r|\exp\left[+\mathbf s^2/4-(\Delta\mathbf r/2)^2/2-(\Delta\mathbf r/2-\mathbf s)^2/2\right]/4\pi \\
&=\int d^2\Delta\mathbf r |\Delta\mathbf r|\exp\left[-(\Delta\mathbf r-\mathbf s)^2/4\right]/4\pi$$

The standard deviations of the coordinates has increased by a factor $\sqrt2$ (variance doubling). We want to go to polar coordinates $\Delta r$, $\theta$, so $\Delta\mathbf r.\mathbf s=\Delta rs\cos\theta$:

$$\left<|\Delta\mathbf r|\right>=\int d\Delta rd\theta\Delta r^2\exp\left[-(\Delta r^2+s^2)/4+\Delta rs\cos\theta/2\right]/4\pi$$

It is tempting to integrate out the angular dependence but I suspect I would end up with a modified Bessel function to integrate, not a desirable state of affairs.

We define $t=\Delta r-s\cos\theta$:

$$\left<|\Delta\mathbf r|\right>=\int dtd\theta(t+s\cos\theta)^2\exp\left[-s^2(1-\cos^2\theta)/4-t^2/4\right]/4\pi$$

We can expand this into a series of separated $t$ and $\theta$ integrals. (If we want higher powers for variances and such, a similar technique is possible).

The $t$ integrals will be of the form:

$$T_n=\int dtt^n\exp\left[-t^2/4\right]=2^n\Gamma[(n+1)/2]$$

The $\theta$ integrals are:

$$\Theta_n(s)=\int_{-\pi}^{+\pi} d\theta\cos^n\theta\exp\left[-s^2(1-\cos^2\theta)/4\right]$$

This is an integral of an even function, so integrating over $(-\pi,\pi)$ gives twice the value for $(0,\pi)$. We note further that $\cos\theta$ is odd about $\pi/2$. Odd powers will therefore be odd, and even powers even. The exponential will be even, so the odd powers of $\cos\theta$ will integrate to zero, and we need only consider even powers $n$, and integration over $(0,\pi/2)$. We can consider just $n=0$, since higher powers be derived by differentiating.

We therefore put forward for your consideration:

$$I_0(z)=\frac1\pi\int_0^\pi\exp(\pm z\cos\theta)d\theta$$

As indicated, this is an even function of $z$, since $\cos\theta$ is odd about $\pi/2$. Our integrals are not quite in this form, but can easily be made so through $\cos^2\theta=(\cos(2\theta)+1)/2$.

$$\Theta_0(s)=4\int_0^{+\pi/2} d\theta\exp\left[s^2(\cos(2\theta)-1)/8\right]=2\pi I_0(s^2/8)\exp(-s^2/8)$$

To simplify differentiation we consider $\Theta$ as a function of $z=s^2/8$. Then:

$$\frac{d\Theta_0}{dz}&=-2[\Theta_0(z)-\Theta_2(z)] \\
&=2\pi\left[\frac{dI_0}{dz}-I_0(z)\right]\exp(-z)$$

Also, the final piece, $I_1(z)=I_0'(z)$. Therefore,

$$\Theta_2(z)=\pi\left[I_1(z)+I_0(z)\right]\exp(-z)$$

Returning to our desired object:

$$\left<|\Delta\mathbf r|\right>=(T_2\Theta_0(s)+s^2T_0\Theta_2(s))/4\pi$$