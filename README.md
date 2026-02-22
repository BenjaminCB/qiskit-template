# Qiskit + Nix Devenv Template (IBM Quantum + Jupyter)

A GitHub template for a reproducible Qiskit development environment using Nix
and devenv.

## What’s in this repo

### Environment / tooling

- **Nix + devenv** environment definition:
  - `devenv.nix` – packages, Python setup, and shell hooks
  - `devenv.yaml`, `devenv.lock`, `.devenv.flake.nix`, `.devenv/` – devenv
    internals / lockfiles
- **direnv integration**
  - `.envrc` – automatically loads the devenv shell when you `cd` into the repo
    (after `direnv allow`)
- **Python project / dependency lock**
  - `pyproject.toml` – project metadata + dependencies
  - `uv.lock` – pinned Python dependencies.

### Notebook

- `bell.ipynb` – a minimal notebook that:
  - loads secrets via `python-dotenv`
  - saves / loads IBM Quantum account config using `QiskitRuntimeService`
  - lists available IBM backends
  - runs a Bell circuit:
    - with Aer (optionally with a noise model derived from an IBM backend)
    - with IBM Runtime (`SamplerV2`) on a real backend

## Prerequisites

You’ll need:

1. **Nix** (see https://nixos.org/download/)
2. **devenv** (see https://devenv.sh/getting-started/)
3. **direnv** (optional but recommended, see https://direnv.net/)
   - makes entering the environment automatic

## Setup

- On github there should be a button `Use this template`, use that to create a
  new repository.
- clone the repo.
- cd qiskit-template

### Option A: Use direnv (recommended)

direnv allow

This evaluates .envrc, which runs use devenv, which drops you into the fully
configured dev shell.

From now on this happens automatically every time you cd into the directory.

### Option B: Manual shell

devenv shell

Either way, on entry you should see the hello from devenv message and a git
--version line (from enterShell).

## IBM Quantum setup (token + instance / CRN)

The notebook expects two environment variables:

IBM_TOKEN – your IBM Quantum Platform API token

CRN – the “instance” string used by Qiskit Runtime (passed as instance=...)

These can both be found (or created in case of the API token) on the IBM Quantum
Platform.

Create (or edit) a .env file in the repo root:

```
IBM_TOKEN="your_token_here"
CRN="your_instance_or_crn_here"
```

## Running the notebook

Inside the devenv shell: `jupyter lab`

Then open bell.ipynb.
