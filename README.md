# Lab 3: Shortest Path Algorithms with Negative Edge Handling

## Overview

This project implements and compares three shortest path algorithms to handle graphs with potentially negative edge weights. The focus is on understanding how negative edges and negative cycles affect shortest path calculations, and how to safely compute paths in such graphs.

## The Problem

**Objective**: Find the shortest path from a source node (node 0) to all other nodes in a weighted directed graph.

**Challenge**: Traditional Dijkstra's algorithm assumes non-negative edge weights. When graphs contain:
- **Negative edges**: Dijkstra may produce incorrect results
- **Negative cycles**: Paths can be arbitrarily shortened by traversing the cycle repeatedly

## Algorithms Implemented

### 1. Standard Dijkstra's Algorithm
- **Complexity**: O(V²) with array-based implementation
- **Assumptions**: Works correctly only with non-negative edge weights
- **Limitation**: May produce incorrect results with negative edges

### 2. Positive-Path-Only Dijkstra
- **Complexity**: O(V²)
- **Innovation**: Modified Dijkstra that only accepts paths with non-negative total distance
- **Safety**: Rejects any path where the cumulative distance becomes negative
- **Use case**: Ensures safe results even in graphs with negative edges

### 3. Bellman-Ford Algorithm
- **Complexity**: O(V³) with our implementation
- **Capability**: Correctly handles negative edge weights
- **Detection**: Identifies and reports negative cycles
- **Propagation**: Tracks all nodes affected by negative cycles

## Negative Cycle Analysis

The project includes sophisticated negative cycle categorization:

### Cycle Categories

1. **Problematic Cycles** 
   - Reachable from the source node
   - Can escape from the cycle to reach other nodes
   - **Impact**: Breaks shortest path guarantees (paths can be infinitely shortened)
   - **Solution**: Use Positive-Path-Only Dijkstra

2. **Trapped Cycles** 
   - Reachable from the source node
   - Cannot escape from the cycle
   - **Impact**: None (you get stuck in the cycle, but it doesn't affect other paths)
   - **Safety**: Safe to ignore for other path calculations

3. **Unreachable Cycles** 
   - Cannot be reached from the source node
   - **Impact**: None (doesn't affect any paths from source)
   - **Safety**: Safe to ignore

## Problem Generation

Test problems are generated with configurable parameters:

- **Sizes**: 10, 20, 50, 100, 200, 500, 1000 nodes
- **Densities**: 0.2, 0.5, 0.8, 1.0 (edge connectivity)
- **Noise levels**: 0, 0.1, 0.5, 0.8 (randomness in weights)
- **Negative values**: False, True (allow negative edge weights)

**Total**: 224 problem instances (7 × 4 × 4 × 2)

## Key Features

### 1. Comprehensive Testing
- Generates 224 diverse test problems
- Measures execution time for each algorithm
- Calculates reachability and distance statistics

### 2. Algorithm Comparison
- Side-by-side comparison of all three algorithms
- Performance metrics (execution time)
- Correctness validation
- Identifies when algorithms disagree

### 3. Interactive Problem Explorer
- Analyze individual problems in detail
- View all paths from node 0
- Compare algorithm outputs
- Visual negative cycle analysis
- Safety assessment for each problem

### 4. Results Export
- CSV format for data analysis
- JSON format for detailed information
- Comprehensive text report with complexity analysis
