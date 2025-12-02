# Installation Guide

This guide will help you install and set up EduBots on your computer.

## Prerequisites

Before installing EduBots, make sure you have:

- A computer running Windows, macOS, or Linux
- At least 4GB of RAM
- 2GB of free disk space
- Internet connection (for initial setup)
- Admin/sudo access for driver installation

## Method 1: Docker Installation (Recommended)

Docker is the easiest way to run EduBots.

### Step 1: Install Docker

#### Windows
1. Download [Docker Desktop for Windows](https://www.docker.com/products/docker-desktop)
2. Run the installer
3. Restart your computer
4. Launch Docker Desktop

#### macOS
1. Download [Docker Desktop for Mac](https://www.docker.com/products/docker-desktop)
2. Open the .dmg file and drag Docker to Applications
3. Launch Docker from Applications
4. Grant necessary permissions

#### Linux (Ubuntu/Debian)
```bash
# Update package index
sudo apt update

# Install Docker
sudo apt install docker.io

# Start Docker service
sudo systemctl start docker
sudo systemctl enable docker

# Add your user to docker group
sudo usermod -aG docker $USER

# Log out and back in for group changes to take effect
```

### Step 2: Run EduBots Container

Open Terminal (Mac/Linux) or PowerShell (Windows) and run:

```bash
docker run -d --name edubot -p 1999:1999 openroberta/lab
```

### Step 3: Access EduBots

Open your web browser and go to:
```
http://localhost:1999
```

You should see the EduBots interface!

## Method 2: Building from Source

For developers who want to build from source:

### Prerequisites
- Java 11 or higher
- Maven 3.6+
- Git

### Build Steps

```bash
# Clone repository
git clone https://github.com/rcs-robo/edubots.git
cd edubots

# Build with Maven
mvn clean install

# Run the server
cd openroberta-lab/OpenRobertaServer
mvn exec:java
```

## Installing OpenRoberta Connector

To connect physical robots via USB, install the OpenRoberta Connector:

### Step 1: Install Java

#### Windows
1. Download [Java 17](https://adoptium.net/)
2. Run installer
3. Verify: Open cmd and run `java -version`

#### macOS
```bash
# Using Homebrew
brew install openjdk@17

# Add to PATH
echo 'export PATH="/opt/homebrew/opt/openjdk@17/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

#### Linux
```bash
sudo apt install openjdk-17-jre
```

### Step 2: Download Connector

1. Download the latest [OpenRobertaConnector.jar](https://github.com/OpenRoberta/openroberta-connector/releases)
2. Save to a convenient location (e.g., Desktop)

### Step 3: Run Connector

#### Windows
- Double-click the JAR file
- Or from cmd: `java -jar OpenRobertaConnector.jar`

#### macOS/Linux
```bash
java -jar OpenRobertaConnector.jar
```

The connector will show a system tray icon when running.

## Installing USB Drivers

### Arduino Nano (CH340 chip)

Many Arduino Nano clones use the CH340 USB chip.

#### Windows
1. Download [CH340 Driver](https://sparks.gogo.co.nz/ch340.html)
2. Extract and run installer
3. Restart computer

#### macOS
1. Download [CH340 Driver for Mac](https://github.com/adrianmihalko/ch340g-ch34g-ch34x-mac-os-x-driver)
2. Install the driver
3. Go to System Preferences → Security & Privacy
4. Click "Allow" for the driver
5. Restart Mac

#### Linux
Usually works out of the box. If not:
```bash
# Add user to dialout group
sudo usermod -a -G dialout $USER

# Log out and back in
```

## Verification

### Test Docker Installation
```bash
# Check if container is running
docker ps

# Check logs
docker logs edubot

# Access web interface
# Open browser to http://localhost:1999
```

### Test USB Connection
1. Connect your Arduino/robot via USB
2. Start OpenRoberta Connector
3. In EduBots web interface, click "Connect"
4. Your robot should appear in the list

## Troubleshooting

### Docker Issues

**Problem:** Port 1999 already in use
```bash
# Find what's using the port
lsof -i :1999  # Mac/Linux
netstat -ano | findstr :1999  # Windows

# Use a different port
docker run -d --name edubot -p 8080:1999 openroberta/lab
# Access at http://localhost:8080
```

**Problem:** Container won't start
```bash
# Check Docker logs
docker logs edubot

# Remove and recreate container
docker rm edubot
docker run -d --name edubot -p 1999:1999 openroberta/lab
```

### USB Connection Issues

**Problem:** Robot not detected
- Make sure OpenRoberta Connector is running (check system tray)
- Try a different USB cable
- Try a different USB port
- Verify driver installation
- On Windows: Check Device Manager for COM port
- On Mac/Linux: Run `ls /dev/tty*` to see serial ports

**Problem:** Permission denied (Linux)
```bash
# Add user to dialout group
sudo usermod -a -G dialout $USER
# Log out and back in
```

### macOS Security

If macOS blocks the connector or drivers:
1. System Preferences → Security & Privacy
2. Click lock icon and enter password
3. Click "Allow" for blocked software
4. Restart application

## Next Steps

Once installed:
1. [Connect Your Robot](Connecting-Your-Robot)
2. [Create Your First Program](First-Program)
3. [Explore Tutorials](Home#tutorials)

## Updating EduBots

### Docker Update
```bash
# Stop current container
docker stop edubot
docker rm edubot

# Pull latest version
docker pull openroberta/lab

# Start new container
docker run -d --name edubot -p 1999:1999 openroberta/lab
```

### Source Update
```bash
cd edubots
git pull
mvn clean install
```

---

Need help? Check [Common Issues](Common-Issues) or [ask on GitHub](https://github.com/rcs-robo/edubots/issues).
