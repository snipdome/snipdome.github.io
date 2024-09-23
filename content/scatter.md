In my recent work on the PACS method ([Projection-driven with Adaptive CADs X-ray Scatter Compensation](https://doi.org/10.1016/j.precisioneng.2024.08.006)), I developed a novel approach to address a major challenge in additive manufacturing inspection: X-ray scatter. This innovative method significantly improves non-destructive testing by compensating for scatter, eliminating the need for a prior X-ray CT (X-CT) scan—a traditionally time-consuming and mandatory step for simulation-based methods.

Prior to PACS, X-CT was essential for simulation-based scatter compensation, setting these methods apart from heuristic approaches like [Scatter Kernel Superposition](https://doi.org/10.1088/0031-9155/55/22/007) (SKS) and its many variations. My work bridges this gap, making simulation-based methods competitive with heuristic techniques for the first time.

The main significance of this work is in:

1. Elimination of Prior Scans: Unlike traditional scatter compensation methods, PACS removes the need for an expensive and time-intensive prior X-CT scan.
2. Versatile and Dynamic: This method adapts to varying object characteristics and inspection scenarios, offering flexibility across diverse industrial applications (i.e. different object shapes and materials) without need for re-train (SKS, Deep Learning methods).
    

The PACS pipeline begins with registration and deformation estimation, which you can see in more detail [here](../registration) and [here](../deformation) ...

![preliminary procedures](/images/scatter/reg-and-deform.png)

Once the registration process is complete, the pipeline uses an X-ray particle interaction simulation to estimate scattered radiation during the scan.

![MC scatter gif](/gifs/scatter/scatter3d.gif)

I used GATE for these simulations—a CPU-based tool known for accurately simulating full physics interactions. As the number of simulated photons increases, the scattered radiation estimation becomes less noisy, as seen in this example:

![scatter MC statistics and noise](/images/scatter/scatterMC.png)

To me, two cases of the results shown in the article are worth mentioning here. By comparing projections affected by scattered radiation with scatter-compensated counterparts (SKS vs. PACS), PACS proved to be the only method that reliably highlighted defective areas. In residual images (i.e., real projections minus simulated projections), defective zones are only expected where these residuals differ from zero. This was demonstrated clearly in the following close-up:

![Scatter corrected projection and residual](/images/scatter/proj.png) 


![Close up](/images/scatter/closeupfig.png)

In the reconstructed volume space, a similar observation can be made. The scatter-compensated projections—particularly PACS—showed a reduced influence from scattering artifacts, which tend to introduce spurious gray value trends unrelated to the actual material density of the gear:

![reco slice](/images/scatter/slice-482.png) 

![line profile of reco](/images/scatter/line-profile_slice-482.png) 

This project has been the longest and most complex I’ve undertaken so far, involving intricate simulations and extensive coding. It brought immense satisfaction when the final line of the pipeline came out.