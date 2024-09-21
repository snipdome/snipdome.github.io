Imagine a factory where rapid and accurate quality control is essential for maintaining production efficiency and product reliability. Traditional methods like X-ray computed tomography offer precise internal inspections but are often too expensive and time-consuming for routine quality checks.

To address this challenge, I developed a faster, cost-effective alternative that enables analysis directly in projection space by registering the object and its CAD model using only a few X-ray radiographs. This approach facilitates the comparison between acquired and simulated projections, simplifying defect detection and providing information about X-ray path lengths—useful for post-processing methods like beam-hardening compensation. The method utilises a mesh projector implemented as differential program ([CAD-ASTRA](https://doi.org/10.1364/OE.498194)), a tool that simulates X-ray projections from known object surfaces.
#### How It Works

1. Initial Setup: Start with an approximate position and orientation of the objects composing the scanned scene.
2. X-Ray Projection Simulation: Use CAD-ASTRA to simulate the projections.
3. Mesh Registration: Employ a PyTorch framework to iteratively adjust the objects pose to match the X-ray projections.

![target1](/gifs/registration/opt.gif)

![target2](/gifs/registration/opt3d.gif)

#### Final result
Aligned 3D models of the CADs w.r.t. the object and its supporting elements.

![target3](/images/registration/final.jpeg)

In the [article](https://link.springer.com/article/10.1007/s10921-024-01071-y), it is shown how it was possible to reach make it work even with just two radiographs. For what were the initial purposes of the project, we are in a case of.. **Mission accomplished!**