# MoM-Inspired-Physics-Constrained-NN-Synthesis-of-Microstrip-Patch-Antenna
------------------------------------------------------------------------------

Aligned single-patch MoM + NN project for MPA synthesis at 2.4 GHz
================================================

Brief preview:
-----------------------------------------------------------------------------
This project is more a runnable educational MoM-style proxy project for a single coax-fed rectangular MPA (Microstrip Patch Antenna) on FR4 around 2.4 GHz. It combines:

- a lightweight Method-of-Moments-style electromagnetic proxy core,
- a small neural-network surrogate workflow,
- a quick goal-driven synthesis script,
- and plot generation for return loss, VSWR, directivity, radiation pattern, E/H cuts, and a 3D polar plot.

Important notes:
-----------------------------------------------------------------------------------
This is NOT a rigorous 3D full-wave solver like are e.g. HFSS/CST/WIPL-D.

our project is more an educational/research scaffold with a proxy Green operator and proxy S11 model. The coax feed (here we got the most of error during testing/verification) is modeled as a localized coax-like excitation surrogate, not as a full 3D connector. 

For example, a plain single FR4 patch at 2.4 GHz generally will not deliver 15 dBi gain (more realistic is 5-7 dBi)
but, if you want 15 dbi then we usually need an MPA array, a superstrate/metasurface, or a higher-directivity structure.

The project still accepts the 15 dBi request as an aspirational target, but in practice it maximizes gain within a more realistic single-patch regime while prioritizing 2.4 GHz matching.

Baseline geometry used in this version
--------------------------------------------------------------------------------
- Single patch (not an array)
- Substrate: FR4_epoxy-like, eps_r = 4.4, tan(delta) = 0.02
- Substrate thickness: 1.6 mm
- Initial substrate size: 70 mm x 70 mm
- Initial patch size: computed from classical rectangular microstrip formulas for 2.4 GHz on FR4
- Coax-probe surrogate inner radius: 0.35 mm
- Coax-probe surrogate outer radius: 1.20 mm
- Feed position: optimized local x/y offset on the patch
- Target center frequency: 2.4 GHz
- Requested targets: strong matching near -30 dB return loss, high gain, wide HPBW

Files:
-----
- config.py                    -> global configuration
- geometry.py                  -> single-patch mesh generation
- basis.py                     -> local x/y basis functions
- greens.py                    -> proxy layered Green operator
- port_model.py                -> coax-like local excitation surrogate
- mom_assembler.py             -> Z-matrix assembly and pattern metrics
- solver.py                    -> frequency sweep and EM result packaging
- dataset_and_metrics.py       -> dataset build and local refinement objective
- nn_numpy.py                  -> tiny NumPy MLP implementation
- train_and_synthesize.py      -> full NN surrogate workflow
- main.py                      -> entry point (calls train_and_synthesize.main)


How to run Full NN + surrogate path:
-------------------------------------
    python main.py



Outputs
-------
The project generates:
- return_loss.png
- vswr.png
- directivity.png
- radiation_pattern.png
- e_h_field_patterns.png
- polar_3d.png
- nn_training_history.png  (only in the full NN path)
- synthesis_summary.txt
