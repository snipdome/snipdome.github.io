In additive manufacturing, accurately estimating the deformation of a printed object is often desired to assess printing quality. This deformation can arise from various factors in the printing process, such as residual stress, thermal expansion, or inaccuracies in material deposition. Understanding and quantifying this deformation is essential to ensure the structural integrity and functionality of the manufactured component. X-ray Computed Tomography (X-CT) and other non-destructive evaluation techniques provide a way to inspect these deformations by comparing the printed part with its original CAD model.

The deformation estimation approach involves using a differential mesh projector, for which I implemented the differential part ([CAD-ASTRA](https://doi.org/10.1364/OE.498194)), in combination with scanned X-ray projections to detect discrepancies between the scanned object and its digital twin. The CAD model of the printed object is utilized to simulate the nominal shape of the part. By projecting this CAD model into the X-ray projection space, we can estimate first the object's position and then any deformations that occurred during the printing process.

The process begins with obtaining a few X-ray projections of the printed object. These projections allow the system to estimate the pose of the object and provide a starting point for iteratively refining the object's shape. 

![gear deformation with CAD model](/images/deformation/gear_deform_cad.png)

In this figure, it is superimposed the scanned object X-CT and the theorical CAD model after registration on the scanned object. The mesh of the scanned object is not available usually, unless through a complete X-CT, which is reported here just for highlighting the deformation of the object w.r.t. the original CAD model.

By minimizing the difference between the simulated projections of the CAD model and the scanned projections of the printed object, we identify surface deformations. These deformations, represented as per-vertex shifts from the nominal surface mesh, give a detailed picture of where and how the object deviates from its original design, as the animation below shows (white/black colors indicate high difference between the scanned and simulated projections):

![gear deformation gif](/gifs/deformation/opt2.gif)

The integration of regularization terms helps maintain the mesh integrity, ensuring that the estimated deformations remain realistic and within expected bounds. 

![gear deformation](/images/deformation/gear_deformation.png)

For more information, visit the [article](https://doi.org/10.1016/j.precisioneng.2024.08.006) in which this estimation has been used for X-ray scattering compensation or for deformation prediction during AM printing (coming soon)!