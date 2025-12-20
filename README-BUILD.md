# XDM Project Build Guide

This project provides multiple build methods to meet different requirements, from fully automated to manual configuration.

## 🚀 Recommended Solution: Simple Build (Most Reliable)

### If your system already has Java installed
1. **Double-click `simple-build.bat`**
   - Automatically detects system Java
   - Downloads and configures Maven
   - Builds the project
   - **This is the most reliable method**

### If your system doesn't have Java
1. **Download OpenJDK 11**
   - Visit: https://adoptium.net/temurin/releases/
   - Select: Version 11.x.x, HotSpot, jdk, Windows, x64, .zip
   - Extract to `tools\jdk\` directory

2. **Double-click `simple-build.bat`**
   - Automatically configures Maven
   - Builds the project

## 🔧 Alternative Solutions

### Option 1: Fixed Full Auto Setup
1. **Double-click `setup-tools-fixed.bat`**
   - Downloads OpenJDK 11.0.29 (English version)
   - Downloads Maven
   - Configures all tools

2. **Double-click `build.bat`**
   - Builds the project

### Option 2: Quick Setup
1. **Double-click `quick-setup.bat`**
   - Only downloads Maven
   - Detects system Java
   - More lightweight approach

2. **Double-click `build.bat`**
   - Builds the project

## 📁 Build Scripts Description

### simple-build.bat - Simple Build (Most Recommended)
**Features:**
- Lightweight, only downloads Maven
- Intelligently detects system Java environment
- Low failure rate, simple configuration
- **Best choice for most users**

### setup-tools-fixed.bat - Fixed Full Auto Setup
**Features:**
- Downloads OpenJDK 11.0.29 (English output, no encoding issues)
- Downloads Maven
- Fully automated but may be affected by network
- **Good choice for users with good network**

### build.bat - Project Build Script
**Function:**
- Automatically detects JDK location (project directory > system environment)
- Configures JAVA_HOME and PATH
- Executes Maven build process: clean → compile → package
- Generates executable JAR file

## 🎯 Directory Structure

```
d:\code\xdm-7.2.11\
├── app\                     # XDM project source code
├── tools\                   # Portable tools directory
│   ├── jdk\                 # OpenJDK directory (if installed)
│   ├── apache-maven-3.8.8\  # Maven (auto downloaded)
│   └── settings.xml         # Maven configuration file
├── simple-build.bat         # Simple build script (recommended)
├── setup-tools-fixed.bat    # Fixed full auto setup script
├── build.bat               # Project build script
└── README-BUILD.md         # This documentation
```

## 🔄 Build Process Selection

### Method A: Simple Build (Recommended for most users)
```batch
# Single step: simple-build.bat
simple-build.bat
```

### Method B: Fixed Full Auto Setup (Good network users)
```batch
# Step 1: full setup
setup-tools-fixed.bat

# Step 2: build project
build.bat
```

### Method C: Manual Configuration
```batch
# 1. Manually download JDK and extract to tools\jdk\
# 2. Run Maven download
# 3. Run build
build.bat
```

## 📋 Build Verification

### Success Indicators
After successful build, you'll see:
```
========================================
Build Completed Successfully!
========================================

JAR file location:
  d:\code\xdm-7.2.11\app\target\xdman.jar

File size:
  XXXXXXXX bytes

To run XDM:
  java -jar "d:\code\xdm-7.2.11\app\target\xdman.jar"
```

### Test Run
```cmd
java -jar app\target\xdman.jar
```

If you see the XDM download manager GUI interface, the build is completely successful!

## 🛠️ Troubleshooting

### Common Issues and Solutions

**1. Maven Download Failed**
```
Issue: Network connection problem or download timeout
Solution:
- Check network connection
- Use VPN or proxy
- Download Maven manually: https://archive.apache.org/dist/maven/maven-3/3.8.8/binaries/apache-maven-3.8.8-bin.zip
```

**2. OpenJDK Download Failed**
```
Issue: Automatic OpenJDK download failed
Solution:
- Use simple-build.bat + manual JDK download
- Visit https://adoptium.net/temurin/releases/ to download
- Or use system-installed Java
```

**3. Build Failed**
```
Issue: Maven compilation error
Solution:
- Check JDK version (need 11+)
- Clean Maven cache: mvn dependency:purge-local-repository
- Check detailed error messages
```

**4. Permission Issues**
```
Issue: Access denied
Solution:
- Run scripts as administrator
- Check antivirus software settings
- Ensure write permissions
```

**5. Chinese Character Encoding Issues**
```
Issue: Chinese characters display as garbled text
Solution:
- Use English scripts: setup-tools-fixed.bat, build.bat
- Or use simple-build.bat which has no encoding issues
```

### Manual Intervention Steps

If automatic configuration fails, you can manually complete:

**1. Manually Download Maven**
```cmd
# Download from: https://archive.apache.org/dist/maven/maven-3/3.8.8/binaries/apache-maven-3.8.8-bin.zip
# Extract to tools directory, rename to apache-maven-3.8.8
```

**2. Manually Download OpenJDK**
```cmd
# Download from: https://adoptium.net/temurin/releases/
# Select: Version 11.x.x, HotSpot, jdk, Windows, x64, .zip
# Extract to tools\jdk directory
```

**3. Run Build**
```cmd
build.bat
```

## 🌍 Network Environment Adaptation

### Corporate Network Environment
If your company has firewall or proxy:
1. Configure Maven to use internal mirrors
2. Use system Java environment (no download needed)
3. Configure proxy settings

### Domestic Network Optimization
- Maven configuration already uses Aliyun mirror
- Prioritize domestic mirrors for download
- Support multiple OpenJDK download sources

## 🎯 Advanced Configuration

### Using Different JDK Versions
Edit the JDK detection logic in build scripts, or manually specify:
```batch
set JAVA_HOME=tools\jdk\jdk-17.0.1
```

### Custom Maven Configuration
Edit `tools\settings.xml`:
```xml
<mirrors>
  <mirror>
    <id>company-repo</id>
    <mirrorOf>*</mirrorOf>
    <url>http://company-maven/artifactory/repo</url>
  </mirror>
</mirrors>
```

### Skip Test Build
Modify commands in `build.bat`:
```batch
mvn package -DskipTests  # Skip tests (default)
mvn package              # Include tests
mvn compile              # Compile only
```

## 📞 Technical Support

The build system is designed for high reliability. If you encounter issues:

1. **First try**: `simple-build.bat` + manual JDK download
2. **Check environment**: Java version, network connection, disk space
3. **Check logs**: Detailed error messages usually point to the problem
4. **Alternative**: Use system Java environment (if already installed)

After completing the build, you will get a completely independent XDM download manager that can run on any Windows system.

## 💡 Tips

- First build may need to download many dependencies, please be patient
- The built JAR file contains all dependencies and can run independently
- You can copy the entire project folder to other Windows machines to use
- It's recommended to keep the tools directory to avoid re-downloading tools
- **If you encounter encoding issues, use the English scripts (`simple-build.bat` or `setup-tools-fixed.bat`)**

## 🎯 Quick Start Commands

### For Users with Java Already Installed:
```cmd
simple-build.bat
```

### For Users Without Java:
1. Download JDK from https://adoptium.net/temurin/releases/
2. Extract to `tools\jdk\`
3. Run:
```cmd
simple-build.bat
```

### For Network Environments with Download Issues:
```cmd
quick-setup.bat
# Then manually download JDK to tools\jdk\
build.bat