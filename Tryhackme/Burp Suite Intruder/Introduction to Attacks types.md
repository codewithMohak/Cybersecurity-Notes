The **Positions** tab in Burp Suite Intruder contains a dropdown menu for selecting the attack type. Intruder provides four attack types, each designed for different testing purposes.
### Sniper

The **Sniper** attack type is the default and most commonly used option. It inserts one payload at a time into each selected position in the request. Payloads are tested one by one in a linear manner, making this attack useful for precise and focused testing.

### Battering Ram

The **Battering Ram** attack type sends the same payload to all selected positions at the same time. This is useful for testing race conditions or situations where the same input must be used simultaneously in multiple places.

### Pitchfork

The **Pitchfork** attack type allows testing multiple positions at the same time using different payload sets. Each position gets its own payload set. This is useful when different parameters need separate but synchronized testing.

### Cluster Bomb

The **Cluster Bomb** attack type combines the behavior of Sniper and Pitchfork. It tests all combinations of payloads from multiple payload sets across different positions. This is useful when we want to test every possible combination of inputs together.

Each attack type has its own advantages and is useful for different testing situations. Choosing the correct attack type helps perform more effective testing.