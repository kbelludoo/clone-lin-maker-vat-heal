# clone-lin-maker-vat-heal

Experimental **LIN** clone of MakerDAO / Sky `Vat.heal` — the Dai and USDS
surplus-buffer settlement kernel (unsigned `_sub` of `sin`/`dai`/`vice`/`debt`
by the same `rad`).

**Proofs live in [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open)** — this repo is the LIN copy only.

- **Upstream (hash-pinned, not vendored):** [makerdao/dss](https://github.com/makerdao/dss) `fa4f6630afb0624d04a003e920b0d71a00331d98`
  - `src/vat.sol` sha256 `9016fd94f0f1b014abf184edab86a3f5843042b17e3734407e0f0fabb920f49f` blob `ff90bbed5b36e54318bd5461cbf32e4167df2b28`
  - License AGPL-3.0-or-later. This repository does **not** vendor the Solidity source.
- **LIN kernel:** [`src/lin_maker_vat_heal.lin`](src/lin_maker_vat_heal.lin) (identical to lin-open)
- **C11 oracle copy:** [`test/oracles/maker_vat_heal_c11.c`](test/oracles/maker_vat_heal_c11.c)
- **Proofs (lin-open only):** `examples/maker_vat_heal/` and `make maker-vat-heal-proof`
- **Class:** EXPERIMENTAL uint64-scale, `RAY' = 1e9`. Not mainnet `RAY=1e27`. Not wad×ray rad. Not a production vat replacement.

Named goldens: VOW heal `rad=1e18` on `sin=2e18 dai=3e18 vice=2e18 debt=5e18` → **heal_ok=1**;
FULL_SETTLE `rad=vice=2e18` → **new_vice=0**, **settled=2e18**, leftover dai `1e18`;
four-way identity Δsin=Δdai=Δvice=Δdebt=rad; no `live`/`auth` (unlike `frob`/`suck`);
naive i64 `7e18+3e18` wraps to **-8446744073709551616**; checked `u_add` fail-closes to **0**.

## Reproduce proofs (in lin-open)

```bash
make maker-vat-heal-proof
# or: python3 test/prove_maker_vat_heal_external.py
```

## Not claimed

Uint256 / RAY=1e27 / wad×ray rad mainnet parity.
LIN replacing Maker, Sky, vat, Vow, or the EVM. TVL or dollar savings. zk soundness.
`wish` / `wards` mappings. `vat.grab` (see clone-lin-maker-vat-grab). `vat.frob` (see clone-lin-maker-vat-frob).
