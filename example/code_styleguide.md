# Code Style Guide - Bloggy McBlog

## Core Principle: "Clarity Over Cleverness"

Write code that tells a story. Every function, variable, and module should clearly express its purpose. Optimize for readability and maintainability over premature optimization.

## Python Style Guidelines

### Base Style Guide
- Follow PEP 8 strictly
- Use Black for automatic formatting (line length: 100)
- Use isort for import sorting
- Use type hints for all public functions
- Use ruff for linting

### Project-Specific Conventions

## Naming Conventions

### Variables
```python
# Good
user_password = request.form.get('password')
post_content = markdown.render(raw_content)
keith_user = User.query.filter_by(username='keith').first()

# Bad
pw = request.form.get('password')
data = markdown.render(raw_content)
u = User.query.filter_by(username='keith').first()
```

### Functions
```python
# Good
def get_recent_posts(limit: int = 10) -> List[Post]:
    """Retrieve recent posts for display."""
    pass

def authenticate_user(username: str, password: str) -> Optional[User]:
    """Verify user credentials and return user if valid."""
    pass

# Bad
def posts(n):
    pass

def auth(u, p):
    pass
```

### Classes
```python
# Good
class PostManager:
    """Handles post creation, editing, and deletion."""
    pass

class AnalyticsTracker:
    """Tracks and aggregates user analytics events."""
    pass

# Bad
class PM:
    pass

class tracker:
    pass
```

## Import Organization

```python
# Standard library imports
import os
import sys
from datetime import datetime
from typing import List, Optional, Dict

# Third-party imports
import markdown
from flask import Flask, render_template, request
from flask_login import login_required, current_user
from sqlalchemy import desc

# Local application imports
from app.models import Post, User, Comment
from app.utils import generate_excerpt, create_thumbnail
from app.config import Config
```

## Function Documentation

```python
def create_post(
    title: str,
    content: str,
    author: User,
    summary: Optional[str] = None
) -> Post:
    """
    Create a new blog post.
    
    Args:
        title: The post title
        content: Markdown content of the post
        author: User object of the post author
        summary: Optional custom summary, auto-generated if None
    
    Returns:
        The created Post object
    
    Raises:
        ValidationError: If title or content is empty
    """
    pass
```

## Error Handling

```python
# Good
try:
    post = Post.query.get_or_404(post_id)
    post.view_count += 1
    db.session.commit()
except Exception as e:
    logger.error(f"Failed to update view count for post {post_id}: {e}")
    db.session.rollback()
    # Continue - non-critical error

# Bad
try:
    post = Post.query.get(post_id)
    post.view_count += 1
    db.session.commit()
except:
    pass  # Never silent fail
```

## Database Queries

```python
# Good - Explicit and efficient
recent_posts = (
    Post.query
    .filter_by(is_deleted=False)
    .order_by(Post.published_at.desc())
    .limit(10)
    .all()
)

# Good - With relationships
posts_with_comments = (
    Post.query
    .options(joinedload(Post.comments))
    .filter_by(is_deleted=False)
    .all()
)

# Bad - N+1 query problem
posts = Post.query.all()
for post in posts:
    print(post.comments)  # Triggers query for each post
```

## Flask-Specific Patterns

### Blueprints
```python
# In app/main/__init__.py
from flask import Blueprint

main = Blueprint('main', __name__)

from app.main import routes  # noqa: E402, F401
```

### Routes
```python
@main.route('/post/<uuid:post_id>')
@login_required
def view_post(post_id: str):
    """Display a single blog post."""
    post = Post.query.get_or_404(post_id)
    
    # Only show non-deleted posts to regular users
    if post.is_deleted and not current_user.is_admin:
        abort(404)
    
    post.increment_view_count()
    return render_template('main/post.html', post=post)
```

### Forms
```python
class CommentForm(FlaskForm):
    """Form for adding comments to posts."""
    
    content = TextAreaField(
        'Your thoughts',
        validators=[DataRequired(), Length(min=1, max=1000)]
    )
    submit = SubmitField('Share')
```

## Testing Patterns

```python
class TestPostCreation:
    """Test suite for post creation functionality."""
    
    def test_create_post_with_valid_data(self, client, admin_user):
        """Test creating a post with all required fields."""
        # Arrange
        post_data = {
            'title': 'Test Letter',
            'content': 'Dear World, ...'
        }
        
        # Act
        response = client.post('/admin/create', data=post_data)
        
        # Assert
        assert response.status_code == 302
        assert Post.query.filter_by(title='Test Letter').first() is not None
```

## Configuration

```python
class Config:
    """Base configuration."""
    
    # Security
    SECRET_KEY = os.environ.get('SECRET_KEY') or 'dev-secret-key'
    WTF_CSRF_ENABLED = True
    
    # Database
    SQLALCHEMY_DATABASE_URI = os.environ.get('DATABASE_URL') or 'sqlite:///app.db'
    SQLALCHEMY_TRACK_MODIFICATIONS = False
    
    # Application
    POSTS_PER_PAGE = 10
    MAX_CONTENT_LENGTH = 16 * 1024 * 1024  # 16MB max file size
```

## Security Patterns

```python
# Good - Password hashing
from werkzeug.security import generate_password_hash, check_password_hash

class User(db.Model):
    password_hash = db.Column(db.String(255))
    
    def set_password(self, password: str) -> None:
        """Hash and store password."""
        self.password_hash = generate_password_hash(password)
    
    def check_password(self, password: str) -> bool:
        """Verify password against hash."""
        return check_password_hash(self.password_hash, password)

# Good - SQL injection prevention (using ORM)
post = Post.query.filter_by(id=post_id).first()

# Bad - SQL injection vulnerable
query = f"SELECT * FROM posts WHERE id = {post_id}"  # Never do this!
```

## Logging

```python
import logging

logger = logging.getLogger(__name__)

# Good logging
logger.info(f"User {current_user.username} logged in")
logger.error(f"Failed to process image: {e}", exc_info=True)
logger.warning(f"Rate limit exceeded for IP {request.remote_addr}")

# Bad logging
print(f"User logged in")  # Don't use print in production
logger.info(f"Password: {password}")  # Never log sensitive data
```

## Comments in Code

```python
# Good - Explains WHY, not WHAT
def generate_excerpt(content: str, length: int = 200) -> str:
    """Generate excerpt from post content."""
    # Strip markdown formatting to get plain text for excerpt
    plain_text = strip_markdown(content)
    
    # Find the last complete word within the length limit
    # to avoid cutting words in half
    if len(plain_text) > length:
        excerpt = plain_text[:length]
        last_space = excerpt.rfind(' ')
        if last_space > 0:
            excerpt = excerpt[:last_space]
        return excerpt + '...'
    
    return plain_text

# Bad - States the obvious
def save_post(post):
    # Save the post
    db.session.add(post)
    # Commit the session
    db.session.commit()
    # Return the post
    return post
```

## File Organization

### Models (app/models.py)
- One model per major entity
- Related models grouped together
- Business logic in model methods

### Routes (app/*/routes.py)
- Thin controllers - business logic in models/services
- Clear separation between blueprints
- Consistent URL patterns

### Templates
- Organized by blueprint
- Partial templates prefixed with underscore
- Macros for repeated elements

### Static Files
- Organized by type (css/, js/, images/)
- Versioned filenames for cache busting
- Minified versions for production

## Git Commit Messages

```bash
# Good
feat(auth): Add rate limiting to login attempts
fix(posts): Correct pagination on mobile devices
style(admin): Update dashboard layout for better UX
test(comments): Add tests for emoji reaction limits

# Bad
fixed stuff
WIP
update
```

## Performance Guidelines

1. Use query optimization (eager loading, indexing)
2. Implement caching for expensive operations
3. Lazy load images and non-critical resources
4. Minimize database queries per request
5. Use pagination for large datasets

## Accessibility

1. Always include alt text for images
2. Use semantic HTML elements
3. Ensure keyboard navigation works
4. Test with screen readers
5. Maintain proper color contrast

## Mobile-First Development

1. Test on actual devices, not just browser DevTools
2. Design for touch interactions (minimum 44x44px targets)
3. Optimize images for mobile bandwidth
4. Consider offline functionality
5. Test on slow connections

## Code Review Checklist

- [ ] Follows PEP 8 style guide
- [ ] Has appropriate type hints
- [ ] Includes docstrings for public functions
- [ ] Has unit tests with good coverage
- [ ] Handles errors appropriately
- [ ] No sensitive data in logs or commits
- [ ] SQL queries are optimized
- [ ] Mobile responsive
- [ ] Accessible
- [ ] Security best practices followed