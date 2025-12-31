# Dynamic Equilibrium Spawn System (DESS)

> **A Performance-Responsive Spawn Framework for Cooperative Action Games**

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Version](https://img.shields.io/badge/version-1.0-blue.svg)]()

---

## The Problem

Traditional spawn systems in horde-style games hardcode enemy counts based on player count:

```
spawn_count = base_spawns × player_count_multiplier
```

This creates three fundamental issues:

1. **Binary tuning** — Each team size needs separate balancing (4p vs 8p vs 16p configs)
2. **Difficulty breakpoints** — Adding/removing one player causes dramatic difficulty jumps
3. **Performance ignorance** — Skilled 4-player teams face the same spawns as struggling ones

**Result:** Developers spend extensive time balancing each configuration, and the system still breaks when players join/leave mid-game.

---

## The Solution

DESS responds to **actual team performance** instead of headcount. It measures how fast enemies are being cleared and adjusts spawn rate to maintain consistent pressure.

**Key Innovation:** A single parameter set works across 4–16+ players because the system responds to **clear rate**, not roster size.

### Core Mechanisms

1. **Reactive spawning** — Fast clears → more spawns. Slow clears → fewer spawns.
2. **Weakness targeting** — Spawns concentrate on poorly defended directions, preventing camping.
3. **Saturation caps** — Pressure limits prevent infinite accumulation and force tactical rotation.

---

## Key Observations (Validated via Simulation)

**30 simulation runs across 4/8/16-player configurations with identical parameters:**

| Players | Avg Spawned | Spawn Increase | Win Rate | Peak Active Mobs |
|---------|-------------|----------------|----------|------------------|
| 4       | 2,820       | —              | 50%      | ~215             |
| 8       | 3,795       | +34.5%         | 80%      | ~205             |
| 16      | 4,882       | +73.1%         | 90%      | ~212             |

### What This Means

**Sublinear scaling** — Doubling team size increased spawns by ~30%, not 100%  
**Consistent battlefield density** — All configs maintained ~210 peak active mobs  
**Performance-based difficulty** — Win rates improved with team size through coverage redundancy, not reduced challenge  
**No manual tuning per team size** — Same parameters worked across all configurations

**The system adapts automatically because it responds to outcomes, not inputs.**

### Why Sublinear? (Amdahl's Law for Gameplay)

Like [Amdahl's Law](https://en.wikipedia.org/wiki/Amdahl%27s_law) in parallel computing, adding more players doesn't linearly increase throughput due to:

- **Target competition** — Players compete for the same enemies
- **Spatial constraints** — Can't all engage simultaneously
- **Coordination overhead** — Larger teams face communication bottlenecks

DESS naturally accounts for these diminishing returns by measuring **actual clear rate**, not player count. An efficient 4-player team can face similar spawn rates as an uncoordinated 8-player team.

---

## Applications

DESS works across multiple cooperative game modes:

- **Wave Defense** — Directional pressure prevents camping, forces rotation
- **Escort Missions** — Dual-zone tracking maintains forward momentum, prevents speedrunning
- **Boss Encounters** — Health-inverse spawning scales add phases to damage output
- **Capture-and-Hold** — Multi-zone pressure balances defensive coverage requirements
- **Survival Modes** — Objective health modulation adapts to real-time performance

The same pressure-relief feedback loop applies to all modes—just configure zone definitions and priority weights.

---

## How to Use This Repo

**`dess.md`** — Full technical specification with mathematical formulation, simulation results, and implementation guidance  
**`simulation_results/`** — Visual data from 30 simulation runs

### For Game Developers

Read Section 11 (Implementation Considerations) and Section 9 (Tuning Parameters) for practical integration guidance.

**Quick Start:**
- `P_initial = 100` (starting pressure)
- `α = 0.2` (escalation rate)
- Saturation threshold = `1.8× base pressure`
- Spawn interval = 15 seconds

Tune `P_initial` until Wave 5 feels appropriately challenging, then scale difficulties proportionally.

### For Researchers

See Section 7 (Player-Count Comparative Analysis) for empirical results and Section 13.4 (Future Work) for extension opportunities.

---

## Limitations & Caveats

This is a **mathematical thought experiment** validated through simulation:

- Assumes uniform player skill (1.0× baseline clear rate)
- Perfect target distribution (no coordination overhead modeled)
- Simplified spatial constraints (collision, line-of-sight abstracted)

**The simulation proves the concept; playtesting proves the experience.**

Real-world implementations should expect lower win rates due to human coordination overhead and skill variance.

---

## Citation

```bibtex
@techreport{stuckert2025dess,
  title={Dynamic Equilibrium Spawn System (DESS): A Performance-Responsive Spawn Framework for Cooperative Action Games},
  author={Stuckert, Daniel},
  year={2025},
  institution={Independent},
  note={Version 1.0}
}
```

---

## License

Licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) — Free to use, modify, and distribute with attribution.

---

**Balance once. Adapt automatically.** 🎮
