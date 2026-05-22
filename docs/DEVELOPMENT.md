# Development Guide

## Prerequisites

- Node.js v18 or later
- npm or yarn package manager
- MongoDB v5.0 or later (running on port 27017)
- Git
- A code editor (VS Code recommended)

## Environment Setup

### 1. Clone the Repository

```bash
git clone https://github.com/Babashova/skills-build-applications-w-copilot-agent-mode.git
cd skills-build-applications-w-copilot-agent-mode/octofit-tracker
```

### 2. Install MongoDB

**macOS (using Homebrew):**
```bash
brew tap mongodb/brew
brew install mongodb-community
brew services start mongodb-community
```

**Windows:**
Download from https://www.mongodb.com/try/download/community

**Linux (Ubuntu):**
```bash
sudo apt-get install -y mongodb
sudo systemctl start mongodb
```

### 3. Backend Setup

```bash
cd backend

# Install dependencies
npm install

# Create .env file
cp .env.example .env

# Start development server
npm run dev
```

The backend server will run on `http://localhost:8000`

### 4. Frontend Setup

Open a new terminal:

```bash
cd frontend

# Install dependencies
npm install

# Start development server
npm run dev
```

The frontend will run on `http://localhost:5173`

## Development Workflow

### Branch Strategy

1. Create a feature branch from `main`:
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. Make your changes and commit:
   ```bash
   git add .
   git commit -m "feat: add new feature"
   ```

3. Push to your fork and create a pull request

### Commit Message Convention

Follow the Conventional Commits format:

- `feat:` for new features
- `fix:` for bug fixes
- `docs:` for documentation changes
- `refactor:` for code refactoring
- `test:` for test additions/changes
- `chore:` for build/tooling changes

Example:
```bash
git commit -m "feat: add user authentication endpoint"
```

### Code Style

#### Frontend
- Use React functional components with hooks
- Use TypeScript for type safety
- Follow ESLint rules: `npm run lint`

#### Backend
- Use Express middleware patterns
- Implement proper error handling
- Use TypeScript strict mode
- Follow ESLint rules: `npm run lint`

## Testing

### Backend

```bash
cd backend

# Run tests (to be implemented)
npm test

# Run linter
npm run lint

# Type check
npx tsc --noEmit
```

### Frontend

```bash
cd frontend

# Run tests (to be implemented)
npm test

# Run linter
npm run lint

# Build for production
npm run build
```

## Debugging

### Backend Debugging

Using VS Code's built-in debugger:

1. Install the `Debugger for Chrome` extension
2. Create `.vscode/launch.json`:
   ```json
   {
     "version": "0.2.0",
     "configurations": [
       {
         "type": "node",
         "request": "launch",
         "name": "Launch Server",
         "program": "${workspaceFolder}/backend/src/index.ts",
         "restart": true,
         "console": "integratedTerminal",
         "internalConsoleOptions": "neverOpen"
       }
     ]
   }
   ```
3. Press F5 to start debugging

### Frontend Debugging

- Open Chrome DevTools (F12)
- Use React Developer Tools extension
- Check Network tab for API calls
- View Console for errors/logs

### MongoDB Debugging

Use MongoDB Compass to inspect data:
1. Download from https://www.mongodb.com/products/compass
2. Connect to `mongodb://localhost:27017`
3. Browse collections and documents

## Building for Production

### Backend

```bash
cd backend
npm run build
npm start
```

### Frontend

```bash
cd frontend
npm run build
npm run preview
```

## Troubleshooting

### MongoDB Connection Failed

```bash
# Check if MongoDB is running
ps aux | grep mongod

# Start MongoDB
brew services start mongodb-community  # macOS
sudo systemctl start mongodb           # Linux
```

### Port Already in Use

**Backend (8000):**
```bash
lsof -ti:8000 | xargs kill -9
```

**Frontend (5173):**
```bash
lsof -ti:5173 | xargs kill -9
```

**MongoDB (27017):**
```bash
lsof -ti:27017 | xargs kill -9
```

### Module Not Found

```bash
# Clear node_modules and reinstall
rm -rf node_modules package-lock.json
npm install
```

### TypeScript Errors

```bash
# Type check
npx tsc --noEmit

# Fix common issues
npm run lint -- --fix
```

## Development Tools

### VS Code Extensions

Recommended extensions:
- ES7+ React/Redux/React-Native snippets
- ESLint
- Prettier - Code formatter
- Thunder Client (for API testing)
- MongoDB for VS Code

### Command Line Tools

```bash
# View backend logs
npm run dev -- --verbose

# View frontend build details
npm run build -- --debug
```

## Performance Optimization

### Frontend
- Use React.memo for component optimization
- Implement code splitting with React.lazy
- Use production build for testing

### Backend
- Implement database indexing
- Use caching strategies
- Monitor API response times

## Git Workflow

```bash
# Update your fork
git fetch upstream
git merge upstream/main

# Push changes
git push origin feature/your-feature

# Pull latest from main
git pull origin main
```

## Resources

- [React Documentation](https://react.dev)
- [Express Documentation](https://expressjs.com)
- [MongoDB Documentation](https://docs.mongodb.com)
- [Vite Documentation](https://vitejs.dev)
- [TypeScript Documentation](https://www.typescriptlang.org/docs)
