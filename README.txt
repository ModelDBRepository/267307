Model files for the NEURON simulation environment for the paper

"Cell type-specific mechanisms of information transfer in data-driven biophysical models of hippocampal CA3 principal neurons"

by Daniele Linaro, Matthew J. Levy, and David L. Hunt

PLOS Computational Biology 2022



This repository contains the following folders:

1. mechanisms: the MOD-files used by the models.
2. morphologies: two cell morphologies in SWC format, one for each cell type.
3. individuals: two sets of parameters, one for each cell type, corresponding to several "individuals" obtained with a multi-objective optimization procedure.
4. configs: configuration files to be used with the script "synaptic_cooperativity.py".
5. dlutils: a small Python library necessary to run the code. This is part of the neuronopt package that can be freely downloaded from https://github.com/danielelinaro/neuronopt.



The following scripts can be used to simulate the models:

-------------------------------------------------------------------------------
current_injection.py

Runs a simple current injection protocol on a model cell.

Examples:

python3 current_injection.py -f morphologies/DH070813C1.swc -p individuals/DH070813C1/individual_0.json -c individuals/DH070813C1/parameters.json -n DH070813C1 --replace-axon yes --add-axon-if-missing yes --plot  -v --dur 1000 --delay 500 500

python3 current_injection.py -f morphologies/DH070213C3.swc -p individuals/DH070213C3/individual_0.json -c individuals/DH070213C3/parameters.json -n DH070213C3 --replace-axon yes --add-axon-if-missing yes --plot  -v --dur 1000 --delay 500 50


-------------------------------------------------------------------------------
fI_curve.py

Injects several steps of current in a model cell to compute its static input-output curve (f-I curve).

Examples:

python3 fI_curve.py -f morphologies/DH070813C1.swc -p individuals/DH070813C1/individual_1.json -c individuals/DH070813C1/parameters.json -n DH070813C1 --replace-axon yes --add-axon-if-missing yes --dur 1000 --delay 500 --tran 100 200:600:100

python3 fI_curve.py -f morphologies/DH070213C3.swc -p individuals/DH070213C3/individual_0.json -c individuals/DH070213C3/parameters.json -n DH070213C3 --replace-axon yes --add-axon-if-missing yes --dur 1000 --delay 500 --tran 0 0:250:50   


-------------------------------------------------------------------------------
measure_Rin.py

Injects a hyperpolarizing step of current into each compartment of a model cell to compute its input resistance. It can use SCOOP to run in parallel if the package is available on the platform.

Examples:

python3 -m scoop measure_Rin.py -f morphologies/DH070813C1.swc -p individuals/DH070813C1/individual_1.json -c individuals/DH070813C1/parameters.json -n DH070813C1 --replace-axon yes --add-axon-if-missing yes --dur 1000 --delay 500 --model-type passive --plot -o DH070813C1

python3 -m scoop measure_Rin.py -f morphologies/DH070213C3.swc -p individuals/DH070213C3/individual_0.json -c individuals/DH070213C3/parameters.json -n DH070213C3 --replace-axon yes --add-axon-if-missing yes --dur 1000 --delay 500 --model-type passive --plot -o DH070213C3


-------------------------------------------------------------------------------
measure_spine_AR.py

Injects an EPSP-shaped current into a spine head to measure the spine/dendrite amplitude ratio.

Examples:

python3 measure_spine_AR.py -F morphologies/DH070813C1.swc -p individuals/DH070813C1/individual_1.json -c individuals/DH070813C1/parameters.json -n DH070813C1 --replace-axon yes --add-axon-if-missing yes --model-type passive -O . -q 'apical[14](0.5)'

python3 ../neuronopt/measure_spine_AR.py -F morphologies/DH070213C3.swc -p individuals/DH070213C3/individual_0.json -c individuals/DH070213C3/parameters.json -n DH070213C3 --replace-axon yes --add-axon-if-missing yes --model-type passive -O . -q 'apical[16](0.5)'


-------------------------------------------------------------------------------
synaptic_cooperativity.py

Simulates the sequential activation of spines located on the dendritic tree of a model cell while also injecting an Ornstein-Uhlenbeck current in the soma to replicate ongoing background synaptic activity.

Examples:

python3 synaptic_cooperativity.py config/synaptic_inputs_config_thorny.json

python3 synaptic_cooperativity.py config/mutual_information_config_thorny.json



Each script has an extensive online help that can be accessed by typing

python3 <script-name> --help


For further questions on how to use this model please contact Daniele Linaro at the following email address: danielelinaro@gmail.com.
