# Desktop Cleaner 🗂️

An automated file organization tool that monitors your Downloads, Pictures, and Desktop folders and automatically sorts files into categorized directories based on their file extensions.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [How It Works](#how-it-works)
- [Installation](#installation)
- [Usage](#usage)
- [File Organization Structure](#file-organization-structure)
- [Supported File Types](#supported-file-types)
- [Configuration](#configuration)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)


## 🌟 Overview

Desktop Cleaner is a Python-based file management utility that automatically organizes your files by monitoring specified directories and moving files to categorized folders based on their extensions. It runs continuously in the background and organizes files as soon as they appear in the watched directories.

## ✨ Features

- **Real-time Monitoring**: Uses watchdog to monitor file system events
- **Automatic Organization**: Sorts files by type into predefined categories
- **Date-based Structure**: Creates year/month subdirectories for better organization
- **Duplicate Handling**: Automatically renames files to prevent overwrites
- **Multi-directory Support**: Monitors Downloads, Pictures, and Desktop simultaneously
- **Extensive File Type Support**: Handles 80+ file extensions across multiple categories
- **Background Operation**: Runs silently in the background with minimal resource usage

## 🔧 How It Works

1. **File Detection**: The tool monitors your Downloads, Pictures, and Desktop folders for new files
2. **Extension Recognition**: When a file is detected, it identifies the file type by its extension
3. **Category Assignment**: Files are categorized into groups like media, documents, programming files, etc.
4. **Date Organization**: Files are placed in year/month subdirectories (e.g., `2024/JAN/`)
5. **Conflict Resolution**: If a file with the same name exists, it adds a number suffix to make it unique
6. **File Movement**: The file is moved to its designated organized location

## 📦 Installation

### Prerequisites

- Python 3.6 or higher
- pip (Python package installer)

### Install Dependencies

```bash
pip install watchdog
```

### Clone the Repository

```bash
git clone https://github.com/yourusername/desktop-cleaner.git
cd desktop-cleaner
```

## 🚀 Usage

### Basic Usage

1. Navigate to the project directory:
   ```bash
   cd desktop_cleaner
   ```

2. Run the cleaner:
   ```bash
   python cleandesk.py
   ```

3. The tool will start monitoring your directories. You'll see it running until you stop it with `Ctrl+C`.

### Running as a Background Service

**On Linux/macOS:**
```bash
nohup python cleandesk.py &
```

**On Windows:**
You can create a batch file or use Task Scheduler to run it automatically on startup.

## 📁 File Organization Structure

Files are organized in the following structure:

```
~/Downloads/holder of things/
├── 2024/
│   ├── JAN/
│   │   ├── media/
│   │   │   ├── images/
│   │   │   ├── audio/
│   │   │   └── video/
│   │   ├── text/
│   │   │   ├── pdf/
│   │   │   ├── microsoft/
│   │   │   └── presentations/
│   │   ├── programming/
│   │   │   ├── python/
│   │   │   ├── java/
│   │   │   └── database/
│   │   └── other/
│   │       ├── compressed/
│   │       ├── executables/
│   │       └── internet/
│   └── FEB/
│       └── [same structure]
└── 2025/
    └── [same structure]
```

## 📄 Supported File Types

### Media Files
- **Images**: `.jpg`, `.jpeg`, `.png`, `.gif`, `.bmp`, `.svg`, `.tiff`, `.psd`, `.ai`, `.cr2`
- **Audio**: `.mp3`, `.wav`, `.ogg`, `.wma`, `.m3u`, `.midi`, `.aif`
- **Video**: `.mp4`, `.avi`, `.mkv`, `.mov`, `.wmv`, `.flv`, `.3gp`

### Documents
- **Text**: `.txt`, `.rtf`, `.tex`, `.odt`
- **PDF**: `.pdf`
- **Microsoft Office**: `.doc`, `.docx`, `.xls`, `.xlsx`, `.ppt`, `.pptx`
- **Presentations**: `.key`, `.odp`, `.pps`

### Programming Files
- **Python**: `.py`
- **Java**: `.java`, `.class`
- **C/C++**: `.c`, `.h`
- **Web**: `.html`, `.css`, `.js`, `.php`, `.asp`
- **Database**: `.csv`, `.sql`, `.json`, `.xml`, `.db`
- **Shell**: `.sh`

### Other Categories
- **Compressed**: `.zip`, `.rar`, `.7z`, `.tar.gz`
- **Executables**: `.exe`, `.apk`, `.jar`, `.bat`
- **Fonts**: `.ttf`, `.otf`, `.fnt`
- **System**: `.dll`, `.sys`, `.ini`, `.ico`

## ⚙️ Configuration

### Customizing Watch Directories

Edit the `cleandesk.py` file to modify watched directories:

```python
# Current default paths
watch_path_1 = Path.home() / 'Downloads'
watch_path_2 = Path.home() / 'Pictures'
watch_path_3 = Path.home() / 'Desktop'

# Destination directories
destination_root_1 = Path.home() / 'Downloads/holder of things'
destination_root_2 = Path.home() / 'Pictures/holder of things'
destination_root_3 = Path.home() / 'Desktop/holder of things'
```

### Adding New File Types

Edit `extensions.py` to add new file extensions:

```python
extension_paths = {
    '.your_extension': 'category/subcategory',
    # Add your custom extensions here
}
```

### Changing Destination Folder Names

Modify the destination paths in `cleandesk.py` to use different folder names:

```python
destination_root_1 = Path.home() / 'Downloads/Organized Files'
```

## 🛠️ Troubleshooting

### Common Issues

1. **Permission Errors**
   - Ensure Python has permission to read/write in the target directories
   - On macOS, you might need to grant Terminal full disk access

2. **Files Not Moving**
   - Check if the file extension is listed in `extensions.py`
   - Verify the destination directory exists and is writable

3. **Script Stops Unexpectedly**
   - Check for file system errors or insufficient disk space
   - Review the console output for error messages

### Debug Mode

Add print statements to `EventHandler.py` for debugging:

```python
def on_modified(self, event):
    print(f"Event detected: {event}")
    # ... rest of the code
```

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/amazing-feature`
3. **Add new file types** to `extensions.py`
4. **Improve the organization logic** in `EventHandler.py`
5. **Add error handling** and logging
6. **Write tests** for new functionality
7. **Commit your changes**: `git commit -m 'Add amazing feature'`
8. **Push to the branch**: `git push origin feature/amazing-feature`
9. **Open a Pull Request**

### Ideas for Contributions

- Add a GUI interface
- Implement configuration file support
- Add logging functionality
- Create platform-specific installers
- Add support for cloud storage synchronization
- Implement undo functionality
- Add file preview before moving

## 📈 Future Enhancements

- [ ] GUI interface with system tray integration
- [ ] Configuration file support (YAML/JSON)
- [ ] Logging and activity history
- [ ] Undo functionality
- [ ] Cloud storage integration
- [ ] Machine learning-based file categorization
- [ ] Email notifications for organized files
- [ ] Scheduled cleanup routines

## ⚠️ Important Notes

- **Backup your files** before running the tool for the first time
- The tool **moves files** (not copies), so they will be relocated from their original position
- **Large files** might take a moment to process
- The tool runs **continuously** until manually stopped

## 📋 System Requirements

- **Operating System**: Windows, macOS, or Linux
- **Python**: 3.6 or higher
- **RAM**: Minimal (< 50MB)
- **Storage**: Depends on files being organized
- **Permissions**: Read/write access to monitored directories

