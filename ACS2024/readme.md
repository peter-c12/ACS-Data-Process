## BG → TAZ Allocation Methodology Overview

### Objective

This methodology allocates American Community Survey (ACS) Block Group (BG) household, population, and employment control totals to model Traffic Analysis Zones (TAZs). The framework is designed to preserve aggregate totals exactly, reduce geometric artifacts introduced by boundary misalignment, and support stable travel demand modeling.

---

### Methodological Framework

A layered spatial allocation approach is applied.

**Spatial Intersection**

BG polygons are intersected with TAZ polygons to identify all overlapping BG–TAZ geometries. All area calculations are performed in a projected coordinate reference system to ensure measurement accuracy.

**Area-Based Weighting**

For each BG–TAZ overlap:

- `bg_ratio` represents the proportion of the BG area contained within the TAZ.
- `taz_ratio` represents the proportion of the TAZ area derived from the BG.

Primary allocation weights are derived from `bg_ratio`.

---

### Stability Controls

**Dominance Rule (Threshold = 0.85)**

Where 85 percent or more of a BG lies within a single TAZ, the BG is fully assigned to that TAZ. All other splits are removed.

This rule:

- Reduces artificial boundary-driven splits  
- Minimizes instability in trip generation inputs  
- Improves behavioral consistency  

**Proportional Allocation**

If no TAZ satisfies the dominance threshold, allocations are applied proportionally to spatial overlap. Allocation shares are normalized to ensure that each BG sums to exactly 1.0.

This preserves legitimate multi-zone distributions in dense urban environments.

---

### Manual Override Mechanism

A controlled override file allows specified BGs to be fully assigned to designated TAZs for special land use cases (e.g., parks, military installations, coastline artifacts). Overrides are applied after automated allocation rules.

This mechanism:

- Supports professional planning judgment  
- Avoids distortion of global thresholds  
- Maintains reproducibility and auditability  

---

### Validation

Post-allocation validation confirms that aggregated TAZ totals match original BG control totals exactly.

| Variable | Difference |
|----------|------------|
| TOT_HH   | 0 |
| HH_POP   | 0 |
| TOT_POP  | 0 |
| EMP_RES  | 0 |

No loss, duplication, or rounding drift was observed, confirming full mass preservation.

---

### Conclusion

The final allocation framework preserves statistical integrity while reducing geometric noise and improving model stability. The methodology is suitable for production-level travel demand model integration and supports transparent, reproducible implementation.

