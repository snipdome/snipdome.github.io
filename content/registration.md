Imagine a factory where rapid and accurate quality control is essential for maintaining production efficiency and product reliability. Traditional methods like X-ray computed tomography (X-CT) offer precise internal inspections but are often too expensive and time-consuming for routine quality checks.

To address this challenge, I developed a faster, cost-effective alternative that enables analysis directly in projection space by registering the object and its CAD model using only a few X-ray radiographs.

In fast-paced manufacturing environments, inspecting the internal structure of parts is crucial, but conventional methods requiring numerous X-ray images from various angles are impractical. My technique allows for the registration of a CAD model into projections with minimal radiographs. This approach facilitates the comparison between acquired and simulated projections, simplifying defect detection and providing critical information about X-ray path lengths—useful for post-processing methods like beam-hardening compensation. The method leverages a differentiable mesh projector ([CAD-ASTRA](https://doi.org/10.1364/OE.498194)), a tool that simulates X-ray projections from known object surfaces.
#### How It Works

1. Initial Setup: Start with an approximate position and orientation of the object.
2. X-Ray Projection Simulation: Use CAD-ASTRA to simulate the projections.
3. Mesh Registration: Employ a PyTorch framework to iteratively adjust the object's 3D model to match the X-ray projections.

![target1](/gifs/registration/opt.gif){height=100px, class="right"}

#### Final result
An aligned 3D model of the CAD w.r.t. the object, even with just a pair of X-ray radiographs.

![target2](/gifs/registration/opt3d.gif)
![target3](/images/registration/final.jpeg)

**Mission accomplished!**