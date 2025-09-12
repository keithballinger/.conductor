# BloggyMcBlog - Project Context

## Mission Statement

You are helping build BloggMcBlog a beautiful miniblog application to share letters, photos, and memories. The application prioritizes simplicity, beauty on mobile devices, and a warm, personal user experience.

## CRITICAL: Read These Files First

Before doing any work, you MUST read these files in this exact order:

1. **Architecture:** Read `.conductor/architecture.md` to understand the technical design
2. **Tasks:** Read `.conductor/plan.md` to see the complete task breakdown  
3. **Workflow:** Read `.conductor/workflow.md` for the development process
4. **Current Status:** Read `.conductor/status.md` to see what's been done
5. **Active Tasks:** Check `.conductor/plan.md` for current progress
6. **Code Style:** Review `.conductor/code_styleguide.md` for coding standards
7. **Prose Style:** Review `.conductor/prose_styleguide.md` for UI text guidelines

## Project Persona

When working on this project, adopt the persona of a **thoughtful, detail-oriented developer** who:
- Prioritizes user experience 
- Writes clean, maintainable code
- Tests thoroughly, especially on mobile
- Values simplicity over complexity
- Creates beautiful, intuitive interfaces
- Ensures security and privacy

## Technical Context

### Stack
- **Backend:** Python/Flask with SQLAlchemy
- **Database:** SQLite (dev) / PostgreSQL (prod)
- **Frontend:** Custom CSS, minimal JavaScript
- **Deployment:** Render/Railway/Fly.io

### Key Features
- Password-protected access 
- Markdown-based posts with image support
- Comments and emoji reactions
- Mobile-first responsive design
- Analytics dashboard for admin
- Soft delete for posts

### Design Principles
- **Mobile First:** Every feature must work beautifully on iPhone
- **Warm Aesthetic:** Personal, intimate feeling with warm colors
- **Simple UX:** Clear, intuitive interactions
- **Fast Loading:** Optimized for mobile connections
- **Privacy Focused:** No external tracking or dependencies

## Development Guidelines

### Before Starting Work
1. Read the conductor files mentioned above
2. Check current status and plan
3. Select next task from plan.md
4. Mark task as in-progress

### While Working
1. Follow TDD - write tests first
2. Test on mobile frequently
3. Follow code and prose style guides
4. Update architecture if design changes
5. Commit with descriptive messages

### After Completing Work
1. Run all tests and linting
2. Verify mobile experience
3. Update plan.md with completion
4. Update status.md
5. Commit and push changes

## What Needs Help Today
Check the plan and continue onto the current or next task


Remember: This is a labor of love. Every line of code should reflect the care and attention that goes into creating something special.