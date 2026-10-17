# tooltree

A **JetBrains IntelliJ Platform plugin** project, freshly generated from the official IntelliJ Platform Plugin Template (May 2026). So far it contains only the template's sample code — there is no tooltree-specific functionality, description or README yet, and the repo itself doesn't say what the plugin is meant to do. **Ask Brett what tooltree should be before building anything.**

## Status (as of Oct 17 2026)
- **Built:** template scaffold only (sample tool window with a "shuffle" random-number button, sample project service, startup activity, sample test). Plugin id `com.github.mossesx.tooltree`, version 0.0.1. Single commit: "Template cleanup" (May 18 2026).
- **In progress:** nothing.
- **Next:** define the plugin's purpose with Brett; then work through the template ToDo list in README.md (rewrite plugin.xml description + README, remove sample code and its `plugin.xml` registrations, `rootProject.name` in settings.gradle.kts still says "IntelliJ Platform Plugin Template").

## Stack & layout
Kotlin JVM 2.1.20, IntelliJ Platform Gradle Plugin 2.16.0, changelog plugin 2.5.0, targets IntelliJ IDEA 2025.2.6.2, Java 21 in CI, Gradle wrapper 9.5.0, JUnit 4 tests.
```
src/main/kotlin/com/github/mossesx/tooltree/
  MyBundle.kt                       i18n bundle (messages/MyBundle.properties)
  services/MyProjectService.kt      sample service
  startup/MyProjectActivity.kt      sample post-startup activity
  toolWindow/MyToolWindowFactory.kt sample tool window "MyToolWindow"
src/main/resources/META-INF/plugin.xml   plugin id/name/vendor/description + extension registrations
src/test/kotlin/.../MyPluginTest.kt      sample tests (testData in src/test/testData)
.run/                               IDE run configs (Run Plugin / Tests / Verifications)
.github/workflows/build.yml, release.yml; .github/dependabot.yml (daily Gradle updates)
CHANGELOG.md                        Keep-a-Changelog; release workflow patches it
```

## Build, run, test
Commands are from the template's CI (`./gradlew` is committed):
- Build plugin ZIP: `./gradlew buildPlugin` → `build/distributions/*.zip`
- Tests: `./gradlew check`
- Plugin Verifier: `./gradlew verifyPlugin`
- Run a sandbox IDE with the plugin: `./gradlew runIde` (GUI — not useful on the headless VPS; the "Run Plugin" config in `.run/` uses it).
- **CI:** push to `main` or any PR runs **Build** (build → test → verify → create a **draft GitHub release** on non-PR runs).
- **Release:** publishing a GitHub release runs `release.yml` → `./gradlew publishPlugin` to JetBrains Marketplace (needs secrets `PUBLISH_TOKEN`, `PRIVATE_KEY`, `PRIVATE_KEY_PASSWORD`, `CERTIFICATE_CHAIN` — none confirmed set), uploads the ZIP to the release and opens a changelog PR.
- First local build downloads IntelliJ IDEA (~1 GB+); Java 21 required. Not verified on the VPS.

## Conventions & decisions
- Follow the IntelliJ Platform Plugin Template conventions: version in `gradle.properties`, changes under `## [Unreleased]` in CHANGELOG.md (the release flow reads it).
- Keep `plugin.xml` registrations in sync when adding/removing services, tool windows or activities.
- README badges use a `MARKETPLACE_ID` placeholder until the plugin is published.
- Group/package: `com.github.mossesx.tooltree`.

## Related repos
None referenced in this repo. Brett's other projects are mostly Android apps (`MossesX/pilotx`, `MossesX/ActiveX`, `MossesX/xAI`) plus `MossesX/axHub` on his VPS.

## Working with Brett (same in every MossesX repo)

- **Where he works:** mostly from his Android phone (Samsung Galaxy S26 Ultra), often through **Moshi** (mosh) into his Hostinger VPS, where Claude Code runs. Keep replies phone-readable: lead with the result, short paragraphs, no walls of text.
- **Model choice:** before any build task, recommend which model to use and why, then let him pick from the top three (Fable, Opus, Sonnet). Use Fable where it's warranted, Opus for most work, and Sonnet only when you're sure Opus isn't needed.
- **The repo is the shared memory.** Sessions on the phone (Moshi), desktop, web and claude.ai don't share chat history, so anything a future session needs must live in this repo. Commit and push often with clear messages, and update the **Status** section of this file whenever something meaningful changes.
- **No secrets in the repo:** no tokens, passwords, keys or IPs with credentials. Use environment variables or GitHub Actions secrets.
- **GitHub:** account `MossesX`. A new repo must exist on GitHub before a session can push to it.
- **Server:** a Hostinger VPS running **Coolify**. Coolify's Traefik proxy owns ports 80/443, so new web apps go behind it as Coolify apps (no separate nginx). His domain is `amberxai.com`.
- **axHub:** his connector hub on the VPS (repo `MossesX/axHub`). If the axHub MCP server is configured in this Claude Code install, use its `list_services`, `describe_service` and `call` tools to reach his other services instead of asking him for credentials.
