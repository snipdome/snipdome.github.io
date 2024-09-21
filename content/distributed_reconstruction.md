In my work on CT reconstruction, I utilized a distributed computing approach with MPI to address the significant memory and computational demands of iteratively reconstructing large volumes. By distributing the computational load across multiple GPUs, I was able to efficiently manage the iterative reconstruction process.

By partitioning the reconstruction volume into smaller chunks, each GPU worker in a computational node is responsible for a specific section of the projection data. This setup reduces memory usage on each node and enables parallel processing of the forward and backprojection steps, as described by [Palenstijn](https://doi.org/10.1186/s40679-016-0032-z). The distributed nature of these computations also necessitated careful coordination of data exchanges between GPUs, particularly in the overlapping regions of the CT scan, where adjacent data slabs needed to communicate their results.

![MPI work distribution](/images/distributed_reconstruction/mpi.png)

The algorithms which were developed with this distributed system by minimising the projective error as in the traditional SIRT reconstruction, are BB (based on [Barzilai-Borwein optimisation step](https://doi.org/10.1093%2Fimanum%2F8.1.141)) and [DART](https://doi.org/10.1109/TIP.2011.2131661) (discrete reconstruction). Additionally, by accounting for the [energy-dependent behavior](https://doi.org/10.1007/s10921-024-01071-y) of conventional X-ray scanning systems, two more algorithms were developed: poly-BB (polychromatic BB) and poly-DART.

Examples of reconstructions are provided below.

## BB
![BB and polyBB reconstructions](/images/distributed_reconstruction/bbs.png)

On the left, you see a slice of the BB reconstruction. On the right is the corresponding poly-BB reconstruction. Notably, the poly-BB reconstruction does not suffer from the cupping artifact typically caused by beam hardening.

## DART
![DART and polyDART reconstructions](/images/distributed_reconstruction/darts.png)

On the left is a slice of the DART reconstruction, while the right side shows the related poly-DART reconstruction. It’s evident that the DART reconstruction struggles to classify pixels accurately, particularly near the object's inner region, where it is affected by the beam hardening effect. In contrast, the poly-DART reconstruction is not impacted by this issue.

The non-distributed versions of these algorithms will soon be integrated into the [ASTRA toolbox](https://github.com/astra-toolbox/astra-toolbox).