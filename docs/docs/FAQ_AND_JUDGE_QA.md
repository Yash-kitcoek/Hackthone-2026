# Judge Q&A

> Answers are conditional on implementation status. Before judging, update each answer with real evidence from [PROJECT_AUDIT.md](PROJECT_AUDIT.md) and [RESULTS.md](RESULTS.md). Don't state anything marked UNVERIFIED as fact.

**Q1. Why does this problem matter?**  
Some high-security networks only permit one-way observation, yet still need threat detection. Active tools can't be used. (Sponsor details are not claimed; official statement UNVERIFIED.)

**Q2. Why is unidirectional traffic difficult?**  
Handshake completion, RTT, server responses, NXDOMAIN, certificates and upload/download ratios need both directions. We list which features remain observable in DETECTOR_DESIGN.md.

**Q3. How is this different from Snort/Suricata?**  
Those are capable IDS tools; many rules assume full sessions. Our focus is explicit feature-availability handling, evidence alerts and measuring the one-way penalty. We have not benchmarked against them (UNVERIFIED unless done).

**Q4. Why six detectors rather than one model?**  
Threats have different observables and time scales. Specialised detectors give interpretable evidence and let us disable those whose features aren't available.

**Q5. Why LightGBM/scikit-learn?**  
Tabular features, small fast models, easy explanation. Choice is proposed; show the baseline comparison we actually ran.

**Q6. How good is your dataset quality?**  
Public datasets have known issues (label problems, age, testbed artefacts). We use time/family splits and rebuild features from PCAP. Real-network performance is not claimed.

**Q7. What about false positives?**  
We measure FPR on benign traffic, choose thresholds on validation data, and use severity tiers. Current FPR: NOT YET MEASURED unless Results is filled.

**Q8. Can you detect malware in encrypted traffic?**  
No. We flag suspicious metadata patterns only. We never claim decryption or definitive malware identification.

**Q9. How do you detect DGA?**  
Lexical features (length, entropy, n-grams) and query rates. Held-out DGA families test generalisation. Dictionary-based DGAs are harder.

**Q10. How do you detect DNS tunnelling one-way?**  
Long/high-entropy labels, many unique subdomains, high query rate from queries alone. Responses are unavailable if only queries are mirrored.

**Q11. Is it real-time?**  
Designed for streaming. Measured throughput/latency: NOT YET MEASURED unless Benchmarks is filled. We won't state numbers without a run.

**Q12. How do you enforce read-only?**  
Internal Docker network, read-only FS, dropped capabilities, no send code, plus an egress test. Docker isn't a hardware diode.

**Q13. What's your threat model?**  
See THREAT_MODEL.md: malformed packets, evasion, poisoning, alert flooding, egress from the enclave.

**Q14. How do you prevent data leakage?**  
Time/family splits, de-duplication, training-only preprocessing, no random flow splits.

**Q15. Is it reproducible?**  
Pinned versions, seeds, dataset hashes, deterministic replay. Verification status per audit.

**Q16. What is novel?**  
Candidates: the three-configuration directional-blindness evaluation and test-backed read-only design. We haven't completed a prior-work survey, so we don't claim first-ever.

**Q17. Show evidence for the novelty claim.**  
We can show our experiment tables and isolation tests if completed; otherwise we state they are planned.

**Q18. Can it scale?**  
Prototype is single host. Scaling would need load tests and possibly Redis Streams/multiple workers; not yet measured.

**Q19. How would it be deployed?**  
Behind a TAP/SPAN receive-only port in an enclave, with API in a management zone. Prototype only today.

**Q20. Why feasible in a hackathon?**  
Public data, standard libraries, build order from simplest detectors. Scope cut-offs are defined in ROADMAP.md.

**Q21. What are the current limitations?**  
See LIMITATIONS_AND_RISKS.md; mention unmeasured items honestly.

**Q22. What's the future development?**  
Live sensor tests, calibration, more data, SOC export from the management zone only.

**Q23. Why not use a deep-learning model?**  
Little labelled data, need for explainability and small footprint. Could be tested as an additional baseline.

**Q24. Is the confidence a probability?**  
No, not unless calibration is evaluated. The alert field confidence_type states this.

**Q25. Why no automatic blocking?**  
Policy and safety: blocking needs a path back and could break isolation or cause outages. Alerts go to humans.

**Q26. How do you handle scanning without seeing RST/SYN-ACK?**  
We use destination fan-out and attempt rate from outbound SYNs. Failed-connection signals are unavailable.

**Q27. How do you handle slow/low-and-slow attacks?**  
Longer windows and baselines help, but evasion is possible. This is a stated limitation.

**Q28. What if the sensor sees only server→client?**  
Config SENSOR_DIRECTION flips; the availability table changes and detectors degrade accordingly. Needs testing.

**Q29. Did you test on a real data diode?**  
No, unless stated in Results. Our experiments simulate the restriction on datasets and are labelled that way.

**Q30. Why not blockchain, given the theme?**  
No verified requirement for it; adds complexity. We'd revisit if the official statement requires it.

**Q31. Why not use blockchain, given the theme is Blockchain & Cybersecurity?**  
The problem statement is about detecting threats in one-way traffic, and we found no requirement for a ledger (portal text to be rechecked). A distributed ledger would add latency and complexity without helping detection. Where integrity matters we propose a simple hash-chained alert log, which is optional and planned, not claimed as built.

**Q32. How do you avoid alert floods?**  
Deduplication, aggregation per window and rate limits (planned).

**Q33. What privacy risks exist?**  
PCAPs and IPs are sensitive; we use public/synthetic data and follow SECURITY.md.

**Q34. What was actually implemented?**  
Answer strictly from PROJECT_AUDIT.md and RESULTS.md. Never from this Q&A.

**Q35. Is your hash-chained log a blockchain?**  
No. It is a tamper-evident log: each alert includes the hash of the previous one. There is no consensus or distributed network. It detects edits after storage, but only if the latest hash is kept somewhere the attacker cannot write.

**Q36. Can an attacker with database access just rebuild the chain?**  
Yes, unless the head hash is anchored externally (offline record or signature with a key outside the enclave). We state this limit; the anchoring choice is undecided.

**Q37. Does the hash chain prove an alert is correct?**  
No. It only shows the stored alert was not changed afterwards. Correctness comes from detector evaluation.

