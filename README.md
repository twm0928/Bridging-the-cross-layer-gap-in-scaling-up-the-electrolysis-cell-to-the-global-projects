# Bridging-the-cross-layer-gap-in-scaling-up-the-electrolysis-cell-to-the-global-projects
Overview
This repository provides a multi-layer modeling and optimization pipeline for electrolyzer systems, including stack, module, plant, and project levels. Each layer contains dedicated calculation modules and optimization routines that can be run independently or as a workflow.

1. Stack Level
cal_stack.m: Main function for stack-level simulation. Allows specification of various stack design parameters.
f_stack.m: Subroutine for calculating bypass current within the stack, supporting analysis of efficiency losses and current distribution.

2. Module Level
2.1 Lumped state space model:
cal_module.m: Main function for module-level calculations.
topology.xlsx: Input table defining primary parameters for different module topologies.
P_command.mat: Generator for module dispatch power commands.
cluster_UC_I4.m: Optimization model for unit combination (cluster scheduling) within the module layer.
2.2 LSBoost surrogate model:
cal_fitting.m: LSBoost-based regression model for surrogate efficiency prediction. Trains and saves module efficiency surrogate functions by fitting efficiency against scenario features; outputs eta model.

3. Plant Level
cal_plant.m: Main plant-level calculation routine; takes boundary parameters for investment and operation, calls cal_smart.m and eta model, computes hydrogen production.
cal_smart.m: Implements the dispatch (scheduling) strategy; inputs site total power and threshold, outputs power assigned to each module in the plant.

4. Project Level
cal_project.m: Main computation function for real-project evaluation; logic is analogous to cal_plant.m, taking practical economic/operational boundaries as input, and outputting project-level hydrogen production results.
