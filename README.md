# ProtGraphX

This project is a follow-up to [ProtGraph](https://github.com/your-username/ProtGraph), with added support for multi-chain proteins, sequential edges, and export to GNN-friendly formats.

**ProtGraphX** builds on the idea of representing protein structures as graphs.
It extracts Cα atoms from all chains in a PDB file, adds both spatial and sequential edges between residues, and assigns biochemical features to each node.

The resulting graph can be saved in multiple formats including [PyTorch Geometric] for use in graph neural network models.

---

## What it does

1. Reads a PDB file and extracts all chains
2. Gets the Cα (alpha carbon) coordinates for all residues
3. Builds a graph with:

   * Edges between residues that are close in 3D space (≤ 8 Å)
   * Edges between consecutive residues in the sequence (i → i+1)
4. Assigns numerical features to each node from a CSV file:

   * Hydrophobicity
   * Molecular weight
   * Net charge
5. Converts the graph to **NetworkX** and **PyTorch Geometric** formats
6. Saves and visualizes the graph (colored by hydrophobicity)

---

## Files

* protgraphx.ipynb → main notebook
* data/1AOS.pdb → sample protein file
* data/amino_acid_properties.csv → residue features
* graphs/protein_graph.graphml / .gpickle → saved NetworkX graph
* graphs/1AOS_graph.pt → PyG-ready graph for training
* graph.png → image of the graph (colored by hydrophobicity)
* requirements.txt` → required packages

---

## How to run

Install dependencies with:

```
pip install -r requirements.txt
```

Then install PyTorch Geometric (CPU version) with:

```
pip install torch-scatter torch-sparse torch-geometric -f https://data.pyg.org/whl/torch-2.0.0+cpu.html
```

Make sure your `.pdb` and `.csv` files are in the correct location, then run the script step-by-step or use your own notebook.

---

## Output

* A residue-level graph with both spatial and sequence-based edges
* Node features include biochemical properties
* Graphs are saved in:

  * `.graphml` and `.gpickle` (for NetworkX)
  * `.pt` (for PyTorch Geometric)
* Visualization image saved as `graph.png`

![graph preview](graph.png)

---

## Planned Extensions

* Use contact maps instead of raw Cα distance
* Optional threshold tuning and edge filtering
* Batch graph creation for large PDB datasets

---

**This is a personal project to explore and preprocess protein structures for machine learning.**
Feel free to fork it, suggest improvements, or open issues!

---
