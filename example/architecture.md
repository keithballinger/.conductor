# Bloggy McBlog - Technical Architecture

## Project Overview
A blog in Python

## Technology Stack

### Backend
- **Framework**: Flask 3.x (lightweight, easy to deploy)
- **Database**: SQLite for development, PostgreSQL for production
- **ORM**: SQLAlchemy 2.x
- **Forms**: Flask-WTF with CSRF protection
- **Markdown**: Python-Markdown with extensions
- **Image Processing**: Pillow for thumbnail generation
- **Charts**: Chart.js (frontend) with JSON API endpoints

### Frontend
- **CSS Framework**: Custom CSS with CSS Grid/Flexbox
- **JavaScript**: Vanilla JS for interactions (minimal dependencies)
- **Fonts**: Inter for body, Crimson Pro for headings
- **Icons**: Heroicons for UI elements
- **Markdown Editor**: SimpleMDE or similar lightweight editor

### Deployment
- **Application Server**: Gunicorn
- **File Storage**: Local filesystem with option for S3
- **Deployment Target**: Render, Railway, or Fly.io (all support easy Python deployment)

## Database Schema

### Some Random Table
```sql
users:
  - id: UUID (primary key)
  - username: VARCHAR(50) UNIQUE NOT NULL
  - password_hash: VARCHAR(255) NOT NULL
  - is_admin: BOOLEAN DEFAULT FALSE
  - created_at: TIMESTAMP
  - last_login: TIMESTAMP
```

(etc)


## Application Architecture

### Directory Structure
```
calculator/
├── .conductor/           # Project management files
├── app/
│   ├── __init__.py      # Flask app factory
│   ├── models.py        # SQLAlchemy models
│   ├── auth.py          # Authentication blueprint
│   ├── main.py          # Main blog blueprint
│   ├── admin.py         # Admin blueprint
│   ├── analytics.py     # Analytics blueprint
│   ├── forms.py         # WTForms definitions
│   ├── utils.py         # Helper functions
│   └── config.py        # Configuration classes
├── templates/
│   ├── base.html        # Base template
│   ├── auth/
│   │   └── login.html
│   ├── main/
│   │   ├── index.html   # Post listing
│   │   ├── post.html    # Single post view
│   │   └── _post_card.html
│   └── admin/
│       ├── dashboard.html
│       ├── edit_post.html
│       ├── analytics.html
│       └── settings.html
├── static/
│   ├── css/
│   │   └── style.css
│   ├── js/
│   │   ├── main.js
│   │   └── analytics.js
│   └── uploads/         # User uploaded images
│       └── thumbnails/
├── migrations/          # Alembic migrations
├── tests/
│   ├── test_auth.py
│   ├── test_posts.py
│   ├── test_admin.py
│   └── test_analytics.py
├── requirements.txt
├── runtime.txt         # Python version for deployment
├── Procfile           # Deployment commands
├── .env.example
├── .gitignore
├── Makefile
└── README.md
```

## Core Features

### 1. Authentication System
- Session-based authentication using Flask-Login
- Remember me functionality
- Automatic session timeout after 30 days
- Failed login attempt tracking

### 2. Post Management
- Rich text editor with Markdown support
- Image upload with automatic thumbnail generation
- Drag-and-drop image upload
- Auto-save drafts every 30 seconds
- Soft delete with recovery option for admin
- Post scheduling (future publish dates)
- Excerpt generation from content or custom summary

### 3. User Experience
- Clean, minimal listing of posts in reverse chronological order
- Pagination (10 posts per page)
- Post cards showing title, date, excerpt, and thumbnail
- Full post view with images displayed inline
- Comment box at bottom of each post
- Emoji reaction picker (max 5 different emojis per user per post)
- Responsive design optimized for iPhone
- Smooth scrolling and touch-friendly interactions

### 4. Admin Interface
- Dashboard with recent activity overview
- Create/Edit/Delete posts with live preview
- Markdown editor with toolbar
- Image management (upload, insert, delete)
- Password management (change passwords)
- Analytics dashboard with charts:
  - Login frequency
  - Page views per post
  - Comment activity
  - Popular posts
  - User engagement timeline
- Bulk operations (delete multiple posts)

### 5. Analytics System
- Track all significant events
- Privacy-focused (no external trackers)
- Visualizations using Chart.js:
  - Line chart for login frequency
  - Bar chart for post popularity
  - Activity heatmap
  - Engagement metrics
- Export data as CSV

## Security Considerations

### Authentication & Authorization
- Passwords hashed using Werkzeug's pbkdf2
- CSRF protection on all forms
- Session cookies with HttpOnly and Secure flags
- Rate limiting on login attempts (5 attempts per 15 minutes)
- Separate permission levels (user vs admin)

### Data Protection
- SQL injection prevention via SQLAlchemy ORM
- XSS protection via Jinja2 auto-escaping
- File upload validation (type, size limits)
- Sanitized markdown rendering
- No direct file serving (all through Flask routes)

### Privacy
- No external analytics or tracking
- All data stored locally
- No CDN dependencies (all assets served locally)
- HTTPS enforced in production

## Performance Optimizations

### Database
- Indexed fields: created_at, published_at, is_deleted
- Eager loading for related data (comments, reactions)
- Query pagination with LIMIT/OFFSET
- Connection pooling

### Caching
- Static file caching headers
- Template fragment caching for sidebar
- Thumbnail generation on upload (not on request)

### Frontend
- Minified CSS/JS in production
- Lazy loading for images
- Responsive images with srcset
- Minimal JavaScript (no heavy frameworks)

## Deployment Strategy

### Environment Variables
```
FLASK_APP=app
FLASK_ENV=production
SECRET_KEY=<generated-secret>
DATABASE_URL=<postgres-connection-string>
ADMIN_PASSWORD=<hashed-password>
USER_PASSWORD=<hashed-password>
UPLOAD_FOLDER=/app/uploads
MAX_CONTENT_LENGTH=16777216  # 16MB max file size
```

### Deployment Steps
1. Push to GitHub repository
2. Connect to deployment service (Render/Railway)
3. Set environment variables
4. Configure PostgreSQL database
5. Run migrations on deploy
6. Configure persistent storage for uploads

### Backup Strategy
- Daily database backups
- Weekly full backup including uploaded files
- Backup retention: 30 days

## Mobile-First Design Principles

### Layout
- Single column layout on mobile
- Touch-friendly button sizes (min 44x44px)
- Adequate spacing between interactive elements
- Sticky header with minimal height
- Bottom navigation for key actions

### Typography
- Base font size: 16px (no zooming needed)
- Line height: 1.6 for readability
- Comfortable measure (line length)
- High contrast colors

### Interactions
- Swipe gestures for navigation
- Tap to show/hide metadata
- Long press for context menu
- Pull to refresh on post listing
- Smooth scrolling with momentum

### Performance
- Progressive image loading
- Optimized fonts (subset, woff2)
- Minimal initial payload
- Service worker for offline viewing

## Testing Strategy

### Unit Tests
- Model validation and methods
- Authentication functions
- Markdown rendering
- Image processing
- Analytics aggregation

### Integration Tests
- Authentication flow
- Post CRUD operations
- Comment submission
- File uploads
- Analytics tracking

### End-to-End Tests
- Complete user journey (login → read → comment)
- Admin workflow (create → edit → publish)
- Mobile interactions
- Performance benchmarks

### Coverage Goals
- Overall: >80% coverage
- Critical paths: >95% coverage
- Models: 100% coverage

## Future Enhancements (Phase 2)

1. **Rich Media**
   - Video upload support
   - Audio messages
   - Gallery view for images

2. **Advanced Features**
   - Post categories/tags
   - Search functionality
   - Email notifications for new posts
   - RSS feed generation

3. **Personalization**
   - Multiple user support
   - Customizable themes
   - User preferences

4. **Backup & Sync**
   - Automatic S3 backup
   - Export to PDF/ePub
   - Import from other platforms

## Development Workflow

### Local Setup
```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Setup database
flask db init
flask db migrate -m "Initial migration"
flask db upgrade

# Create .env file
cp .env.example .env
# Edit .env with your settings

# Run development server
flask run
```

### Testing
```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=app --cov-report=html

# Run specific test file
pytest tests/test_auth.py

# Run linting
ruff check .
black --check .
mypy app/
```

### Deployment
```bash
# Build for production
make build

# Run production server locally
gunicorn app:create_app()

# Deploy to Render
git push origin main  # Auto-deploys via webhook
```

## Technical Decisions & Rationale

### Why Flask?
- Lightweight and simple for a small application
- Easy to deploy on modern PaaS providers
- Extensive ecosystem of extensions
- Familiar Python ecosystem

### Why SQLite/PostgreSQL?
- SQLite perfect for development and small deployments
- PostgreSQL for production scalability
- SQLAlchemy provides abstraction layer

### Why Server-Side Rendering?
- Better SEO (if ever made public)
- Faster initial page load
- Simpler architecture
- Works without JavaScript

### Why Minimal JavaScript?
- Reduces complexity
- Better performance on mobile
- Easier maintenance
- Progressive enhancement approach

### Why Markdown?
- Simple and readable format
- Easy to write and edit
- Good ecosystem of tools
- Exports well to other formats
