# home_automation

Is comfort our end goal in life ?

## The big TV screen

I don't watch "television" anymore. But I have a big flat Panasonic TV screen attached to my Thinkpad notebook and I watch much too much Youtube videos.  
The Thinkpad and the "big monitor" are switched on all day. What can I do? I am crazy about computers and stuff, and I hoard them.  
![TV setup](https://github.com/LucianoBestia/arduino_turns_on_laptop/raw/main/images/TV_setup.jpg)

## turn them on

First I want to turn all of the components with one switch: TV, active speakers, mixing console and the Thinkpad. I put all of them on one power outlet which I then control with a 433 MHz remote control. But there was  problem (like always): the Thinkpad cannot be turned on like this. So I made a simple Arduino project for that. All the info is here:  
<https://github.com/LucianoBestia/arduino_turns_on_laptop>  
It is not great, but it is good enough. It works.  

## I need a clock

I don't have any clock around my flat, but I need one. The TV screen is always on, why not use it to show a big black clock. And for fun let make it a rust project as a tutorial for new programmers.  
<https://github.com/LucianoBestia/rust_wasm_pwa_minimal_clock>  
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

## clock in millidays

My hobby is to think about time and date formats. There would be no fun in it, if these formats were "perfect", but they are terribly confusing and outdated. So I am proposing a reform to time/date to make it look modern, more `metric`. Sure we have to adapt it to the rotation of our planet and to human rhythms and traditions. It will always be just a compromise. It is impossible to make it "perfect". But we have to somehow change this archaic ways we use today to something better.  
<https://github.com/LucianoBestia/new_date_time_units_and_formats>  
<https://github.com/LucianoBestia/veeks_millis_clock>  
<https://github.com/LucianoBestia/veeks_millis>  

The Task Scheduler exported xml (only important parts):  
<?xml version="1.0" encoding="UTF-16"?>
<Task version="1.2" xmlns="http://schemas.microsoft.com/windows/2004/02/mit/task">
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

## all together






