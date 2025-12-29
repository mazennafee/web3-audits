# Smart Contract Audit Checklist
Professional workflow for Immunefi bug bounties and Solidity audits.

## High-Level Audit Steps

1. **Scope Review**  
   Read Immunefi program page, project docs, and README. Confirm in-scope contracts only (ignore out-of-scope). Note versions, dependencies, and deployment networks.

2. **Architecture Mapping**  
   Diagram protocol flows, contracts, external calls (oracles, bridges), and user journeys. Use Excalidraw or Solidity Metrics for visualizations. Identify trust assumptions and attack surfaces.

3. **Automated Static Analysis**  
   Run Slither, Mythril, and Solhint. Record all findings with file:line references. Export JSON for triage.

4. **Fuzzing & Invariant Testing**  
   Set up Echidna or Foundry fuzz tests. Define 5-10 key invariants (e.g., totalSupply consistency). Run 1M+ iterations; review corpus for edge cases.

5. **Unit & Integration Testing**  
   Use Hardhat/Foundry to write/run tests. Achieve 90%+ coverage. Fork mainnet for integration tests; check for reverts and state changes.

6. **Line-by-Line Manual Review**  
   Read every contract line-by-line. Check:  
   - Access control (RBAC, onlyOwner)  
   - Math (overflows, SafeMath usage)  
   - Upgradeability (proxy patterns)  
   - Oracles/externals (freshness, manipulation)  
   - Liquidity/AMM (sandwich, flashloan)  
   - Reentrancy, front-running, DoS  
   Use Solodit/Tincho checklists as reference. Annotate code with comments.

7. **Findings Triage & Severity**  
   Deduplicate issues. Assign severity: Critical/High/Medium/Low/Informational per Immunefi guidelines. Write PoC for each. Re-test fixes. 

8. **Report Generation**  
   Use template: Executive Summary, Findings Table, Recommendations, Appendix (tools output). Submit to Immunefi.

## Tools Inventory & Usage Schedule

| Category          | Tools                  | When Used (Step) | Command Example |
|-------------------|------------------------|------------------|-----------------|
| Static Analysis   | Slither, Mythril, Solhint | 3 | `slither . --json output.json`  |
| Fuzzing/Invariants| Echidna, Foundry Invariants | 4 | `forge test --fuzz-runs 10000`  |
| Testing Frameworks| Hardhat, Foundry     | 5 | `forge test --coverage`  |
| Visualization     | Excalidraw, slither-analyzer | 2 | N/A  |
| Manual Reference  | Solodit, SWC Registry | 6 | Browser search  |
| Reporting         | Markdown template     | 8 | N/A |

## Pro Tips for Professional Audits
- **Time Allocation**: 10% scope/arch, 20% automation, 50% manual review, 20% report.  
- **Version Control**: Git commit after each step with `git commit -m "step-3-slither-complete"`.  

