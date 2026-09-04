# CCP Prototype

CCP is a research prototype for solving a constrained preference/equilibrium problem while keeping participant preferences hidden until the appropriate stage. The implementation is intentionally small and is useful for experimenting with commitment, preference evaluation, and equilibrium search rather than as a production cryptographic protocol.

## Components

| File | Role |
|---|---|
| `preference.py` | Defines the preference-function abstraction used by participants. |
| `crypto.py` | Implements the sealed-commitment demonstration and commitment rules. |
| `solver.py` | Searches for an equilibrium and returns an `EquilibriumResult`. |
| `demo.py` | Runs a human-readable example of the protocol. |
| `interactive.py` | Provides an interactive way to configure or inspect an example. |
| `test_ccp.py` | Tests the solver, including the regression case that exposed a greedy-search bug. |

## Running the prototype

Use Python 3. The repository has no dependency manifest, so the core demonstration currently relies on the standard library.

```bash
python demo.py
python interactive.py
python -m unittest discover -v
```

If the test module is intended to be run directly, `python test_ccp.py` is also supported by the local test layout.

## Model and limitations

A participant supplies a preference function and commits to it before the solver evaluates the collective problem. The commitment demonstration protects the value from casual inspection, but this repository should not be described as a formally audited cryptographic implementation. Review `crypto.py` before making security claims.

The prototype is best extended by adding typed input validation, property-based tests for solver invariants, complexity measurements, and a formal statement of the equilibrium conditions. Keep the mathematical model in `preference.py` and the search strategy in `solver.py` separated so experiments remain comparable.
