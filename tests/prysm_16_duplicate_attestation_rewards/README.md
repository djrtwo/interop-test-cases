# Test case `prysm_16_duplicate_attestation_rewards`

State mismatch after the (1 -> 2) epoch transition.

This state was formed on a Prysm <-> Trinity 16 val (split) testnet.
Prysm was aggregating attestations, but Trinity was not. This led to some
attestations being included more than once (some as aggregated while others as
singles). This caused an error in Prysm that led to duplicate rewards being
applied for each duplicated attestation. This was because they were not using a
`set` operation to de-duplicate indices in `get_unslashed_attesting_indices`.

## Diffs

### Prysm

Balances mismatch.

```
bash$ zcli diff state post.ssz bad_post_prysm.ssz
BeaconState objects A and B are different:
modified: .RegistryState.BalancesState.Balances[0], from = 0x773859b08; to = 0x77395fbac
modified: .RegistryState.BalancesState.Balances[10], from = 0x7736fc4dc; to = 0x773802580
modified: .RegistryState.BalancesState.Balances[11], from = 0x77370b96e; to = 0x773811a12
modified: .RegistryState.BalancesState.Balances[12], from = 0x773813d00; to = 0x773919da4
modified: .RegistryState.BalancesState.Balances[13], from = 0x77371d0f0; to = 0x773823194
modified: .RegistryState.BalancesState.Balances[14], from = 0x7736fc4dc; to = 0x773802580
modified: .RegistryState.BalancesState.Balances[1], from = 0x77372e872; to = 0x773834916
modified: .RegistryState.BalancesState.Balances[2], from = 0x7736fc4dc; to = 0x773802580
modified: .RegistryState.BalancesState.Balances[3], from = 0x77370b96e; to = 0x773811a12
modified: .RegistryState.BalancesState.Balances[4], from = 0x77370b96e; to = 0x773811a12
modified: .RegistryState.BalancesState.Balances[5], from = 0x773751776; to = 0x77385781a
modified: .RegistryState.BalancesState.Balances[6], from = 0x7736fc4dc; to = 0x773802580
modified: .RegistryState.BalancesState.Balances[7], from = 0x77371f3e0; to = 0x773825484
modified: .RegistryState.BalancesState.Balances[8], from = 0x773813d00; to = 0x773919da4
modified: .RegistryState.BalancesState.Balances[9], from = 0x773836c04; to = 0x77393cca8
```