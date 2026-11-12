# TExchange network allowlist

Public trusted validator set: Ed25519 pubkeys + gossip `host:port` only. **No seeds or secrets.**

| File | Purpose |
| --- | --- |
| `network-allowlist.json` | Full permissioned voting set (`TEX_VALIDATORS`) + `core` bootstrap list |
| `core-validators.json` | Stable dial targets only — remotes use these for `TEX_CONSENSUS_PEERS` / catch-up |

## Joiners

```bash
# Full set (required for voting after admission)
curl -fsSL https://raw.githubusercontent.com/fortzADA/tex-network-allowlist/main/network-allowlist.json | jq .

# Core dial targets (enough peers to catch up)
curl -fsSL https://raw.githubusercontent.com/fortzADA/tex-network-allowlist/main/core-validators.json | jq .

./scripts/tex-allowlist.sh apply --from \
  https://raw.githubusercontent.com/fortzADA/tex-network-allowlist/main/network-allowlist.json \
  .env
# → TEX_VALIDATORS=everyone, TEX_CONSENSUS_PEERS=core hosts
```

Operators refresh with `./scripts/tex-allowlist.sh publish-branch` from tokenExchange.
