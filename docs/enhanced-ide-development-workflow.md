# Enhanced Development Workflow

This is a simple step-by-step guide to help you efficiently manage your development workflow using the BMad Method. Refer to the **[<ins>User Guide</ins>](user-guide.md)** for any scenario that is not covered here.

## Create new Branch

1. **Start new branch**

## Story Creation (Scrum Master)

1. **Start new chat/conversation**
2. **Load SM agent**
3. **Execute**: `*draft` (runs create-next-story task)
4. **Review generated story** in `docs/stories/`
5. **Update status**: Change from "Draft" to "Approved"

## Story Implementation (Developer)

1. **Start new chat/conversation**
2. **Load Dev agent**
3. **Execute**: `*develop-story {selected-story}` (runs execute-checklist task)
4. **Review generated report** in `{selected-story}`

## Test Architect Integration Throughout Workflow

### Stage 1: After Story Creation (Before Dev Starts)

**Optional but Valuable - Set Dev Up for Success:**

```bash
# Design test strategy for developer
@qa *design {approved-story}
# Output: docs/qa/assessments/{epic}.{story}-test-design-{YYYYMMDD}.md
# Why: Gives Dev clear test requirements upfront

# Identify risks to watch for
@qa *risk {approved-story}
# Output: docs/qa/assessments/{epic}.{story}-risk-{YYYYMMDD}.md
# Why: Helps Dev avoid critical issues and focus on risk areas
```

### Stage 2: During Development (Optional Checkpoints)

**Dev Can Self-Check Progress:**

```bash
# Validate NFRs mid-implementation
@qa *nfr {story-in-progress}
# Output: docs/qa/assessments/{epic}.{story}-nfr-{YYYYMMDD}.md
# Why: Catch performance/security issues early

# Verify test coverage while developing
@qa *trace {story-in-progress}
# Output: docs/qa/assessments/{epic}.{story}-trace-{YYYYMMDD}.md
# Why: Ensure you're writing the right tests
```

### Stage 3: Story Review (Required)

**Standard Review Flow:**

1. **Start new chat/conversation**
2. **Load QA agent** (Test Architect - Quinn)
3. **Execute**: `@qa *review {selected-story}`
4. **Review outputs**:
   - QA Results section added to story file
   - Quality gate file in `docs/qa/gates/{epic}.{story}-{slug}.yml`

**If Issues Found:**

```bash
# After fixes, update gate status
@qa *gate {reviewed-story}
# Output: Updates docs/qa/gates/{epic}.{story}-{slug}.yml
```

### Special Situations

**High-Risk Stories or Brownfield:**

- Always run `*risk` and `*design` before development
- Extra focus on regression testing

**Complex Integrations:**

- Run `*trace` to ensure all integration points tested
- Consider `*nfr` for performance validation

**Performance-Critical Features:**

- Run `*nfr` during development, not just at review
- Set performance baselines early

### Understanding Gate Decisions

- **PASS**: Ready for production, all quality criteria met
- **CONCERNS**: Non-critical issues to review with team
- **FAIL**: Critical issues must be fixed (security, missing tests)
- **WAIVED**: Known issues accepted by team with documentation

### What Quinn Does During Review

1. **Analyzes code quality** and architecture patterns
2. **Actively refactors** code when safe to do so
3. **Validates test coverage** at appropriate levels
4. **Identifies risks** (security, performance, data)
5. **Checks NFRs** against standards
6. **Creates quality gate** with clear decision criteria
7. **Documents everything** for audit trail

## Commit Changes and Push

1. **Commit changes**
2. **Push to remote**

## Repeat Until Complete

- **SM**: Create next story → Review → Approve
- **Dev**: Implement story → Complete → Mark Ready for Review
- **QA**: Review story → Mark done
- **Commit**: All changes
- **Push**: To remote
- **Continue**: Until all features implemented
