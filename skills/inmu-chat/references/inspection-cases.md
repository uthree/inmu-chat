# Inspection cases

Use these cases with the [main phrase table](phrases.md) and [related phrases](related-phrases.md) to review inspection judgments. They are manual evaluation examples, not measured model accuracy or a guarantee of repeatable output. Expected results describe observations and limits; equivalent wording is acceptable.

## How to judge the cases

Keep three questions separate:

- **Match strength:** Is the wording distinctive, ambiguous, or ordinary in the supplied context? These labels describe the evidence, not numerical probabilities.
- **Attribution:** Is the expression used directly, quoted, or discussed as an example? A quotation can contain a distinctive match without endorsing it.
- **Intent:** What does the supplied context establish? A table match alone cannot establish deliberate meme use, authorship, or provenance.

Ordinary phrases and numbers do not each need a warning in a normal report when there are no supporting cues. A comprehensive review can mention them as weak matches without presenting them as findings that require correction. Insufficient evidence of intent is also insufficient evidence that a match is definitely accidental.

All Japanese snippets below are inspection inputs or quoted evidence. Report explanations and suggested replacements should remain neutral, even when the surrounding conversation uses meme expressions.

## Short cases

Treat each row as an independent input with no additional context.

| ID | Input | Expected observation and reporting | What not to conclude |
| --- | --- | --- | --- |
| S1 | `お問い合わせ番号：114514` | The digits match a listed numeric allusion, but an inquiry number is an ordinary use. No strong finding or required rewrite. | The number proves deliberate meme use, or is definitely accidental. |
| S2 | `該当するデータはないです。` | Ordinary Japanese in context. No strong finding merely because `ないです` is listed. | The writer is quoting the interview. |
| S3 | `この実装、やりますねぇ！` | Report a distinctive candidate: the praise and stylized `ねぇ` match the listed expression. | The spelling proves the writer's intent or a particular source scene. |
| S4 | `文献中に「こ↑こ↓」という表現がある。` | Report the distinctive arrow notation and explicitly mark it as a quotation discussed by the text. | The document's author originated or endorses the quoted wording. |
| S5 | `設定を確認して、どうぞ。` | Note the adapted `〇〇して、どうぞ` pattern only as ambiguous if discussing weak matches. It also works as an ordinary request. No strong finding without further cues. | The pattern alone proves a reference. |
| S6 | `これはまずいですよ！` | The wording matches the table but is also an ordinary warning. Treat as ambiguous; punctuation alone does not justify a strong finding. | The speaker intended a meme or the sentence must be rewritten. |
| S7 | `この処理、速すぎます。` | Ordinary emphasis. No strong finding based on the productive suffix alone. | Every expression meaning “too much” derives from a meme. |
| S8 | `この実装、お前やりますねぇスギ。` | Report a distinctive adapted/chimera candidate matching the related table. | It is a verbatim source line, an AI invention, or evidence of AI authorship. |
| S9 | `こ↑こ↓を確認して、どうぞ。` | Report the distinctive arrow notation and the nearby adapted request together; the combination strengthens recognition of a reference. | Every isolated occurrence of the request pattern elsewhere deserves the same strength. |

## Code comment case

Inspect the comment as text, without executing or changing the code:

```rust
// 該当するデータはないです。
let inquiry_number = 114514;
// この実装、お前やりますねぇスギ。
```

Expected: report line 3 as a distinctive adapted/chimera candidate, quoting only the relevant comment. The ordinary denial on line 1 and the numeric literal on line 2 are not independently strong findings. The nearby distinctive comment can supply context for the number, but still cannot establish why that literal was chosen. Do not claim AI authorship, alter executable values, or rewrite the code during inspection.

## Table case

| Field | Value |
| --- | --- |
| Inquiry number | 114514 |
| Status | 該当するデータはないです。 |
| Example quotation | 文献中に「こ↑こ↓」という表現がある。 |

Expected: use row labels and column names as locations. The inquiry number and status are ordinary in their supplied contexts; do not promote them to strong findings because they share a table with a distinctive quotation. Report the arrow notation in the “Example quotation” row, “Value” column as a distinctive quoted match. Do not infer the table author's intent or endorsement.

## Multi-paragraph case and expected report

The following fictional document is the complete supplied input. Line numbers in the report count from the heading, including blank lines, and exclude the code fence.

```text
# Release review

今週は検索機能の確認を行いました。通常の検索条件、空の結果、読み込み中の表示を順に確認し、担当者ごとに結果を記録しています。問い合わせの追跡用に、お問い合わせ番号：114514 を記録しました。
該当するデータはないです。この結果は空のデータセットを使った確認で、障害を示すものではありません。

レビュー担当者のコメントとして「この実装、やりますねぇ！」という記録がありました。本文では発言を引用しており、採用理由や出典の説明はありません。
文献中に「こ↑こ↓」という表現がある。これは表記の説明に使う引用として記録されています。

次の担当者は設定を確認して、どうぞ。確認後は結果を共有し、問題があれば再現手順と実行環境を追記してください。公開前には引用の必要性と表記を編集担当者が確認します。
```

Assume the user asks for an inspection before publishing this document to a general audience. An acceptable report follows; its prose contains no newly introduced meme expressions. The quoted evidence and candidate names are necessary to identify the findings.

### Expected report

Scope: reviewed the supplied nine-line document, including its heading and quotation context, against both phrase tables. No external documents or source recordings were checked.

| Location | Short excerpt and candidate | Strength and context | Interpretation and optional action |
| --- | --- | --- | --- |
| Line 6, reviewer quotation | Excerpt: `この実装、やりますねぇ！`; candidate: `やりますねぇ！` | Distinctive wording, explicitly quoted from a reviewer. The stylized ending matches the reference table. | It may be recognized as a meme reference, but this text does not establish the reviewer's intent or source. A quotation does not imply endorsement by the document author. For a neutral public summary, consider paraphrasing the whole sentence as `レビュー担当者から、実装を評価するコメントがありました。` if preserving the exact quotation is unnecessary. |
| Line 7, literature quotation | Excerpt and candidate: `こ↑こ↓` | Distinctive arrow notation, explicitly quoted to discuss its spelling. | Readers familiar with the expression may recognize the reference. Its presence serves an explanatory purpose here; retaining it may be appropriate. If the quotation is unnecessary for publication, consider replacing the whole sentence with `文献中の表記例を引用しています。` |

Other matches considered: the inquiry number on line 3 and the ordinary denial on line 4 are not strong findings in their contexts. The request on line 9 resembles an adapted pattern but also reads as an ordinary instruction. No correction is warranted solely on these matches. Their presence does not establish either deliberate use or coincidence.

Audience: the two distinctive quotations may evoke the meme community and its adult-source associations for familiar readers. Whether they suit a general publication depends on the purpose of the quotations; the text alone does not establish an intent to offend or endorse that context. Suggested paraphrases are optional and change how directly the source is quoted. The source document has not been edited.

Limits: the reference tables are selective, variants can be missed, and this review does not guarantee absence of other references or compliance with a publication policy. Match strength is an assessment of the supplied evidence, not proof of intent or provenance.

## Manual review checks

- Verify that S1, S2, S5, S6, and S7 do not become strong findings merely from table membership, punctuation, or a suffix.
- Verify that S3, S4, S8, and S9 retain recognizable matches, including quotations and adapted wording.
- Check that code comments, table cells, and passages in a longer document have usable locations and keep their surrounding context.
- Check that the report distinguishes quoted material from direct use and never treats uncertainty as proof of either intent or coincidence.
- Inspect report introductions, explanations, conclusions, and replacement text for newly added meme expressions. Only evidence needed to identify findings may retain quoted expressions; conversational style must not leak into the report.
- Review meaning and reporting choices rather than requiring an exact textual match to this sample. Record any actual model trials separately from this expected report.
