# GSoC 2026 Final Report: Decentralized Identity Tokens (DIT)

**Contributor:** Khushal Agarwal ([@khushal1512](https://github.com/khushal1512))<br>
**Organization:** AOSSIE, Stability Nexus<br>
**Mentors:** Bruno ([@Zahnentferner](https://github.com/Zahnentferner)), Kanishk Sogani ([@KanishkSogani](https://github.com/KanishkSogani))<br>
**Project page:** [GSoC 2026](https://summerofcode.withgoogle.com/programs/2026/projects/RQpiYggb)<br>
**Repos:** [IdentityTokens-EVM-Contracts](https://github.com/StabilityNexus/IdentityTokens-EVM-Contracts), [IdentityTokens-EVM-Frontend](https://github.com/StabilityNexus/IdentityTokens-EVM-Frontend)<br>
**Live app:** [dit.stability.nexus](https://dit.stability.nexus) (Sepolia testnet)

## Project

DIT lets a person own their identity on-chain. A wallet first creates its main identity, then mints tokens under it that describe them (a degree, a GitHub account, a membership) and one profile token with a username and links. Other users can attest a token to vouch for it, revoke that later, or flag a token they think is fake.

I worked on the Solidity contracts that hold the data and rules, and the Next.js dApp that people use. I followed test driven development and kept PRs small so each one was easy to review, which is why the list below links the main ones and the full list is at the end.

## Work completed

### Smart contracts

- [#84](https://github.com/StabilityNexus/IdentityTokens-EVM-Contracts/pull/84), [#86](https://github.com/StabilityNexus/IdentityTokens-EVM-Contracts/pull/86): moved to a main identity with tokens under it, split the logic into modules, and added the profile token.
- [#88](https://github.com/StabilityNexus/IdentityTokens-EVM-Contracts/pull/88), [#98](https://github.com/StabilityNexus/IdentityTokens-EVM-Contracts/pull/98), [#103](https://github.com/StabilityNexus/IdentityTokens-EVM-Contracts/pull/103): unique usernames, editable profiles and any number of on-chain links, read in pages.
- [#96](https://github.com/StabilityNexus/IdentityTokens-EVM-Contracts/pull/96): paginated attestation views, so the app can list attesters without hitting RPC limits.
- [#100](https://github.com/StabilityNexus/IdentityTokens-EVM-Contracts/pull/100): separate, readable IDs for identities, tokens and profiles (`id-`, `tk-`, `pf-`).
- [#104](https://github.com/StabilityNexus/IdentityTokens-EVM-Contracts/pull/104): an optional donation to AOSSIE on every user action, capped in the contract.
- [#106](https://github.com/StabilityNexus/IdentityTokens-EVM-Contracts/pull/106): a creator can no longer attest their own token, and an identity must be 30 days old to flag.

### Frontend

- [#106](https://github.com/StabilityNexus/IdentityTokens-EVM-Frontend/pull/106), [#111](https://github.com/StabilityNexus/IdentityTokens-EVM-Frontend/pull/111), [#125](https://github.com/StabilityNexus/IdentityTokens-EVM-Frontend/pull/125): connected the app to the contracts with wagmi and viem, moved it to GitHub Pages, and added a local Anvil setup for development.
- [#127](https://github.com/StabilityNexus/IdentityTokens-EVM-Frontend/pull/127), [#129](https://github.com/StabilityNexus/IdentityTokens-EVM-Frontend/pull/129): a product tour for new users and a `/claim` page to reserve a username.
- [#131](https://github.com/StabilityNexus/IdentityTokens-EVM-Frontend/pull/131), [#142](https://github.com/StabilityNexus/IdentityTokens-EVM-Frontend/pull/142): profile editing that only sends changed fields, with any number of links.
- [#123](https://github.com/StabilityNexus/IdentityTokens-EVM-Frontend/pull/123), [#150](https://github.com/StabilityNexus/IdentityTokens-EVM-Frontend/pull/150): an attesters list and a "Who attested" card in place of the old trust score.
- [#133](https://github.com/StabilityNexus/IdentityTokens-EVM-Frontend/pull/133), [#162](https://github.com/StabilityNexus/IdentityTokens-EVM-Frontend/pull/162): token ID search, and token card menus (share, copy ID, transfer, burn, flag) that show the right actions to owners and visitors.
- [#157](https://github.com/StabilityNexus/IdentityTokens-EVM-Frontend/pull/157): the donation checkbox on every action.
- [#115](https://github.com/StabilityNexus/IdentityTokens-EVM-Frontend/pull/115), [#165](https://github.com/StabilityNexus/IdentityTokens-EVM-Frontend/pull/165), [#152](https://github.com/StabilityNexus/IdentityTokens-EVM-Frontend/pull/152): privacy policy, a Terms of Use modal with a required checkbox, and SEO.
- [#147](https://github.com/StabilityNexus/IdentityTokens-EVM-Frontend/pull/147), [#149](https://github.com/StabilityNexus/IdentityTokens-EVM-Frontend/pull/149): custom token types, and attestations with no expiry date.
- [#144](https://github.com/StabilityNexus/IdentityTokens-EVM-Frontend/pull/144), [#145](https://github.com/StabilityNexus/IdentityTokens-EVM-Frontend/pull/145): removed misleading claims, badges and ranks.

### Tests

Every contract change came with Foundry tests in the same PR:

- [#84](https://github.com/StabilityNexus/IdentityTokens-EVM-Contracts/pull/84): tests for the new modular system (about 900 lines).
- [#86](https://github.com/StabilityNexus/IdentityTokens-EVM-Contracts/pull/86), [#88](https://github.com/StabilityNexus/IdentityTokens-EVM-Contracts/pull/88): profile token and username tests.
- [#98](https://github.com/StabilityNexus/IdentityTokens-EVM-Contracts/pull/98), [#103](https://github.com/StabilityNexus/IdentityTokens-EVM-Contracts/pull/103): editable profiles and paginated links.
- [#96](https://github.com/StabilityNexus/IdentityTokens-EVM-Contracts/pull/96): attestation pagination.
- [#100](https://github.com/StabilityNexus/IdentityTokens-EVM-Contracts/pull/100): typed token IDs.
- [#104](https://github.com/StabilityNexus/IdentityTokens-EVM-Contracts/pull/104): donation and deploy tests, which brought patch coverage to 100%.
- [#106](https://github.com/StabilityNexus/IdentityTokens-EVM-Contracts/pull/106): self-attestation and flagging rules.
- [#108](https://github.com/StabilityNexus/IdentityTokens-EVM-Contracts/pull/108): split the single large test file into 13 focused files.

## Final status

DIT now has a modular contract system with typed IDs, editable profiles, attestations, flags and an optional donation, and a live app that enables every flow: create an identity, claim a username, build a profile, mint tokens, attest, revoke, flag, transfer and burn. The contracts were deployed to Sepolia six times, all listed in [Deployment.md](https://github.com/StabilityNexus/IdentityTokens-EVM-Contracts/blob/main/Deployment.md).

Still open: the notification bell ([FE #159](https://github.com/StabilityNexus/IdentityTokens-EVM-Frontend/pull/159)) is in review, and the donation and security fixes go live with the next Sepolia deployment (v0.0.7).

**All my work:** [merged PRs](https://github.com/pulls?q=is%3Apr+author%3Akhushal1512+org%3AStabilityNexus+is%3Amerged+created%3A2026-05-01..2026-10-31) (45) and [issues](https://github.com/issues?q=is%3Aissue+author%3Akhushal1512+org%3AStabilityNexus+created%3A2026-05-01..2026-10-31) (38). I also co-maintain both repos ([MAINTAINERS.md](https://github.com/StabilityNexus/IdentityTokens-EVM-Frontend/blob/main/MAINTAINERS.md)).

## Demo

[Watch the demo video](https://drive.google.com/file/d/1NthwW3dK3Pl__wllUVCvvAGKxXCvgwWi/view)

## What's next

- Get users onto DIT.
- Support multiple chains smoothly, which will be new learning for me.
- An experimental idea: give AI agents access to identities on-chain, so an agent can hold or check a DIT identity.
- Make the contracts and the frontend's wagmi and viem calls more efficient.

GSoC is complete, but I don't see the project as finished. The next version will come from more and more people using it.

## Challenges and learnings

1. Just before the midterm, I found out that what I was building was very close to another project the mentors had in mind, Profiles. Instead of keeping them apart, I adapted and restructured my work so both live in DIT, and made the profile a token of its own. I had to redesign the contracts partway through, that was a challenge but it gave the project a much clearer shape.
2. I built DIT e2e from scratch, from the UI design to the smart contract architecture. I learned and practised wagmi and viem along the way, especially how wallet transactions work, and how to keep actions cheap and efficient for users at scale with reuse, resilience and readability in mind.

## My experience

My experience was really good. Working on one project for a long time helped me understand how contracts and a frontend work together.

I would like to sincerely thank my mentors for reviewing every PR. Thank you Kanishk ([@KanishkSogani](https://github.com/KanishkSogani)) for your mentorship, guidance and PR reviews. You guided me to write smaller, more readable PRs, and talking through ideas with you helped me make better decisions before I started building.

Thank you Bruno ([@Zahnentferner](https://github.com/Zahnentferner)) from you I learned attention to detail and to think from the user's side and your suggestions and constructive feedback made the project better.

My summer was well spent.
