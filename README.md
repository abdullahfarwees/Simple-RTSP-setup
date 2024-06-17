# Local RTSP Server Configuration

## Overview
This guide will help you set up a local RTSP server in just one minute. The server will use a local video file as its source and stream it in a loop. The output can be viewed using VLC Player.

## Requirements
- A video file (e.g., `BigBuckBunny.mp4`)
- [RTSP-SIMPLE-SERVER (mediamtx)](https://github.com/bluenviron/mediamtx)
- [FFmpeg](https://ffmpeg.org/download.html)
- [VLC Player](https://www.videolan.org/vlc/)


## Instructions

### Step 1: Save the Batch Script
Create a new file named `StartServer.bat` and copy the following code into it:

```batch
@echo off
REM Check if ffmpeg is available
ffmpeg -version >nul 2>&1
if %errorlevel% neq 0 (
    echo FFmpeg is not installed or not found in PATH.
    exit /b 1
)

REM Start the RTSP caster
start "RTSP Server" cmd /c "mediamtx"
timeout /t 3 /nobreak >nul

REM Start the FFMPEG piping
start "FFmpeg" cmd /c "ffmpeg -re -stream_loop -1 -i BigBuckBunny.mp4 -c:v copy -c:a copy -f rtsp rtsp://localhost:8554/mystream"
timeout /t 3 /nobreak >nul

REM Start VLC
start "VLC" vlc
```

### Step 2: Ensure Dependencies are Installed
- **RTSP-SIMPLE-SERVER (mediamtx)**: Ensure it is installed and available in your PATH.
- **FFmpeg**: Ensure it is installed and available in your PATH.
- **VLC Player**: Ensure it is installed.

### Step 3: Place the Video File
Ensure the video file (e.g., `BigBuckBunny.mp4`) is in the same directory as `StartServer.bat`.

### Step 4: Run the Batch Script
Double-click `StartServer.bat` to execute it. This will perform the following steps:
1. Check if FFmpeg is installed.
2. Start the RTSP server using `mediamtx`.
3. Start streaming the video file in a loop using FFmpeg to the RTSP server.
4. Launch VLC Player.

### Step 5: View the Stream in VLC Player
1. In VLC Player, press `CTRL+N` to open the "Open Media" dialog.
2. Go to the "Network" tab.
3. Paste the following URL: `rtsp://localhost:8554/mystream`.
4. Click "Play" to start the stream.

### Demo Video 
 [Click here to view](https://youtu.be/TqGxsCsfXsw)
   

## Troubleshooting
- **FFmpeg Not Found**: Ensure FFmpeg is present.
- **RTSP-SIMPLE-SERVER Not Found**: Ensure `mediamtx` is accessible.
- **VLC Player Not Launching**: Ensure VLC is installed correctly.

For any issues, refer to the respective documentation of the tools used (FFmpeg, RTSP-SIMPLE-SERVER, VLC Player or Comment this repo :) ).

Enjoy your streaming!
