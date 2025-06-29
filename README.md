# Flytbase-Robotics-Assignment

Drone Deconfliction System - Documentation

README

Overview

This project implements a drone deconfliction system that checks for spatial and temporal conflicts between a primary drone and other drones in shared airspace. It also visualizes drone trajectories in a 4D simulation (3D space + time).

Requirements

Python 3.7+

matplotlib

numpy

Setup

pip install matplotlib numpy

Running the Simulation

python main.py

You can configure different drone scenarios by editing the main.py file to define new DroneTrajectory objects.

Files

trajectory.py: Defines the Waypoint and DroneTrajectory classes.

conflict_checker.py: Implements deconfliction_service() to check for conflicts.

visualizer.py: Contains create_animation() to simulate and visualize the missions.

main.py: Entry point for defining drone missions and running simulation.

Reflection & Justification Document

Design and Architecture

We designed the system with modularity and future scalability in mind:

DroneTrajectory class encapsulates each drone's movement.

Waypoints are used to define routes in 3D space.

Conflict checking logic is independent and can be scaled or optimized.

The animation and visualization module simulates drone movement and highlights conflicts in real-time.

Spatial and Temporal Checks

Spatial Check: Computes Euclidean distance between the primary drone and others at each timestep. A conflict is flagged if distance < safety threshold.

Temporal Check: Only evaluates conflicts during overlapping time windows using a linear interpolation model for position estimation.

AI Integration

Currently, the system does not include AI for autonomous decision-making. However, the architecture allows for integrating:

Conflict prediction using ML models.

AI-based rerouting or flight rescheduling.

Testing Strategy

We manually test scenarios:

No conflicts.

Conflict at midpoint.

Conflict due to altitude.

Multiple drones causing simultaneous conflict.

Automated tests can be added using pytest to validate the deconfliction_service() logic against known test cases.

Edge Case Handling

Empty waypoint list is handled via validation.

Time outside bounds returns None for position.

Segment indexing ensures drones do not exceed waypoint range.

Scalability Considerations

To support real-world scaling with thousands of drones:

Spatial Indexing: Use R-Trees or k-d trees to quickly locate nearby drones.

Real-Time Streaming: Integrate with Kafka or MQTT to receive real-time drone telemetry.

Distributed Processing: Partition the airspace into regions and assign to worker nodes for parallel conflict checks.

Database Optimization: Store trajectories in time-series databases like InfluxDB.

Fault Tolerance: Use cloud-native tools (Kubernetes, Docker) to ensure availability and autoscaling.

The system provides a solid foundation for simulation and can evolve into a production-grade air traffic coordination service for unmanned aerial vehicles (UAVs).
