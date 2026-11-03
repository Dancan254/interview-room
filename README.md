# The Interview Room

A curated, open-source bank of backend engineering interview questions — answered on camera, one at a time.

Every question here is also a short-form video. The repo holds the questions, the answers, and the links. The reasoning lives on video.

## Episodes

| # | Question | Category | Status | Video |
|---|----------|----------|--------|-------|
| 001 | 200 requests hit your API at the exact same millisecond. What happens? | Concurrency / Backend fundamentals | **Published** | [link](episodes/ep001.md) |
| 002 | Why is `count++` not thread-safe even with `volatile`? | Java Concurrency | Scripted | [link](episodes/ep002.md) |
| 003 | Your `@Transactional` method is failing silently | Spring Boot | Scripted | - |
| 004 | Why retrying a payment can charge the card twice | Distributed Systems | Scripted | - |
| 005 | Your Kafka consumer crashes after processing but before committing the offset | Distributed Systems | Scripted | - |

## Question bank

- [Java Concurrency](questions/java-concurrency.md)
- [Spring Boot](questions/spring-boot.md)
- [Distributed Systems](questions/distributed-systems.md)
- [Databases](questions/databases.md)
- [System Design](questions/system-design.md)
- [Security](questions/security.md)

## How to contribute a question

1. Open an issue or a pull request.
2. Add the question to the right file under `questions/` (or create a new category file).
3. Use the five-line metadata format:

```markdown
### Your question here?
- **Category:** The topic
- **Level:** Junior / Mid / Senior
- **Languages:** Any (answer with Java + Spring Boot)
- **Status:** Planned
- **Video:** -
```

- Do not attribute questions to specific companies.
- Keep questions language-agnostic where possible.
- The answer should be explainable in 60–90 seconds.

## Philosophy

Questions are free. Answers are the product. If you want the reasoning, watch the video. If you want to study the bank, use the repo.

## Licence

MIT. See [LICENCE](LICENCE).
