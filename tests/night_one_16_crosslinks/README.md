# Test case `night_one_16_crosslink`

State mismatch after the (1 -> 2) epoch transition. The attestations for shard
from the previous epoch were included at the current epoch. Those and the ones
from the current epoch are "competing" for the winning root for the crosslink.
The previous epoch should be favored but some clients were favoring the current.
There were also some both realted _and_ unrelated issues with rewards and penalties.

Trinity and ZCLI favored current epoch crosslink instead of previous epoch
crosslink when picking winner. Also associated rewards/penalties issues.

Lighthouse had correct crosslinks but rewards/penalties issues.

## Diffs

### ZCLI

Crosslink 7 and some balances mismatch.

```
bash$ zcli diff state post.ssz bad_post_zcli.ssz 
BeaconState objects A and B are different:
modified: .CrosslinksState.CurrentCrosslinks[7].EndEpoch, from = 0x0; to = 0x1
modified: .RegistryState.BalancesState.Balances[10], from = 0x7736e2199; to = 0x7737f99bd
modified: .RegistryState.BalancesState.Balances[13], from = 0x7736e2199; to = 0x7737f99bd
modified: .RegistryState.BalancesState.Balances[14], from = 0x7736e2199; to = 0x7737f99bd
modified: .RegistryState.BalancesState.Balances[3], from = 0x7736e2199; to = 0x7737f99bd
modified: .RegistryState.BalancesState.Balances[4], from = 0x7736e2199; to = 0x7737f99bd
modified: .RegistryState.BalancesState.Balances[5], from = 0x77370509d; to = 0x77381c8c1
modified: .RegistryState.BalancesState.Balances[6], from = 0x7736e2199; to = 0x7737f99bd
modified: .RegistryState.BalancesState.Balances[7], from = 0x77370509d; to = 0x77381c8c1
```

### Trinity


Crosslink 7 and some balances mismatch.

```
bash$ zcli diff state post.ssz bad_past_trinity.ssz 
BeaconState objects A and B are different:
modified: .CrosslinksState.CurrentCrosslinks[7].EndEpoch, from = 0x0; to = 0x1
modified: .RegistryState.BalancesState.Balances[12], from = 0x77381c8c1; to = 0x77370509d
modified: .RegistryState.BalancesState.Balances[9], from = 0x77381c8c1; to = 0x77370509d
```

### Lighthouse

Balances mismatch.

```
bash$ zcli diff state post.ssz bad_post_lighthouse.ssz 
BeaconState objects A and B are different:
modified: .RegistryState.BalancesState.Balances[0], from = 0x77381c8c1; to = 0x77370509d
modified: .RegistryState.BalancesState.Balances[11], from = 0x77381c8c1; to = 0x77370509d
modified: .RegistryState.BalancesState.Balances[12], from = 0x77381c8c1; to = 0x77370509d
modified: .RegistryState.BalancesState.Balances[1], from = 0x77381c8c1; to = 0x77370509d
modified: .RegistryState.BalancesState.Balances[8], from = 0x7737f99bd; to = 0x7736e2199
modified: .RegistryState.BalancesState.Balances[9], from = 0x77381c8c1; to = 0x77370509d
```