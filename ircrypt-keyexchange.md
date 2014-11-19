Part 1: Description of the key exchange protocol
================================================

The key exchange protocol can be divided in three phases.

### Phase 1:

The first Phase of the key exchange protocol has the tasks to Start the key exchange and clarify wether public keys have to be exchanged. The proceeding is shown between Alice and Bob in the following list:

 1. Alice starts key exchange. Therefore she sends a notice to Bob inclusive the fingerprint of Bob's public key (If she has a public key for Bob).
 2. Bob receives the notice. If there is no fingerprint, Bob knows, that he has to send his public key in phase 2. Otherwise he checks the fingerprint and continue the key exchange. Therefor he sends a notice to Alice inclusive the fingerprint of Alice's public key (If he has a public key for Alice).
 3. Alice receives the notice to continue the key exchange. If there is no fingerprint, Alice knows, that she has to send her public key in phase 2. Otherwise she checks the fingerprint and continue the key exchange. Therefore she sends a notice to Bob. After that she starts phase 2 (if one or two public keys have be exchanged) or phase 3.
 4. Bob receives the notice and starts phase 2 (if one or two public keys have be exchanged) or phase 3.
