# SciDocGym v0.1 Licensing and Redistribution Policy

## 1. Scope

This policy governs licensing, provenance, admission, and redistribution of:

* SciDocGym source code;
* SciDocGym documentation and schemas;
* source scientific articles;
* figures, graphics, media, supplementary files, and other source assets;
* derived PDFs, HTML, JATS-RL, DoclingDocument files, annotations, and benchmark artifacts.

No source article may enter the SciDocGym corpus without a valid machine-readable rights record.

## 2. SciDocGym-owned material

SciDocGym source code, tests, command-line tools, and software components are licensed under:

`0BSD`

SciDocGym-authored documentation, schemas, manifests, and metadata are dedicated under:

`CC0-1.0`

Third-party material is never relicensed by SciDocGym. Its original license and copyright status remain authoritative.

## 3. Admissible source article licenses

SciDocGym v0.1 uses a strict allowlist.

An article is admissible only when its verified article-level license is exactly one of:

* `CC0-1.0`
* `CC-BY-4.0`

The following are not admissible in v0.1:

* CC BY-NC;
* CC BY-ND;
* CC BY-NC-ND;
* CC BY-NC-SA;
* CC BY-SA;
* custom licenses;
* publisher-specific reuse terms;
* licenses that cannot be unambiguously mapped to an allowed SPDX identifier;
* missing or ambiguous license information.

Public availability, free-to-read status, presence in PMC, or membership in the PMC Open Access Subset is not by itself evidence of admissibility.

## 4. PMC verification

Every PMC article must be verified individually.

For each candidate article the admission process must:

1. record the PMCID and DOI when available;
2. record that the source was retrieved from an authorized PMC dataset service;
3. retain the original JATS XML and its SHA-256 digest;
4. extract the article-level rights statement from JATS;
5. extract the canonical license reference when present;
6. normalize the license to an SPDX identifier;
7. compare that identifier with the v0.1 allowlist;
8. inspect asset-specific rights information;
9. create a machine-readable rights record;
10. reject admission if any mandatory rights information remains ambiguous.

PMC Open Access Subset membership may be recorded as supporting provenance but must never replace article-level license verification.

## 5. Figures and other assets

Rights are evaluated independently for every asset included in the SciDocGym-supported document content.

This includes at least:

* figures;
* graphics;
* photographs;
* tables supplied as external assets;
* video or audio;
* supplementary material;
* externally referenced files.

An explicit asset-level rights statement overrides the article-level license.

An asset may inherit the article-level license only when:

* no conflicting asset-specific license or copyright statement exists;
* no statement indicates third-party ownership or separate permission requirements;
* the article license applies to that asset;
* the inheritance decision is recorded in the rights record.

An asset with unknown, ambiguous, non-commercial, no-derivatives, all-rights-reserved, permission-only, or otherwise incompatible terms must not be redistributed.

For SciDocGym v0.1, if such an asset is referenced by content that would enter JATS-RL or a generated benchmark document, the entire article is rejected.

Assets outside the supported JATS-RL content may be omitted, but their omission and rights status must be represented in the rights record.

## 6. Derived artifacts

SciDocGym does not claim ownership of source article content merely because that content has been transformed.

Derived artifacts containing CC BY 4.0 article content must retain:

* source attribution;
* the original CC BY 4.0 notice;
* provenance to the source article;
* an indication that the representation was transformed by SciDocGym.

Derived artifacts based exclusively on CC0 material may themselves be distributed under CC0 where applicable.

SciDocGym-authored metadata that is separable from source content is released under CC0-1.0.

## 7. Mandatory rights record

Every admitted article must have exactly one machine-readable rights record conforming to the versioned SciDocGym rights schema.

The record must identify:

* policy/schema version;
* PMCID;
* DOI when available;
* source provider;
* source retrieval method;
* retrieval timestamp;
* source hashes;
* article license SPDX identifier;
* canonical license reference;
* original rights statement or evidence reference;
* copyright holder and year when available;
* verification status and timestamp;
* every included asset;
* the effective license of every included asset;
* whether that license is explicit or inherited;
* whether the asset is redistributable;
* evidence supporting the asset rights decision;
* the final corpus admission decision and reason.

Unknown values must be represented explicitly. They must never be silently interpreted as permissive rights.

## 8. Admission invariant

An article is admitted if and only if:

`article_license ∈ {CC0-1.0, CC-BY-4.0}`

AND

`rights_record_valid == true`

AND

`article_rights_verified == true`

AND

for every source asset included in the supported SciDocGym representation:

`asset.redistributable == true`

AND

`asset.license ∈ {CC0-1.0, CC-BY-4.0}`

AND

all required provenance and hashes are present.

Failure of any condition rejects the article.

There is no permissive fallback.

## 9. Conflicts and ambiguity

Explicit narrower rights always override broader inherited rights.

When PMC metadata, JATS metadata, publisher statements, or asset-specific statements conflict, admission must fail with a structured diagnostic.

Ambiguous rights must never be resolved automatically in favor of redistribution.

## 10. Enforcement

The corpus build must run the rights validator before an article is materialized into the canonical corpus.

A failed rights check must:

* return a non-zero result;
* prevent corpus admission;
* produce a structured diagnostic;
* preserve sufficient evidence for review.

CI must contain positive and negative fixtures proving these rules.

## 11. Policy versioning

Rights records must contain the policy version used for their admission decision.

A change to:

* the allowed license set;
* inheritance rules;
* asset handling;
* required evidence;
* admission semantics

requires a policy version change and revalidation of the affected corpus.

