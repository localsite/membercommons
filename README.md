# MemberCommons - Project Collaboration Platform

MemberCommons is a beautiful, professional JAM Stack web application designed for technical teams working on local innovation projects. Built with modern web technologies and featuring AI-powered insights, it connects developers, designers, and innovators to collaborate on government modernization and community impact projects.

## 🌟 Key Features

### Project Management
- **Post Activities**: Create detailed project postings, job openings, and collaboration requests
- **Smart Discovery**: AI-powered project search with natural language queries
- **Task Tracking**: Manage assigned tasks with progress monitoring and deadlines
- **Timeline Views**: Visual project timelines and milestone tracking

### Team Collaboration
- **People Directory**: Connect with developers, designers, and project leaders
- **Team Formation**: Create and join focused development teams
- **Organization Network**: Connect with verified organizations and funding sources
- **Skills Matching**: AI-powered matching based on technical skills and interests

### AI-Powered Insights
- **Smart Search**: Natural language search powered by Google Gemini AI
- **Project Recommendations**: Personalized project suggestions based on skills and interests
- **Data Analysis**: Smart insights for team and project performance
- **Policy Matching**: Connect with projects aligned to your policy preferences

### Personal Profiles
- **Skills Portfolio**: Showcase technical expertise with visual skill levels
- **Interest Ratings**: 5-star rating system for 20+ focus areas
- **Policy Preferences**: Comprehensive survey with Sankey chart visualizations
- **Certification Tracking**: Verified badges and achievements

## 🚀 Technology Stack

### Frontend (JAM Stack)
- **HTML5/CSS3**: Modern, semantic markup with CSS Grid and Flexbox
- **Vanilla JavaScript**: No build process required - runs directly in browser
- **Responsive Design**: Mobile-first design with smooth animations
- **Notion-Inspired UI**: Clean, minimal aesthetic with soft shadows and gradients

### Backend (Rust)
- **Actix-web**: High-performance web framework
- **SQLx**: Async PostgreSQL database toolkit
- **Gemini AI**: Google's AI for smart search and insights
- **JWT Authentication**: Secure token-based authentication

### Database
- **PostgreSQL**: Production-ready relational database
- **SuiteCRM Schema**: Compatible with Salesforce/Dynamics table structure
- **Azure/Google Cloud**: Cloud-ready database configuration

## 📁 Project Structure

```
MemberCommons/
├── index.html              # Main application file
├── css/                    # Stylesheets
│   ├── projects.css        # Project management styles
│   ├── people-teams.css    # People & teams styles
│   └── account.css         # Account & survey styles
├── js/                     # JavaScript modules
│   ├── projects.js         # Project management functionality
│   └── survey.js           # Survey & skills management
├── config/                 # Configuration files
│   └── settings.example.js # Example configuration
├── src/                    # Rust backend source
│   └── main.rs            # Main server application
├── sql/                    # Database schema
│   └── suitecrm-postgres.sql
└── project/               # Additional frontend assets
    └── edit.html
```

## 🎨 Design Philosophy

### Notion-Inspired Aesthetic
- **Clean & Minimal**: Uncluttered interface focusing on content
- **Soft Color Palette**: Light green, pastel blue, muted orange accents
- **Smooth Animations**: Subtle transitions and hover effects
- **Professional Typography**: Inter font family with consistent hierarchy

### User Experience
- **Collapsible Navigation**: Smooth sidebar with icon tooltips
- **Responsive Design**: Optimized for desktop, tablet, and mobile
- **Accessibility**: WCAG compliant with keyboard navigation support
- **Progressive Enhancement**: Works without JavaScript for core features

## 🛠️ Setup Instructions

### Prerequisites
- Rust 1.70+ with Cargo
- PostgreSQL 12+
- Modern web browser
- (Optional) Google Gemini AI API key

### Backend Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd MemberCommons
   ```

2. **Configure environment**
   ```bash
   cp config/settings.example.js config/settings.js
   # Edit config/settings.js with your API keys and database settings
   ```

3. **Set up database**
   ```bash
   # Create PostgreSQL database
   createdb ModelEarthDB
   
   # Run schema setup
   psql ModelEarthDB < sql/suitecrm-postgres.sql
   ```

4. **Configure environment variables**
   ```bash
   export DATABASE_URL="postgresql://sqladmin@model-earth-server.database.windows.net/ModelEarthDB"
   export GEMINI_API_KEY="your-gemini-api-key"
   export SERVER_HOST="127.0.0.1"
   export SERVER_PORT="8081"
   ```

5. **Initialize database schema**
   ```bash
   cargo run -- init-db
   ```
Or 

      SERVER_PORT=8081 cargo run -- serve

6. **Start the backend server**
   ```bash
   cargo run -- serve
   ```

### Frontend Setup

1. **Serve the frontend**
   ```bash
   # Option 1: Simple HTTP server
   python -m http.server 3000
   
   # Option 2: Node.js serve
   npx serve .
   
   # Option 3: PHP server
   php -S localhost:3000
   ```

2. **Open in browser**
   ```
   http://localhost:3000
   ```

## 🔧 Configuration

### API Configuration
Update the API base URL in your frontend:
```javascript
const API_BASE = 'http://localhost:8081/api';
```

### Database Configuration
The application supports Azure and Google Cloud PostgreSQL:
```rust
// In Cargo.toml or environment variables
DATABASE_URL=postgresql://sqladmin@model-earth-server.database.windows.net/ModelEarthDB
```

### Authentication Providers
Configure OAuth providers in `config/settings.js`:
- Google OAuth 2.0
- GitHub OAuth
- LinkedIn OAuth
- Email/password authentication

## 🚀 Usage

### For Developers
1. **Sign up** using Google, GitHub, LinkedIn, or email
2. **Complete your profile** with skills and interests
3. **Take the policy survey** to find aligned projects
4. **Browse opportunities** or use AI search to find projects
5. **Join teams** and collaborate on local innovation projects

### For Project Managers
1. **Post activities** with detailed requirements
2. **Recruit team members** based on skills and interests
3. **Track project progress** with built-in timelines
4. **Manage team collaboration** with integrated tools

### For Organizations
1. **Register your organization** and get verified
2. **Post funded opportunities** with Innovation Bond support
3. **Connect with local talent** through the directory
4. **Track impact metrics** across multiple projects

## 🎯 Target Audience

**Primary Users**: Technical coders and programmers working on Innovation Bond projects
**Use Cases**: 
- Government AI modernization projects
- Local community development initiatives
- Civic technology implementations
- Public-private partnership collaborations

## 🔮 AI Integration

### Gemini AI Features
- **Natural Language Search**: "Find React developers in Atlanta working on AI projects"
- **Smart Recommendations**: Personalized project and team suggestions
- **Insight Generation**: Analysis of team dynamics and project progress
- **Content Enhancement**: AI-assisted project descriptions and requirements

### Implementation
```javascript
// Example AI search query
const aiResponse = await queryGeminiAI(`
    Based on this search: "${userQuery}"
    Find relevant projects matching:
    - Technical skills: ${userSkills}
    - Location: ${userLocation}
    - Interests: ${userInterests}
`);
```

## 🔒 Security Features

- **JWT Authentication**: Secure token-based user sessions
- **OAuth Integration**: Trusted third-party authentication
- **Data Encryption**: Secure transmission and storage
- **Privacy Controls**: User-controlled data sharing preferences
- **Admin Demo Mode**: Safe demonstration without authentication

## 📊 Survey System

### Policy Preferences
- 20 "hot topic" policy questions with 5-point Likert scale
- Sankey chart visualization of response correlations
- Automatic matching with aligned projects and collaborators

### Interest Areas
- 5-star ratings for 20+ focus areas
- Categories include: Technology Innovation, Environmental Sustainability, Education, Healthcare Access, Economic Growth
- Personalized project recommendations based on ratings

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🆘 Support

- **Documentation**: Check the `/documentation` tab in the application
- **Issues**: Report bugs via GitHub Issues
- **Community**: Join our Discord server for real-time support
- **Email**: support@membercommons.org

## 🔄 Development Roadmap

### Phase 1 (Current)
- ✅ Core project management features
- ✅ Team collaboration tools
- ✅ AI-powered search and recommendations
- ✅ Survey and preference system

### Phase 2 (Coming Soon)
- 🔄 Real-time messaging and notifications
- 🔄 Advanced project timeline visualization
- 🔄 Integration with GitHub/GitLab
- 🔄 Mobile app development

### Phase 3 (Future)
- 📋 Blockchain-based reputation system
- 📋 Advanced analytics dashboard
- 📋 API marketplace for third-party integrations
- 📋 Multi-language support

---

**Built with ❤️ for the Innovation Bond community**

*Connecting technical talent with local impact projects to build the future of government technology.*