Part 1: Description of the key exchange protocol
================================================

The key exchange protocol can be divided in three phases.

### Phase 1:

The first Phase of the key exchange protocol has the tasks to Start the key exchange and clarify wether public keys have to be exchanged. The proceeding is shown between Alice and Bob in the following list:

1. Alice starts key exchange. Therefore she sends a notice to Bob inclusive the fingerprint of Bob's public key (If she has a public key for Bob).
2. Bob receives the notice. If there is no fingerprint, Bob knows, that he has to send his public key in phase 2. Otherwise he checks the fingerprint and continue the key exchange. Therefor he sends a notice to Alice inclusive the fingerprint of Alice's public key (If he has a public key for Alice).
3. Alice receives the notice to continue the key exchange. If there is no fingerprint, Alice knows, that she has to send her public key in phase 2. Otherwise she checks the fingerprint and continue the key exchange. Therefore she sends a notice to Bob. After that she starts phase 2 (if one or two public keys have be exchanged) or phase 3.
4. Bob receives the notice and starts phase 2 (if one or two public keys have be exchanged) or phase 3.

### Phase 2:

The second phase of the key exchange protocol has the task to exchange the public keys of the communication partners, if necessary. If both partners are in the ownership of the public keys, this phase can be skipped. This phase is symmetric. So in the following we only describe the protocol for Alice's side.

1. Alice sends her public key in multiple notices to Bob if necessary and waits for a confirmation of receipt.
2. Alice imports Bob’s public key if he sends it and she is waiting for it. After that she sends an confirmation of receipt.
3. Alice receives a confirmation of receipt from Bob and knows that Bob has now her public key.
4. If Alice knows that both communication partners has the public key of the other, she starts phase 3.

**Important Comment:** Some of the steps 1-3 can be simultaneous, but the 4. step is after step 1-3.

### Phase 3:
The third phase of the key exchange protocol has the tast to exchange the parts of the symmetric key and calculate the whole symmetric key. This phase is symmetric. So in the following we only describe the protocol for Alice's side.

1. Alice calculates her part of the symmetric key and sends it in multiple notices asymmetrically encrypted and signed to Bob.
2. Alice receive Bob’s part of the symmetric key and stores it.
3. Alice XOR both parts to generate the symmetic key and send a confirmation of receipt to Bob.
4. Alice receives a confirmation of receipt from Bob and knows that Bob has the symmetric key.
5. fter sending and receiving the confirmation of receipt, Alice set the new symmetric key for communication with Bob and finishs phase 3.

**Important Comment:** Some of the steps 1-4 can be simultaneous, but the 4. step is after step 1-5.
