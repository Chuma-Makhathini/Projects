# Cybersecurity Awareness Chatbot

A modern Windows desktop application designed to educate users about cybersecurity best practices, provide actionable security tips, and enable effective management of security-related tasks.

## Overview

The Cybersecurity Awareness Chatbot is a comprehensive security education tool that combines an intelligent chat interface with practical task management capabilities. Users can ask questions about cybersecurity concepts, take quizzes to test their knowledge, and manage security-related reminders and tasks—all from a single, intuitive application.

## Key Features

- **Interactive Chat Interface**: Ask cybersecurity questions and receive detailed, contextual responses
- **Task Management**: Create, organize, and track security-related tasks with reminders
- **Assessment Quizzes**: Test and improve your cybersecurity knowledge
- **Activity Logging**: Maintain a record of your interactions and learning progress
- **Audio Notifications**: Customizable welcome sound and alerts

## Folder Structure

```
CybersecurityChatbot/
├── Chatbot/                      # Main application folder
│   ├── ArtDisplay.cs             # Visual elements and UI enhancements
│   ├── ChatbotBase.cs            # Core chatbot functionality
│   ├── InputValidator.cs         # Input validation and sanitization
│   ├── IResponder.cs             # Chatbot response interface
│   ├── MainWindow.xaml           # Main application window (UI)
│   ├── MainWindow.xaml.cs        # Application logic and event handlers
│   ├── Quiz.cs                   # Quiz engine and question management
│   ├── SecurityChatbot.cs        # Cybersecurity-specific implementation
│   └── greeting.wav              # Welcome notification sound
|   
└── README.md                     # This file
```

## System Requirements

- **Operating System**: Windows 10 or later
- **Runtime**: .NET 6.0 or later
- **IDE**: Visual Studio 2022 (recommended)

## Installation

1. Clone or download the repository
2. Open the solution file (`CybersecurityChatbot.sln`) in Visual Studio
3. Restore NuGet packages if prompted
4. Build the solution (`Ctrl+Shift+B`)
5. Run the application (`F5`)

## Configuration

The application automatically creates necessary files and folders on first launch. To customize:

- **Audio Notifications**: Replace `greeting.wav` in the project directory with your preferred audio file
- **Application Settings**: Modify settings located at `%APPDATA%\CybersecurityChatbot\settings.json`

## Usage Guide

### Getting Started

1. Type your question in the input box and press **Enter** or click **Send**
2. Start with `help` to view available commands
3. Use `topics` to explore available cybersecurity subjects

### Chat Commands

| Command | Purpose |
|---------|---------|
| `help` | Display available commands |
| `topics` | List available cybersecurity topics |
| `quiz` | Launch the quiz module |

### Task Management

**Creating Tasks:**
- Use the side panel to add new tasks
- Commands:
  - `Add task [title] with description [description]`
  - `Remind me to [task] in [time period]`
  - `Create task [title]`

**Managing Tasks:**
- Click the checkmark (✓) button to mark tasks as complete
- Click the (×) button to delete tasks

### Quiz Mode

1. Type `start quiz` to begin
2. Select answers from the options presented
3. View your score and feedback upon completion

## Usage Examples

### Chat Examples

**User**: What is phishing?  
**Bot**: 🎣 Phishing uses fake communications to steal sensitive information. Common variants include spear phishing (targeted attacks) and whaling (targeting high-level executives)...

**User**: Give me a password tip  
**Bot**: 💡 Tip: Create memorable passphrases like 'CorrectHorseBatteryStaple' instead of complex random characters for better security and usability...

**User**: I'm worried about malware  
**Bot**: Malware is a serious concern. I can help you understand various types and how to protect your systems...

### Task Management Examples

```
Add task Update passwords with description Change all important account passwords
Remind me to backup files in 3 days
Create task called Check firewall settings
```

### Quiz Example

```
Q: What should you do if you receive an email asking for your password?

1) Reply with your password
2) Delete the email
3) Report the email as phishing
4) Ignore it

Your Answer: 3) Report the email as phishing
✓ Correct! Reporting phishing emails helps prevent fraud and protects the wider community.
```

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Audio notifications not playing | Verify that `greeting.wav` exists in the application directory |
| UI not updating properly | Restart the application |
| Tasks not saving | Check file write permissions in `%APPDATA%\CybersecurityChatbot\` |
| Application crashes on startup | Ensure .NET 6.0 or later is installed and up to date |

## Technology Stack

- **Language**: C# (.NET 6.0)
- **UI Framework**: WPF (Windows Presentation Foundation)
- **Data Storage**: JSON-based configuration

## Support & Feedback

For issues, feature requests, or feedback, please open an issue in the repository.

## License

This project is provided as-is for educational and professional use in cybersecurity awareness.
