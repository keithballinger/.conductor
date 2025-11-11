# Project Workflow - Blogger McBlog

## Guiding Principles

1. **The Plan is the Source of Truth:** All work must be tracked in `plan.md`
2. **The Status is Always Current:** `status.md` must be updated at the end of every work session
3. **The Architecture is Deliberate:** Changes to the system design must be documented in `architecture.md` *before* implementation
4. **Test-Driven Development:** Write unit tests before implementing functionality
5. **High Code Coverage:** Aim for >80% code coverage for all modules
6. **Mobile-First:** Every feature must work beautifully on iPhone
7. **User Experience First:** Every decision should prioritize user experience

## Task Workflow

All tasks follow a strict lifecycle:

### Standard Task Workflow

1. **Select Task:** Choose the next available task from `plan.md` in sequential order

2. **Mark In Progress:** Before beginning work, edit `plan.md` and change the task from `[ ]` to `[~]`

3. **Write Tests First:** For each task:
   - Write unit tests that define expected behavior
   - Ensure tests fail initially (red phase)
   - Implement code to make tests pass (green phase)
   - Refactor while keeping tests green (refactor phase)

4. **Implement:** Perform the work required following TDD principles

5. **Test on Mobile:** When working on a project that requires UI for mobile, for any UI changes:
   - Test in iPhone simulator or device
   - Verify touch interactions work
   - Ensure text is readable
   - Check performance on mobile connection

6. **Verify Coverage:** Run coverage reports:
   ```bash
   pytest --cov=app --cov-report=html
   ```
   Target: >80% coverage for new code

7. **Document Deviations:** If implementation differs from architecture:
   - **STOP** implementation
   - Update `architecture.md` with new design
   - Add dated note explaining the change
   - Resume implementation

8. **Commit Code Changes:**
   - Stage all code changes related to the task.
   - Propose a clear, concise commit message following the prose style guide.
   - Perform the commit.

9. **Create dev_log.md entry:**
   - Obtain the hash of the *just-completed commit* (`git log -1 --format="%H"`).
   - Create a detailed entry in the development log for the completed task, referencing the commit hash.
   - Append the entry to `dev_log.md`.
   - Stage `dev_log.md`.
   - Propose a commit message for the `dev_log.md` update (e.g., "chore(dev_log): Add entry for [Task Name]").
   - Perform the commit.


### Quality Gates

Before marking any task complete, verify:

- [ ] All tests pass
- [ ] Code coverage meets requirements (>80%)
- [ ] Code follows style guidelines (PEP 8)
- [ ] All public functions have docstrings
- [ ] Type hints are present and correct
- [ ] No linting errors (ruff, black)
- [ ] Works correctly on mobile
- [ ] Documentation updated if needed
- [ ] No security vulnerabilities introduced

## Development Commands

### Setup
```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Setup database
flask db upgrade

# Create .env from example
cp .env.example .env
```

### Daily Development
```bash
# Start development server
make run

# Run tests
make test

# Run linting
make lint

# Format code
make format

# Check coverage
make coverage
```

### Before Committing
```bash
# Run all checks
make check

# This runs:
# - black (formatting)
# - ruff (linting)
# - mypy (type checking)
# - pytest (tests)
# - coverage report
```

## Testing Requirements

### Unit Testing
- Every module must have corresponding tests
- Use pytest fixtures for setup
- Mock external dependencies
- Test both success and failure cases

### Integration Testing
- Test complete user flows
- Verify database transactions
- Test authentication and authorization
- Check form submissions

### Mobile Testing
- Test on actual iPhone when possible
- Use Safari developer tools
- Test touch interactions
- Verify responsive layouts
- Check performance on 3G/4G

## Code Review Process

### Self-Review Checklist
Before requesting review:

1. **Functionality**
   - Feature works as specified
   - Edge cases handled
   - Error messages are user-friendly

2. **Code Quality**
   - Follows style guide
   - DRY principle applied
   - Clear variable/function names
   - Appropriate comments

3. **Testing**
   - Unit tests comprehensive
   - Integration tests pass
   - Coverage adequate (>80%)

4. **Security**
   - No hardcoded secrets
   - Input validation present
   - SQL injection prevented
   - XSS protection in place

5. **Performance**
   - Database queries optimized
   - Images optimized
   - Caching implemented where needed

6. **Mobile Experience**
   - Touch targets adequate (44x44px)
   - Text readable without zooming
   - Performance acceptable on mobile
   - Interactions feel native

## Status Update Workflow

At the end of **every work session**:

1. Update `status.md` with:
   - Current date/time
   - Project status
   - Current phase and task
   - Next action needed
   - Any blockers
   - Session notes

2. Commit all changes with descriptive message

3. Push to feature branch

## Commit Guidelines

### Message Format
```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

### Types
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation only
- `style`: Formatting, missing semicolons, etc.
- `refactor`: Code change that neither fixes a bug nor adds a feature
- `test`: Adding missing tests
- `chore`: Maintenance tasks

### Examples
```bash
git commit -m "feat(auth): Add remember me functionality"
git commit -m "fix(posts): Correct excerpt generation for short posts"
git commit -m "test(comments): Add tests for emoji reaction limits"
git commit -m "style(mobile): Improve button touch targets"
```

## Definition of Done

A task is complete when:

1. All code implemented to specification
2. Unit tests written and passing
3. Code coverage >80%
4. Documentation complete
5. Code passes all linting
6. Works beautifully on mobile
7. Implementation notes added to plan.md
8. Status.md updated
9. Changes committed with proper message

## Emergency Procedures

### Critical Bug in Production
1. Create hotfix branch from main
2. Write failing test for bug
3. Implement minimal fix
4. Test thoroughly including mobile
5. Deploy immediately
6. Document in plan.md

### Data Loss
1. Stop all write operations
2. Restore from latest backup
3. Verify data integrity
4. Document incident
5. Update backup procedures

### Security Breach
1. Rotate all secrets immediately
2. Review access logs
3. Patch vulnerability
4. Notify affected users (if any)
5. Document and update security procedures

## Deployment Workflow

### Pre-Deployment Checklist
- [ ] All tests passing
- [ ] Coverage >80%
- [ ] No linting errors
- [ ] Mobile testing complete
- [ ] Environment variables configured
- [ ] Database migrations ready
- [ ] Backup created

### Deployment Steps
1. Merge feature branch to main
2. Tag release with version
3. Push to deployment service
4. Run database migrations
5. Verify deployment
6. Test critical paths
7. Monitor for errors

### Post-Deployment
1. Update status.md
2. Monitor analytics
3. Check error logs
4. Gather user feedback
5. Plan next iteration

## Continuous Improvement

- Review workflow weekly
- Update based on pain points
- Document lessons learned
- Optimize for user happiness
- Keep things simple and maintainable