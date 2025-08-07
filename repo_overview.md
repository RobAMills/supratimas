# Supratimas - Repository Overview

## Project Description
**Supratimas** is a web-based analysis tool for Microsoft SQL Server query execution plans. It provides visual analysis and performance insights for SQL execution plans through an interactive web interface.

## Deployment Options
- **Web Application**: Standalone web app accessible via browser
- **SSMS Plugin**: Integration with SQL Server Management Studio (versions 2008-2018)

## Technology Stack
- **Frontend**: TypeScript, Knockout.js for data binding
- **Build System**: Gulp with custom target system
- **Styling**: LESS CSS preprocessor
- **Module System**: AMD (RequireJS)

## Project Structure

### Core Components

**Build System** (`gulpfile.js`):
- Uses Gulp with custom target system
- Builds multiple outputs: `web` and `ssms` targets  
- Handles TypeScript compilation, CSS (LESS), HTML processing

**Main Applications**:
- **Web App** (`src/webapp/`): Standalone web application
- **SSMS Plugin** (`src/ssms/`): Integration with SQL Server Management Studio

**Core Functionality** (`src/`):
- **SQL Plan Parser** (`sqlplan/`): Parses XML execution plans using SAX parser
- **App Logic** (`app/`): Plan visualization, analysis, and layout management
- **Code Generation** (`codegen/`): Generates TypeScript from XML schema models
- **Layout System** (`layout/`): Handles visual layout and scrolling of plan components

### Key Entry Points

**Web Application**:
```typescript
// src/webapp/app.ts
export function run(id?: string) {
    const app = new Application(id);
    ko.applyBindings(app, document.body);
}
```

**SSMS Integration**:
```typescript
// src/ssms/app.ts  
export function addPlan(planText: string) {
    let app: Application = ko.dataFor(document.body);
    if (!app) {
        app = new Application();
        ko.applyBindings(app, document.body);
    }
    app.showPlan(planText);
}
```

## Local Development Setup (Ubuntu Server)

### Prerequisites
```bash
# Install Node.js and npm
sudo apt update
sudo apt install nodejs npm

# Verify versions (project uses older dependencies)
node --version  # Should work with Node 10+
npm --version
```

### Setup Steps

1. **Install dependencies**:
```bash
npm install
```

2. **Build the project**:
```bash
# Build all targets
npm run build
# OR use gulp directly
npx gulp build
```

3. **Development with auto-rebuild**:
```bash
# Watch for changes and rebuild
npx gulp watch
# OR
npx gulp  # default task runs watch
```

### Serving the Application

The build outputs to `dist/` directory. Choose a web server option:

**Option 1 - Simple HTTP server**:
```bash
# Install a simple server
npm install -g http-server
# Serve from dist directory
cd dist && http-server -p 8080
```

**Option 2 - Python server**:
```bash
cd dist && python3 -m http.server 8080
```

**Option 3 - Nginx**:
Configure nginx to serve the `dist/web/` directory.

### Access Points
- Web app: `http://your-server:8080/webapp/`
- Main site: `http://your-server:8080/`

## Build Targets
- **Web Target** (`dist/web/`): Standalone web application
- **SSMS Target** (`dist/ssms/`): Files for SSMS plugin integration

## Core Workflow
1. Takes SQL execution plan XML as input
2. Parses XML using custom SAX parser (`src/sqlplan/saxparser.ts`)
3. Creates visual representation with interactive layout
4. Provides analysis tools for performance optimization

The project focuses on making SQL Server execution plans more accessible and analyzable through modern web technologies.