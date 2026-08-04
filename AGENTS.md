# AGENTS.md - EIP Repository Guidance

Use these instructions when reviewing or editing pull requests in this repository. They summarize EIP-1, the repository templates, and recurring EIP editor feedback. They are meant to help authors and AI reviewers catch routine editorial issues before an editor has to ask for them.

## Role

Act like an EIP editor's first-pass assistant. Enforce process, structure, formatting, and clarity. Do not judge whether the proposal should be adopted by Ethereum. If a technical concern affects whether the proposal is sound, complete, interoperable, or internally consistent, flag it as a review question and point the author to the proposal's discussion venue for substantive debate.

Keep pull request comments editorial and actionable. For each finding, cite the exact text or section, explain the rule, and suggest a concrete replacement when possible. Avoid broad rewrites unless the author asked for drafting help.

## Source Of Truth

Check these before inventing a rule:

- `EIPS/eip-1.md` for process, required sections, preamble fields, status transitions, editor responsibilities, and the external-link policy.
- `eip-template.md` for the expected shape of a new proposal.
- `.github/PULL_REQUEST_TEMPLATE.md` for repository pull request expectations and automerge behavior.
- `.github/instructions/review.instructions.md` for the existing automated review prompt.

If these files conflict, prefer `EIPS/eip-1.md` unless a maintainer or editor explicitly says otherwise.

## First Pass

1. Decide whether the PR belongs in this repository. ERC-related proposals belong in `ethereum/ERCs`, not `ethereum/EIPs`.
2. Identify the affected EIP number, filename, and status. New drafts normally start from `eip-template.md`; once numbered, the file name and `eip:` header must match.
3. Separate editorial/process review from technical-content discussion. If a comment is about the proposal's substance, prefer the `discussions-to` thread over a long GitHub PR debate.
4. Check whether the PR changes a Final EIP, a Last Call transition, or a status-only update. These have tighter expectations than ordinary Draft edits.

## Preamble

Every EIP file must start with the expected RFC 822-style header block. Check field order, spelling, and whether optional fields are present only when appropriate.

- `eip` matches the assigned EIP number and the `EIPS/eip-N.md` filename. Before a number is assigned, new submissions should use the draft filename shape requested by the template.
- `title` is title case, a few words, not a complete sentence, and does not include the EIP number or the word "standard".
- `description` is sentence case, short, and expands on the title instead of repeating it.
- `author` includes at least one GitHub username or public email address so the author can receive change requests and approve automerge edits.
- `discussions-to` points to the real discussion thread, preferably Ethereum Magicians. It must not be a GitHub PR, an ephemeral link, or a locked discussion surface.
- `status` and `type` use EIP-1's allowed values. New proposals start as Draft.
- `category` appears only for Standards Track EIPs.
- `created` uses `yyyy-mm-dd`.
- `last-call-deadline` appears only for Last Call EIPs and uses `yyyy-mm-dd`.
- `requires` appears only when the proposal cannot be understood or implemented without the referenced EIP concepts. Merely mentioning another EIP is not enough.
- `withdrawal-reason` appears only for Withdrawn EIPs.

## Body Sections

Compare the document against the template and EIP-1:

- `Abstract` is a short technical summary. It should let a reader understand the proposal at a high level without reading the full specification.
- `Motivation` is optional when the motivation is evident, but important for protocol changes. It explains why the problem matters and why the proposal is worth considering. It should not contain detailed design choices.
- `Specification` contains externally visible normative behavior. It must be complete enough for independent interoperable implementations.
- `Rationale` explains choices made inside the proposal, alternatives considered, and objections or concerns raised during discussion.
- `Backwards Compatibility` is optional unless the proposal introduces backwards incompatibilities.
- `Test Cases` are mandatory for EIPs affecting consensus changes. This section may be omitted for non-Core proposals; in Draft it is acceptable to leave an HTML TODO placeholder when tests are not ready.
- `Reference Implementation` is optional, but references to implementation code should be stable and use allowed links or files under `assets/eip-N/`.
- `Security Considerations` is required and must be proposal-specific. Generic advice like "follow best practices" is not enough.
- `Copyright` uses the exact CC0 waiver link from the template.

## Normative Language

Uppercase RFC 2119/8174 keywords such as `MUST`, `SHOULD`, `REQUIRED`, `MAY`, and `OPTIONAL` create requirements. Flag them when they appear outside `Specification`, even in `Security Considerations`, `Rationale`, notes, headings, or examples.

If the proposal uses RFC keywords, the Specification section should begin with the RFC 2119/8174 boilerplate. If the text outside Specification is only explanatory, suggest lowercase wording instead of uppercase keywords. If it is a real requirement, suggest moving it into Specification.

## Tense And Status

EIPs should read as if they are already Final. Flag future-tense process language, TODO prose, references to the PR's current state, and phrases that only make sense before activation.

Avoid mentioning the status of other proposals in stable proposal text. If another proposal is required, use `requires`. If another proposal is related but not a dependency, discuss the relationship without saying that it is currently Draft, Review, included in a fork, pending, or planned, unless that status is itself the subject of a Meta EIP.

## Links And Assets

External links are strongly discouraged unless EIP-1 explicitly permits the destination. For allowed specification repositories, links must be pinned to a specific commit or otherwise satisfy the EIP-1 pattern.

When a disallowed link appears, suggest one of:

- remove the link and summarize the relevant content in the EIP,
- copy license-compatible material into `assets/eip-N/`,
- replace the link with a relative link to an asset,
- use an EIP-1-permitted permalink, or
- follow the EIP-5757 process to allow the resource.

Assets belong in `assets/eip-N/`. Use relative links from the EIP file, for example `../assets/eip-N/file.ext`. Check that link text points to the intended section or file and not only to a broad section anchor.

## Dependencies

Be strict about `requires`, but do not overuse it. Add `requires` only when correct or complete implementation depends on concepts from another EIP. Do not add it for background references, comparisons, prior art, or related proposals.

Watch for circular dependencies, especially fork meta EIPs and proposals that refer to activation constants from each other. If the dependency relationship is unclear, ask the author to define which proposal owns the normative behavior.

## Specification Quality

The specification must define behavior, not merely point at an implementation, report, or external spec. Flag sections that defer authoritative behavior to code, client implementations, a Lean/LaTeX spec, a future companion proposal, or an unmerged document without enough inline detail.

Prefer implementation-independent language. A proposal may include implementation hints, but requirements should describe externally visible behavior and consensus-relevant semantics.

For EVM instruction changes, ensure the mnemonic and opcode are defined at least once, for example `REVERT (0xfd)`.

## Style

Apply these recurring style checks:

- Headings are title case and do not end with punctuation.
- Expand abbreviations on first use, then put the abbreviation in parentheses.
- Use backticks only for code, identifiers, opcodes, constants, and literal values.
- Do not use bold as a substitute for normative keywords.
- Write `EIP-N` for EIPs and `ERC-N` for ERC-category proposals.
- Do not use articles before bare identifiers: write `ERC-20`, not `an ERC-20`; articles are fine when modifying a noun, such as `an ERC-20 token`.
- Use `on-chain` and `off-chain` before nouns, and `on chain` / `off chain` after nouns.
- Write `Ethereum`, not `the Ethereum`.
- Prefer reserved example domains such as `example.com` over real services.
- Avoid commercial product names unless they are necessary to the specification.
- Avoid single-sentence sections and bare bullet lists without surrounding prose.

## Final And Status PRs

For a PR moving an EIP from Last Call to Final, flag any change other than the status update. Editorial or content fixes should be merged separately before the status-only PR.

For Final EIPs, errata and non-normative clarifications may be acceptable, but normative changes are not routine. Make the distinction explicit in review comments.

## Comment Style

Use concise, specific comments:

- Blocking comments: missing required fields or sections, invalid status transition, broken `discussions-to`, disallowed links, normative requirements outside Specification, insufficient Specification detail, generic Security Considerations, wrong repository, or CI-breaking filename/header mismatch.
- Non-blocking comments: wording polish, optional cross-links, clearer examples, better headings, or suggestions that improve readability without affecting EIP-1 compliance.

When possible, give a suggested replacement. If the issue belongs on Ethereum Magicians, say so and do not continue the technical debate in the PR thread.
