2015 Nijmegen Layer Analysis Meeting
====================================

On October 22nd and 23rd 2015, David Norris hosted the first layer-fMRI workshop in Nijmegen. This workshop was focusing on hands-on analysis questions in layer-fMRI. Attendees were asked to share example data across vendors and acquisition methods. The agenda contained open discussions on the following questions:

1. What data quality can we expect?
2. Image registration
3. Defining and determining cortical surfaces
4. The equi-volume principle (Bok)
5. How to determine layer surfaces and how many layers should I model
6. Will it ever be possible to really know the depths of the histological layers in vivo?
7. What are the realistic benefits of high resolution and layer specific fMRI?

Session on Image Registration
#############################

Coordinators: Sue Francis, Rosa Panchuelo (Nottingham)

- Maastricht group mentioned that it is beneficial for layer0fMRI to use small FOVs. Best is to use IR-EPI for segmentation. Mean EPI can also be used, but the contrast between GM/WM is not as good. Acquire a scan with inverted PE direction. Preferably register anatomy to EPI, not the other way around: we want to leave the functional scans as untouched as possible.
- It is mentioned that RETROICOR would beneficial at resolution of 1mm isotropic for 3D EPI.
- It is furthermore suggested to use GLM noise (noise mask + PCA of noise).
- Rosa Panchuelo mentions that AFNI is the best tool for motion correction.
- Tim van Mourik recommends affine registration with boundary-based cost functions (FSL or FreeSurfer).
- Kamil Uludag: we need a more objective way of assessing the quality of registration, people do it by eye at the moment.

Session on Cortical Surfaces
############################

Coordinator: Pierre-Louis (Pilou) Bazin and Sriranga (Sri) Kashyap

- Pilou showed how to use JIST Layout Tool.
- It is mentioned that FOV of the MP2RAGE needs to be reduced in order to get a satisfactory coregistration with the small FOV EPI (uses fslroi).
- Sri showed a pipeline for TOPUP correction.
- Sri showed how to use ITK-SNAP for manual delineation of WM/GM/CSF borders.


Session on Motion Correction
############################

Coordinator: Federico de Martino

- The session agrees that the motion correction should be based on your ROI only. If you do motion correction for the whole brain, it will definitely not perform the best in your ROI.
   - This option uses a spatial weighting of the cost function.
   - For example, SPM can handle a weighting mask: by default it is the inverse of the standard deviation, but any other mask can be used. For example, you can provide a mask with high values within your ROI and low values elsewhere; performs good.
- Question by Tim van Mourik: why would you discard movement exceeding a certain threshold, let’s say 3mm? Shouldn’t the motion correction be accounting for it?
   - Kamil Uludag: the algorithms are not optimized for large motion, the cost function goes to local minima.
   - Federico de Martino: it depends a lot whether the movement is abrupt (=lack of information or distortion) or smooth; 2mm motion over a long scan could be probably handled.
   - David Norris: Motion is worse for 3D EPI. Major movements degrade shim.
- Question by Kashyap: would you include the motion parameters in your GLM?
   - Federico de Martino: it is a good idea but depends how correlated they are with your task. Anyways, when they are too correlated, you’d probably discard the full dataset.

Session on Generating Depth Specific Signals from fMRI Data
###########################################################

Coordinator: Tim van Mourik

- On the spatial GLM
   - Kamil Uludag: A GLM is the best approach when activation is uniform over a layer. This is usually not the case.
   - Christian Keysers: The spatial GLM performs better than interpolation because it has a horizontally optimized filter and assumes that the signal varies only in the vertical direction; but if you have an horizontal variation of the signal, then maybe the results would start to converge with the standard interpolation.
   - Federico de Martino: if your layers are crossing boundaries between areas, your GLM assumption is not valid.
   - David Norris: you can still use the model to subdivide regions – for example, you could ask yourself how many voxel are sufficient to get a good vertical profile.
   - Pierre-Louis Bazin: the spatial GLM is a nice model, but in the real world we have plenty of artifacts which make the signal not horizontally homogeneous (for example veins).
   - Valentin Kemper: you claim GLM has a better PSF. But for EPI acquisitions the PSF is anisotropic and should be taken into account.
   - Norris: your PE direction blurring should be lower than your voxel, otherwise you shouldn’t even be taking the effort to acquire data.

- On the question how many layers should be reconstructed.
   - Uludag: 10 is the magic number = (1 for CSF + 1 for WM + 3 for GM)x2. You absolutely need to have more layers than what is neuroscientifically meaningful, because you need to be sure that you are not missing any effect. So, if you want to infer characteristics of 3 layers, you need to have at least 6 in order to have a robust estimate of the signal.
   - David Norris: at the time being, probably 3 layers is the maximum we can say something about.
   - Natalia Petridou: absolutely dependent on resolution and acquisition scheme.
   - Robert Trampel: depends on cortical region.

- On the question what can be used as a quality measure?
   - Federico de Martino: 1) start from higher resolution images and degrade them, or do simulations. When you have few voxels, the amount of layers should be carefully defined (probably 3 layers is the maximum for the current resolutions). 2) you need a control. If you see a statistically significant difference between two conditions it means that you are seeing something meaningful.
   - David Norris: maybe with simple tasks, but with higher order?
   - Kamil Uludag: you might have an error in one of the two conditions.
   - Pierre-Louis: use anatomy. Or else with fMRI, look at an area that is more or less homogeneous.
   - Christian Keysers: ex-vivo is really appealing for validation, you can image super high resolution with EPI, and then degrade the resolution.

- On the signal change in WM?
   - Kamil Uludag: draining vein effect. No problem with it, unless you claim you see a WM BOLD.

Session on How Layer Specific is the Haemodynamic Response?
###########################################################

Coordinator: Kamil Uludag

- Kamil Uludag discusses a number of mechanisms:
   - Blood flow control – arterioles and capillaries (Atwell et al.)
   - Blood perfusion territory (ASL-type perfusion) – unknown, but likely to be in the order of a few hundreds μm³
   - Blood volume changes – arteries and arterioles
   - Blood oxygenation changes – arterioles-capillaries-veins (increasing order)
   - Undershoot and initial dip have probably a similar origin (arterial volume) and therefore it is enough to investigate one of the two – Uludag is focusing on PSU.
   - Regarding PSU: the inhibition period is longer for prolonged stimulations (the neuronal component of the PSU). The rest period in a block design should absolutely be the double of the active period.
   - The layer profile is different for positive BOLD and PSU.

Cheryl Olman (skype) comments that her group observed very high variability in PSU even for the same subjects.

Session on Layer-Specific Contributions to Neuroscience
#######################################################

Coordinator: Holly Bridge (FMRIB)

- Molly Bright discusses a number of applications for layer-fMRI:
   - short vs long range connectivity;
   - understanding what changes in cortical thickness really mean – using some landmarks as reference, for example the stria of Gennari;
   - boosting SNR by focusing on the layers with signal;
   - language;
   - disorders (amblyopia, dislexia, schizofrenia).

- On the question on how do electrophysiology and fMRI relate? How local is the LFP?
   - Christian Keysers: calcium imaging is the way to go.
   - Federico: LFP fails at laminar level. It is not specific. Kajigawa (2014) for laminar LFP.
   - David Norris: depth-specific LFP experiments cannot be translated to fMRI, no verification dataset.

- On the question of the vascular organisation with respect to cell somas and dendrites? Should we revise the definition of layers when using fMRI?
   - Kamil Uludag: haemodynamic response is closer to the dendrites (ion pumps). What happens at the soma is not the relevant metabolic process.
   - Synaptic density is correlated to vascular density. A work by Bruno Weber shows that metabolism and synapsis correlate to vasculature, not cell bodies.
   - Kamil Uludag: vascular density (excluding surface) does not change much across GM, something like 2.5%.


Acknowledgements
################

We thank Maria Guidi for sharing her detailed notes of this event that were used to generate this event summary.
