---
type: llm
criteria: "The answer gives an ozone filename filter that covers every Metop satellite (for example `*+O3+IASI*`) as its default, and says the series spans Metop-A and Metop-B. It fails if the default filter names only METOPA or METOPB, even with a warning, and fails if it gives no filter. A single-satellite filter is allowed only when offered as an explicit non-default alternative."
---

Mechanism: the default IASI filter covers every satellite, because a Metop-B-only filter drops the earlier years of a 2008 to 2023 series. The collection ID is graded by the regex grader.
