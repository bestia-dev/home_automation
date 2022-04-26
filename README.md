# home_automation

**Is comfort our end goal in life ?**  
***version: 1.0  date: 2021-02-23 author: [bestia.dev](https://bestia.dev) repository: [GitHub](https://github.com/bestia-dev/home_automation)***  

[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Fbestia-dev%2Fhome_automation&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=false)](https://hits.seeyoufarm.com)

Hashtags: #tutorial

## The big TV screen

I don't watch "television" anymore. But I have a big flat Panasonic TV screen attached to my Thinkpad notebook and I watch much too much Youtube videos.  
The Thinkpad and the "big monitor" are switched on all day. What can I do? I am crazy about computers and stuff, and I hoard them.  
![TV setup](https://github.com/bestia-dev/home_automation/raw/main/images/TV_setup.jpg)

## turn them on

First I want to turn all of the components with one switch: TV, active speakers, mixing console and the Thinkpad. I put all of them on one power outlet which I then control with a 433 MHz remote control. But there was  problem (like always): the Thinkpad cannot be turned on like this. So I made a simple Arduino project for that. All the info is here:  
<https://github.com/bestia-dev/arduino_turns_on_laptop>  
It is not great, but it is good enough. It works.  

## I need a clock

I don't have any clock around my flat, but I need one. The TV screen is always on, why not use it to show a big black clock. And for fun let make it a rust project as a tutorial for new programmers.  
<https://github.com/bestia-dev/rust_wasm_pwa_minimal_clock>  
It is even more fun if it speaks the time every full hour.  
I want it to start as soon as I turn on the computer. I used the Task Scheduler with this important parts:

```xml
<Task version="1.2" xmlns="http://schemas.microsoft.com/windows/2004/02/mit/task">
  <RegistrationInfo>
    <URI>\clock on startup</URI>
  </RegistrationInfo>
  <Triggers>
    <LogonTrigger>
      <Enabled>true</Enabled>
    </LogonTrigger>
  </Triggers>
  <Actions Context="Author">
    <Exec>
      <Command>"C:\Program Files (x86)\Google\Chrome\Application\chrome_proxy.exe"</Command>
      <Arguments>--profile-directory=Default --app-id=ccfjhdebcopgibimdhklogjkbeoigcme</Arguments>
    </Exec>
  </Actions>
</Task>
```

It was a pain to discover how to start a PWA in Win10. Finally I found it in the app icon properties. Wow! So strange and unusual.  
The browser opens in the same size and position where it was used last. That is convenient, but prone to mistakes in the future if somebody inadvertently moves the window and then closes it. Later I discovered how to give the size and position as arguments to start the browser. I used it for my other PWA.  

## I want a radio

I don't have a classic radio, but there are many radio stations on the internet. I like one in particular "radio SI". They have made it a PWA and I like that.  
I'd like to start it as soon as I start my Thinkpad+TV combo. I used the Task Scheduler (simplified exported xml):  

```xml
<Task version="1.2" xmlns="http://schemas.microsoft.com/windows/2004/02/mit/task">
  <RegistrationInfo>
    <URI>\radio SI on startup</URI>
  </RegistrationInfo>
  <Triggers>
    <LogonTrigger>
      <Delay>PT5S</Delay>
    </LogonTrigger>
  </Triggers>
  <Actions Context="Author">
    <Exec>
      <Command>"C:\Program Files (x86)\Microsoft\Edge\Application\msedge_proxy.exe"</Command>
      <Arguments>--profile-directory=Default --app-id=ndhchppnnecjjogmjmfnajggokoloahe</Arguments>
    </Exec>
  </Actions>
</Task>
```

## Calendar

The Google calendar is very convenient to have it in sight all the time. Let start it on Logon with a particular profile and defined size and position. Here is the important parts of the exported xml from Task Scheduler:  
```xml
<?xml version="1.0" encoding="UTF-16"?>
<Task version="1.2" xmlns="http://schemas.microsoft.com/windows/2004/02/mit/task">
  <RegistrationInfo>
    <URI>\calendar</URI>
  </RegistrationInfo>
  <Triggers>
    <LogonTrigger>
      <Enabled>true</Enabled>
    </LogonTrigger>
  </Triggers>
  <Actions Context="Author">
    <Exec>
      <Command>"C:\Program Files (x86)\Google\Chrome\Application\chrome.exe"</Command>
      <Arguments>--new-window "https://calendar.google.com/calendar/u/0/r/month" --window-size="800,450" --window-position="480,270" --user-data-dir="C:\Users\happy guest\Documents\ChromeProfiles\Profile1"</Arguments>
    </Exec>
  </Actions>
</Task>
```

This is a combination of 4 calendars:  

1. my personal calendar
2. my wife's personal calendar
3. our common calendar for events we do together
4. my mother's personal calendar

Every calendar event has its own color to easy distinguish.
Just like everything: it is not perfect, but it works good enough.  

## clock in millidays

My hobby is to think about time and date formats. There would be no fun in it, if these formats were "perfect", but they are terribly confusing and outdated. So I am proposing a reform to time/date to make it look modern, more `metric`. Sure we have to adapt it to the rotation of our planet and to human rhythms and traditions. It will always be just a compromise. It is impossible to make it "perfect". But we have to somehow change this archaic ways we use today to something better.  
<https://github.com/bestia-dev/new_date_time_units_and_formats>  
<https://github.com/bestia-dev/veeks_millis_clock>  
<https://github.com/bestia-dev/veeks_millis>  

The Task Scheduler exported xml (only important parts):  

```xml
  <RegistrationInfo>
    <URI>\millisclock on startup</URI>
  </RegistrationInfo>
  <Triggers>
    <LogonTrigger>
      <Enabled>true</Enabled>
      <Delay>PT15S</Delay>
    </LogonTrigger>
  </Triggers>
  <Actions Context="Author">
    <Exec>
      <Command>"C:\Program Files (x86)\Microsoft\Edge\Application\msedge_proxy.exe"</Command>
      <Arguments>--profile-directory=Default --app-id=njeblkadplcimcagioidhnldecembkoa</Arguments>
    </Exec>
  </Actions>
</Task>
```

## all together

On modern 16:9 screens it is clever to put the task bar on the left edge and fix it. Today monitors are far too wide and vertically extremely thin. Every vertical pixel is like gold. Unfortunately windows design was created in times when the monitors were much taller. So there is a lot of elements that consume vertical space instead of horizontal space. Unfortunate!  

![screenshot](https://github.com/bestia-dev/home_automation/raw/main/images/screenshot_1.png)

I like to have a button for fast shutdown on the Taskbar. The Win10 original way to do it is crazy long: click Start - Power - Shutdown.  Maybe there is also a keyboard shortcut, but good luck to teach that to my wife.  
I created a new icon with properties:  
`Target: C:\Windows\System32\shutdown.exe /s /t 00`  
And changed the Icon file: 
<https://github.com/bestia-dev/home_automation/raw/main/images/shutdown.ico>  

I love the file manager TotalCommander from Ghisler:  
<https://github.com/bestia-dev/total_commander_best_file_manager>  
I cannot live without it.  

## other tiny things

Sometimes I would like to listen to music from my smartphone. I don't have a good bluetooth speaker, but I have a Thinkpad attached to big speakers. I found this app `Bluetooth Audio Receiver` from Mark Smirnov and I am happy with it:  
<https://www.microsoft.com/en-us/p/bluetooth-audio-receiver/9n9wclwdqs5j?activetab=pivot:overviewtab>

I use some remote controlled 433 Mhz switches for power outlets. They come with their own remote controls and that is fine. But sometimes I would like to control them from my computer. So I used a Raspberry Pi as a local web server on my WiFi network. Attached to it is an arduino with a 433Mhz transmitter. With a little bit of software it works as a PMHAS - "poor man home automation system" :-). My friend Pingec helped me with Arduino:  
<https://github.com/pingec/SerialRcSwitch>  

## conclusion

So I have my radio, calendar and clock, all in the digital world. Not bad. Maybe overkill, but a lot of fun.  
