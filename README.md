# Supratimas - SQL Server Execution Plan Analyzer

**Supratimas** is a web-based analysis tool for Microsoft SQL Server query execution plans. It provides visual analysis and performance insights for SQL execution plans through an interactive web interface.

## Features

- **Visual Plan Analysis**: Interactive visualization of SQL Server execution plans
- **Performance Insights**: Cost analysis and performance bottleneck identification
- **Plan Navigation**: Zoom, pan, and detailed node inspection
- **Multiple View Modes**: Different perspectives for analyzing query execution
- **File Upload**: Support for loading .sqlplan files
- **Paste Support**: Direct paste of execution plan XML
- **SSMS Integration**: Plugin support for SQL Server Management Studio

## Technology Stack

- **Frontend**: TypeScript, Knockout.js for data binding
- **Build System**: Gulp with custom target system
- **Styling**: LESS CSS preprocessor
- **Module System**: AMD (RequireJS)

## Prerequisites

### Node.js Installation

#### Windows
1. Download Node.js from [nodejs.org](https://nodejs.org/)
2. Run the installer (.msi file)
3. Verify installation:
   ```cmd
   node --version
   npm --version
   ```

#### macOS
**Option 1: Official Installer**
1. Download Node.js from [nodejs.org](https://nodejs.org/)
2. Run the installer (.pkg file)

**Option 2: Homebrew**
```bash
brew install node
```

**Option 3: MacPorts**
```bash
sudo port install nodejs18
```

#### Ubuntu/Debian
**Option 1: NodeSource Repository (Recommended)**
```bash
# Update package index
sudo apt update

# Install Node.js 18.x
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

# Verify installation
node --version
npm --version
```

**Option 2: Ubuntu Package Manager**
```bash
sudo apt update
sudo apt install nodejs npm
```

**Option 3: Snap Package**
```bash
sudo snap install node --classic
```

#### CentOS/RHEL/Fedora
**CentOS/RHEL:**
```bash
# Enable NodeSource repository
curl -fsSL https://rpm.nodesource.com/setup_18.x | sudo bash -
sudo yum install -y nodejs npm
```

**Fedora:**
```bash
sudo dnf install nodejs npm
```

## Build Instructions

### 1. Clone and Setup

```bash
# Clone the repository
git clone <repository-url>
cd supratimas

# Install dependencies
npm install
```

### 2. Build the Project

#### Build All Targets
```bash
# Build both web and SSMS targets
npm run build
# OR
npx gulp build
```

#### Development with Auto-rebuild
```bash
# Watch for changes and rebuild automatically
npx gulp watch
# OR
npx gulp  # default task runs watch
```

### 3. Serve the Application

The build outputs to the `dist/` directory. Choose a web server option:

#### Option 1: Python HTTP Server (Cross-platform)
```bash
cd dist
python3 -m http.server 8080
# For Python 2.x: python -m SimpleHTTPServer 8080
```

#### Option 2: Node.js HTTP Server
```bash
# Install http-server globally
npm install -g http-server

# Serve from dist directory
cd dist && http-server -p 8080
```

#### Option 3: Local Development Server
```bash
# Install serve locally
npm install -g serve

# Serve the dist directory
serve -s dist -l 8080
```

### 4. Access the Application

- **Web app**: `http://localhost:8080/webapp/`
- **Main site**: `http://localhost:8080/`
- **Examples**: `http://localhost:8080/examples/`

## Build Targets

- **Web Target** (`dist/web/`): Standalone web application
- **SSMS Target** (`dist/ssms/`): Files for SSMS plugin integration

## Troubleshooting

### Node.js Version Compatibility
This project uses older dependencies that work best with Node.js 12-18. If you encounter issues:

1. **Check Node.js version**:
   ```bash
   node --version
   ```

2. **Use Node Version Manager (nvm)**:
   
   **Linux/macOS:**
   ```bash
   # Install nvm
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
   
   # Install and use Node.js 16
   nvm install 16
   nvm use 16
   ```
   
   **Windows (nvm-windows):**
   ```cmd
   # Download and install from: https://github.com/coreybutler/nvm-windows
   
   # Install and use Node.js 16
   nvm install 16.20.0
   nvm use 16.20.0
   ```

### Common Build Issues

#### Issue: "primordials is not defined"
**Solution**: Update graceful-fs dependency
```bash
npm install graceful-fs@4.2.0 --save-dev
```

#### Issue: "Task function must be specified"
**Solution**: The project has been updated to use Gulp 4. Ensure you're using the latest code.

#### Issue: Missing sax dependency
**Solution**: Install the sax package
```bash
npm install sax
```

#### Issue: Permission denied (npm global install)
**Linux/macOS Solution**:
```bash
# Use npx instead of global install
npx http-server dist -p 8080

# OR configure npm to use a different directory
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

## Development Workflow

1. **Make changes** to source files in `src/`, `css/`, or `html/`
2. **Run build** with `npx gulp build` or use watch mode with `npx gulp watch`
3. **Test changes** by refreshing the browser
4. **Debug** using browser developer tools

## Project Structure

```
├── src/                 # TypeScript source files
│   ├── webapp/         # Web application source
│   ├── ssms/           # SSMS plugin source
│   ├── app/            # Core application logic
│   └── sqlplan/        # SQL plan parsing logic
├── css/                # LESS stylesheets
├── html/               # HTML templates
├── gulp/               # Build system configuration
├── dist/               # Build output (generated)
│   ├── web/           # Web application build
│   └── ssms/          # SSMS plugin build
└── examples/           # Sample SQL execution plans
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test the build process
5. Submit a pull request

## Usage

### Loading SQL Execution Plans

1. **From File**: Click "Open Plan" and select a `.sqlplan` file
2. **Copy & Paste**: Paste execution plan XML directly into the textarea
3. **Examples**: Try the sample plans in the examples directory

### Analyzing Plans

- **Navigate**: Use zoom controls and pan around the plan
- **Inspect Nodes**: Click on any operation to see detailed information
- **View Modes**: Switch between different visualization perspectives
- **Performance**: Identify expensive operations and bottlenecks
- **Storage**: Examine table and index usage

### Keyboard Shortcuts

- **Zoom In**: `+` or mouse wheel up
- **Zoom Out**: `-` or mouse wheel down
- **Fit to Screen**: `F` key
- **Reset Zoom**: `R` key

## Browser Compatibility

- **Chrome**: 70+ (Recommended)
- **Firefox**: 65+
- **Safari**: 12+
- **Edge**: 79+

## Performance Tips

- For large execution plans, use the compact view mode
- Enable hardware acceleration in your browser for better performance
- Close other browser tabs when analyzing very complex plans

## FAQ

**Q: Can I use this with Azure SQL Database plans?**
A: Yes, Supratimas works with execution plans from Azure SQL Database, SQL Server, and Azure SQL Managed Instance.

**Q: Does this work offline?**
A: Yes, once built and served locally, the application works completely offline.

**Q: Can I integrate this with my own applications?**
A: Yes, the web application can be embedded or integrated into other web applications.

## Support

For issues, questions, or contributions:
1. Check the existing issues in the repository
2. Create a new issue with detailed information
3. Include your operating system, Node.js version, and error messages

## License

[License information - please check the repository for specific license details]
