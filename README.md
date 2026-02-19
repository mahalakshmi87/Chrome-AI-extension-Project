# AI Code Generator Extension

A powerful Chrome extension that leverages Generative AI to automatically generate test automation code from DOM elements. This tool streamlines test automation development by analyzing webpage elements and generating production-ready code in multiple programming languages and frameworks.

## 🎯 Features

### Code Generation
- **Multiple Framework Support**
  - Selenium (Java, C#, Python)
  - Playwright (JavaScript/TypeScript)
  - Cypress (JavaScript)
  - Puppeteer (JavaScript)

- **Generation Modes**
  - **Cucumber Feature Files** - BDD-style test scenarios with Scenario Outlines and realistic data
  - **Page Object Model (POM)** - Maintainable, reusable Selenium Java classes
  - **Step Definitions** - Complete Cucumber step definitions with WebDriver implementation
  - **Standalone Code** - Isolated code snippets for quick implementation

### DOM Element Inspection
- **Interactive Inspector Tool** - Click to select webpage elements
- **Multi-element Selection** - Select multiple DOM elements simultaneously
- **HTML Preview** - View and copy selected DOM content
- **Real-time Highlighting** - Visual feedback during element selection

### AI Provider Integration
- **Groq API** - High-speed model inference
  - deepseek-r1-distill-llama-70b
  - llama-3.3-70b-versatile
- **OpenAI API** - Advanced models
  - GPT-4o
  - GPT-4o Mini
  
### Configuration Management
- **Language Binding Selection** - Java, C#, Python, TypeScript
- **Browser Engine Selection** - Selenium, Playwright, Cypress, Puppeteer
- **API Key Management** - Secure storage of provider credentials
- **GitHub Integration** - Connect to repositories for code management (future feature)

### User Interface
- **Side Panel Integration** - Seamless VS Code-like side panel experience
- **Tabbed Interface** - Separate Code Generator and Settings tabs
- **Dark Theme Support** - Customizable color scheme
- **Syntax Highlighting** - Prism.js for code blocks (Java, Gherkin, TypeScript)
- **Markdown Rendering** - Marked.js for rich text support
- **Chat-like Interface** - Conversational code generation workflow

## 📋 Project Structure

```
ai-extension/
├── manifest.json                 # Chrome extension manifest (v3)
├── panel.html                    # Main UI template
├── bg.js                         # Background service worker
├── src/
│   ├── config/
│   │   ├── appConfig.js         # Application configuration & color scheme
│   │   └── configUtils.js       # Config utilities for style application
│   ├── content/
│   │   ├── content.js           # DOM inspection & element selection
│   │   └── content-script.js    # Alternative DOM observer implementation
│   ├── scripts/
│   │   ├── chat.js              # Main chat UI logic & message handling
│   │   ├── popup.js             # Extension popup/panel initialization
│   │   ├── prompts.js           # AI prompt templates (ICE POT format)
│   │   ├── tabs.js              # Tab switching functionality
│   │   ├── init-colors.js       # Color initialization module
│   │   ├── init-config.js       # Config initialization module
│   │   └── api/
│   │       ├── groq-api.js      # Groq API integration
│   │       ├── openai-api.js    # OpenAI API integration
│   │       └── testleaf-api.js  # Testleaf API integration
│   └── styles/
│       ├── chat.css             # Chat interface styles
│       ├── sidepanel.css        # Side panel styles
│       ├── styles.css           # Global styles
│       └── vars.css             # CSS custom properties
├── lib/
│   ├── css/
│   │   └── all.min.css          # Font Awesome icons
│   ├── marked/
│   │   └── marked.min.js        # Markdown parser
│   └── prism/
│       ├── prism.js             # Syntax highlighter core
│       ├── prism-gherkin-min.js # Gherkin language support
│       ├── prism-typescript.js  # TypeScript language support
│       └── prism-tomorrow.css   # Dark theme for syntax highlighting
└── assets/
    └── images/
        └── logo-small.png       # Extension icon
```

## 🚀 Installation & Setup

### Prerequisites
- Chrome/Chromium browser (v90+)
- API keys from at least one provider:
  - [Groq API](https://console.groq.com/keys)
  - [OpenAI API](https://platform.openai.com/api-keys)
  - Client specific account credentials

### Installation Steps

1. **Clone the Repository**
   ```bash
   git clone https://github.com/mahalakshmi87/GenAI-Tool-development.git
   cd ai-extension
   ```

2. **Load Extension in Chrome**
   - Open `chrome://extensions/` in your browser
   - Enable **Developer mode** (top-right toggle)
   - Click **Load unpacked**
   - Select the `ai-extension` folder
   - The extension will appear in your extensions list

3. **Configure API Keys**
   - Click the extension icon (or open the side panel)
   - Go to **Settings** tab
   - Select your preferred **LLM Provider**
   - Choose a **Model**
   - Enter your API key
   - Click **Test Connection** (optional)

## 💻 Usage Guide

### Basic Workflow

1. **Navigate to Target Website**
   - Open any website you want to generate tests for

2. **Open Side Panel**
   - Click the extension icon in the toolbar
   - The side panel opens on the right side

3. **Inspect Elements**
   - Click the **Inspect** button to activate element selection mode
   - Hover over elements to preview (highlighted with dashed outline)
   - Click to select an element (solid outline with background)
   - Click multiple times to select multiple elements

4. **Configure Generation Settings**
   - Go to **Settings** tab
   - Choose **Language Binding** (Java, C#, Python, TypeScript)
   - Choose **Browser Engine** (Selenium, Playwright, Cypress, Puppeteer)
   - Select your preferred **AI Model**

5. **Generate Code**
   - Return to **Code Generator** tab
   - (Optional) Add context in the text area
   - Select generation mode:
     - ✓ **Feature File** - Cucumber/Gherkin format
     - ✓ **Page Class** - Java Page Object Model
   - Click **Generate** button
   - View generated code in the chat area

6. **Copy & Use**
   - Click to copy code blocks to clipboard
   - Paste into your project

### Advanced Features

**Multi-Element Selection**
- Select multiple DOM elements in sequence
- All selected elements are processed together
- Useful for capturing complex UI components

**Prompt Customization**
- Add specific requirements in the input field before generating
- Provide test data expectations
- Specify naming conventions or patterns

**Code Snippet Viewing**
- Hover over code blocks to see syntax highlighting
- Code is automatically formatted with proper indentation
- Language-specific highlighting (Java, Gherkin, TypeScript)

## 🔧 Configuration

### App Configuration (`src/config/appConfig.js`)

Customize the application appearance and behavior:

```javascript
export const appConfig = {
  colors: {
    primary: '#ff6b2b',
    primaryLight: '#ff9966',
    accent: '#ff6b2b',
    success: '#4caf50',
    danger: '#f44336',
    darkBg: '#1e1e1e',
    panelBg: '#252526',
    // ... more colors
  }
};
```

### Prompt Templates (`src/scripts/prompts.js`)

Three main generation modes:

1. **SELENIUM_JAVA_PAGE_ONLY** - Page Object Model classes
2. **CUCUMBER_ONLY** - Feature files with scenario outlines
3. **CUCUMBER_WITH_SELENIUM_JAVA_STEPS** - Feature files + step definitions

Templates use ICE POT format:
- **Instructions** - Clear generation guidelines
- **Context** - DOM content and URL
- **Examples** - Sample output format
- **Persona** - Target audience specification
- **Output Format** - Expected code structure
- **Tone** - Writing style

## 🔌 API Integration

### Groq API
```javascript
// Configuration in popup.js
const groqModels = [
  'deepseek-r1-distill-llama-70b',
  'llama-3.3-70b-versatile'
];
```

### OpenAI API
```javascript
// Configuration in popup.js
const openaiModels = [
  'gpt-4o',
  'gpt-4o-mini'
];
```

### Message Flow
1. Content script captures selected DOM elements
2. Chat UI sends prompt + DOM content to API via background worker
3. API returns generated code
4. Response is parsed and displayed with syntax highlighting
5. User can copy or regenerate

## 📝 Key Components

### Content Script (`src/content/content.js`)
- Manages DOM element inspection
- Highlights elements on hover
- Tracks multi-element selection
- Communicates selection to panel via `chrome.runtime.sendMessage`

### Chat UI (`src/scripts/chat.js`)
- Handles user messages and code generation
- Manages conversation history
- Parses markdown responses
- Syntax highlights code blocks
- Provides inspector toggle and reset functionality

### Configuration Manager (`src/config/configUtils.js`)
- Single source of truth for styling
- Maps appConfig to CSS variables
- Ensures consistent theming across panels

### API Modules (`src/scripts/api/`)
- **groq-api.js** - Groq API client
- **openai-api.js** - OpenAI API client
- **testleaf-api.js** - Testleaf API client
- Standardized request/response handling

## 🎨 Styling

The extension uses modern CSS with custom properties:

- **Dynamic Color Scheme** - Colors defined in `appConfig.js`
- **CSS Variables** - Applied via `configUtils.js`
- **Responsive Design** - Adapts to different panel sizes
- **Syntax Highlighting** - Prism.js with "Tomorrow" dark theme

## 🔒 Permissions

The extension requests the following permissions:

- `storage` - Save API keys and settings
- `activeTab` - Access current tab information
- `scripting` - Inject content scripts
- `tabs` - Manage tab metadata
- `sidePanel` - Display side panel UI
- `<all_urls>` - Access any website for element inspection

## 🐛 Troubleshooting

### API Connection Issues
- Verify API key is correctly entered
- Check network connectivity
- Ensure API service is operational
- Review browser console for detailed errors

### Element Inspection Not Working
- Ensure inspector mode is activated (button shows active state)
- Check if page content is within an iframe (limited support)
- Refresh the page and try again

### Code Generation Failures
- Verify DOM content is properly selected
- Check API rate limits haven't been exceeded
- Review error message in console for specific issues
- Ensure selected model is supported for your language/framework

### Styling Issues
- Clear browser cache and reload extension
- Check CSS variables are properly applied
- Verify Font Awesome CDN is accessible

## 📦 Dependencies

### External Libraries
- **marked.js** - Markdown parsing and rendering
- **Prism.js** - Syntax highlighting
- **Font Awesome 6.5.1** - Icon library

### Browser APIs
- Chrome Extension Manifest V3
- Storage API
- Messaging API
- Content Scripts
- Service Workers

## 🔄 Version History

- **v2.1** - Current version with full feature set
- Multi-provider support (Groq, OpenAI, Testleaf)
- Enhanced UI with tabbed interface
- Improved DOM inspection

## 📄 License

This project is licensed under the MIT License - see LICENSE file for details.

## 👥 Contributing

Contributions are welcome! Please follow these steps:

1. Create a feature branch (`git checkout -b feature/amazing-feature`)
2. Commit your changes (`git commit -m 'Add amazing feature'`)
3. Push to the branch (`git push origin feature/amazing-feature`)
4. Open a Pull Request

## 🤝 Support

For issues, feature requests, or questions:
- Open an issue on the [GitHub repository](https://github.com/mahalakshmi87/Chrome-AI-extension-Project)
- Check existing issues for solutions
- Provide detailed reproduction steps

## 📧 Contact

For more information, contact the development team or visit the project repository.

---

**Happy Code Generation! 🚀**
