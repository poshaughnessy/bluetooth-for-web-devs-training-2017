title: Bluetooth for Web Developers
output: public/index.html
style: styles.css
controls: false

-- vertical-center

# Bluetooth for <br> Web Developers

### Special l33t training session <br> (awesome Samsung Internet peeps only)

<img src="images/sbrowser5.4.png" alt="Samsung Internet logo" class="w-100"/>

-- vertical-center

## The physical world and the digital world are merging...

-- vertical-center

### ...And your (shiny Samsung) smartphone is at the centre.

<img src="images/bluetooth-smartphone-centre.png" alt="Galaxy S8 and Bluetooth devices" style="max-width: 70%"/>

--

<p class="media-container fill-h">![Anki Overdrive](images/anki-overdrive.gif)</p>
<p class="caption">[Anki Overdrive](https://anki.com)</p>

--

<p class="media-container fill-w fill-h"><iframe src="https://www.youtube.com/embed/-Y77cUI_z30?t=4s" frameborder="0" allowfullscreen></iframe></p>
<p class="caption">[Physical Web lost dog demo](https://youtu.be/-Y77cUI_z30)</p>

--

<p class="media-container fill-w fill-h"><iframe width="560" height="315" src="https://www.youtube.com/embed/b0GDk-53fTo?t=4s" frameborder="0" allowfullscreen></iframe></p>
<p class="caption">[Physical Web restaurant buzzer](https://youtu.be/b0GDk-53fTo)</p>

--

<p class="media-container">![Pokemon Go Plus watch](images/pokemon-go-smartwatch.png)</p>
<p class="caption">[Pokemon Go Plus watch](http://www.pokemongo.com/en-us/pokemon-go-plus/)</p>

-- vertical-center

## Bluetooth Low Energy (BLE)

![BLE](images/ble-phone.png)

-- vertical-center

<img src="images/ble-logo.png" alt="BLE logo" class="w-200"/>

* Can constantly advertise presence
* Can last years on coin cell batteries
* ~100 kbps throughput (vs 24 Mbps!)

-- vertical-center code-bigger gatt

### GATT: Generic ATTribute

```
Profile
 |_ Service
 |  |_ Characteristic
 |  |_ Characteristic
 |  |_ Characteristic
 |_ Service
    |_ Characteristic
    |_ Characteristic
 ...
```

-- vertical-center

## Standard profiles

* Battery Service
* Blood Pressure
* Cycling Speed and Cadence
* Health Thermometer
* Location &amp; Navigation
* ...

<p class="caption">[www.bluetooth.com/specifications/gatt/services](https://www.bluetooth.com/specifications/gatt/services)</a>

-- vertical-center

## Or you can design your own

-- vertical-center

## Characteristics

<img src="images/ble-characteristic-props.png" alt="BLE characteristic properties" style="width: 800px"/>

-- vertical-center code-bigger

## Comms represented by Hex

```
02 02 01 06 02 0a 00 11 07 9e ca dc 24 0e e5 a9
```

<p class="caption">Example packet</p>

-- vertical-center

* Upto 20 bytes per packet
* `0xff === 255` (1 byte)
* `parseInt('ff', 16) === 255`

<p class="caption">[github.com/pebblecode/hex-utils](https://github.com/pebblecode/hex-utils)</p>

-- code-bigger vertical-center

``` javascript
// Length of 12 bytes
var buffer = new ArrayBuffer(12);

// ...Read data into the buffer...
var array = new Uint8Array(buffer);

// Gives e.g. 255 / 0xff:
var my8BitInt = array[0];
```

-- code-bigger vertical-center

``` javascript
var buffer = new ArrayBuffer(12);
var dataView = new DataView(buffer);

// Gives e.g. 255 / 0xff:
var my8BitInt = dataView.getUint8(0);
```

<p class="caption">[html5rocks.com/en/tutorials/webgl/typed_arrays/](http://www.html5rocks.com/en/tutorials/webgl/typed_arrays/)</p>

--

<h2 class="vertical-center">Here's one I helped make earlier...</h2> 

-- vertical-center

<p class="media-container fill-h">![ByBox](images/bybox-stockonnect.gif)</p>
<p class="caption">[ByBox Stockonnect app developed by pebble {code}](https://www.bybox.com/)</p>

-- vertical-center

<p class="media-container vertical-center fill-w">![BLE comms](images/bybox-comms.png)</p>

-- vertical-center previously-now

## *Previously...*
 
### Web devs had to use Node, Cordova, React Native etc.

<img src="images/crowd-boo.jpg" alt="Angry crowd" style="width: 70%;"/>

-- vertical-center

## *Now...*

## Web Bluetooth! 🎉

<img src="images/ble-logo.png" alt="BLE logo" class="w-300"/>

-- vertical-center

* Bluetooth Low Energy only
* "Central" only (i.e. controller, not "peripheral")

-- vertical-center

![caniuse.com](images/web-bluetooth-caniuse.png)
<p class="caption">[caniuse.com](https://caniuse.com)</p>

-- vertical-center

## And this awesome browser called Samsung Internet has it behind a flag!

-- vertical-center

# Part 1: Cutting our (Blue)teeth

-- vertical-center code-bigger

```javascript
let options = {filters: [{
                 services: ['battery_service'] }] };
                 
navigator.bluetooth.requestDevice(options)
```

<p class="caption">[Drone example here](https://github.com/poshaughnessy/web-bluetooth-parrot-drone/blob/master/js/drone.js#L110)</p>

-- vertical-center two-images

<div>
  ![Bluetooth pairing prompt 1](images/pairing-prompt1.png) ![Bluetooth pairing prompt 2](images/pairing-prompt2.png)
</div>

-- vertical-center

```javascript
  ...
  
  .then(device => device.connectGATT())
    
  .then(server =>
    server.getPrimaryService('battery_service'))
    
  .then(service =>
    service.getCharacteristic('battery_level'))
    
  .then(characteristic => {
    // Read battery level
    return characteristic.readValue();
  })
```

-- vertical-center code-bigger

```javascript
  .then(value => {
    let bytes = new Uint8Array(value.buffer);
    console.log(`Battery level: ${bytes[0]}`);
  });
```

<div class="caption">[bit.ly/chrome-bluetooth-guide](http://bit.ly/chrome-bluetooth-guide)</div>

-- vertical-center

<h2 class="vertical-center">Demo time</h2>

-- vertical-center

<p class="media-container">![web-bluetooth-parrot-drone](images/web-drone-screenshot.png)</p>
<p class="caption">[bit.ly/web-bluetooth-drone](http://bit.ly/web-bluetooth-drone)</p>

-- vertical-center

<div class="vertical-center">
    <h2>In case of demo fail</h2>
    [bit.ly/web-bluetooth-drone-video](https://youtu.be/-FO9thLaiug)
</div>

-- vertical-center

## Code time

-- vertical-center

## Control your slides

<video controls style="height: 75%">
  <source src="videos/wb-slides.mp4"/>
</video>

-- vertical-center

## Control your Puck.js

<video controls style="width: 75%">
  <source src="videos/puckjs-web-bluetooth.mp4"/>
</video>

-- vertical-center

# Part 2: Sniffin' n' debuggin'

-- vertical-center

> “This is a short list of issues you will encounter if you try to use native Android BLE...”

-- vertical-center

<p class="media-container fill-h">![Sweetblue](images/sweetblue.png)</p>
<p class="caption">[bit.ly/sweetblue-android](http://bit.ly/sweetblue-android)</p>

-- vertical-center

<div class="vertical-center">
  <ul>
      <li>Start with a small list of supported devices</li>
      <li>Allow lots of time for device testing</li>
  </ul>
</div>  

-- vertical-center

<img alt="Hackaball" src="images/hackaball.jpg" style="max-width:85%"/>
<p class="caption">[hackaball.com](http://www.hackaball.com/)</p>

-- vertical-center

<img alt="CySmart" src="images/cysmart.png" style="max-height:calc(100vh - 4em)"/>
<p class="caption">[CySmart with CySmart BLE dongle (Windows)](http://www.cypress.com/documentation/software-and-drivers/cysmart-bluetooth-le-test-and-debug-tool)</p>

-- vertical-center

<img alt="Bluetooth apps" src="images/bluetooth-debugging-apps.png" style="max-height:calc(100vh - 4em)"/>
<p class="caption">Bluetooth debugging apps: [LightBlue](https://itunes.apple.com/us/app/lightblue-explorer-bluetooth/id557428110?mt=8), [Bluefruit](https://play.google.com/store/apps/details?id=com.adafruit.bluefruit.le.connect&hl=en), [CySmart](https://play.google.com/store/apps/details?id=com.cypress.cysmart&hl=en)</p>

-- vertical-center

<img alt="Bluefruit app (Android)" src="images/bluefruit-info.png" style="max-height:calc(100vh - 4em)"/>
<p class="caption">Bluefruit (Android)</p>

-- vertical-center

<img alt="Bluez" src="images/bluez-hcitool-gatttool-1.png" width="90%"/>
<p class="caption">[BlueZ](http://www.bluez.org/about/)</p>

-- vertical-center

<img alt="Bluez" src="images/bluez-hcitool-gatttool-zoom1.png" width="90%"/>
<p class="caption">[BlueZ](http://www.bluez.org/about/)</p>

-- vertical-center

<img alt="Bluez" src="images/bluez-hcitool-gatttool-zoom2.png" width="90%"/>
<p class="caption">[BlueZ](http://www.bluez.org/about/)</p>

-- vertical-center

<img alt="Bluez" src="images/bluez-hcitool-gatttool-zoom3.png" width="90%"/>
<p class="caption">[BlueZ](http://www.bluez.org/about/)</p>

-- vertical-center

<img alt="Wireshark" src="images/adafruit-ble-sniff.jpg" style="max-height:calc(100vh - 4em)"/>
<p class="caption">[Wireshark](https://www.wireshark.org/) with [Bluefruit BLE sniffer](https://shop.pimoroni.com/products/adafruit-bluefruit-le-sniffer-ble-4-0-nrf51822-v1-0)</p>

-- vertical-center

<img alt="ble-sniffer-osx" src="images/ble-sniffer-osx.png" style="max-height:calc(100vh - 4em)"/>
<p class="caption">[ble-sniffer-osx](https://sourceforge.net/projects/nrfblesnifferosx/)</p>

-- vertical-center

<img alt="Hackaball advertising" src="images/advertising.png" style="max-height:calc(100vh - 4em)"/>

-- vertical-center

<img alt="Hackaball advertising" src="images/advertising-zoom.png" style="max-height:calc(100vh - 4em)"/>

-- vertical-center

<img alt="Hackaball scan response" src="images/scan-response.png" style="max-height:calc(100vh - 4em)"/>

-- vertical-center

<img alt="Hackaball scan response" src="images/scan-response-zoom.png" style="max-height:calc(100vh - 4em)"/>

-- vertical-center

<img alt="A Hackaball command" src="images/hackaball-sniffing.png" style="max-height:calc(100vh - 4em)"/>

-- vertical-center

<img alt="A Hackaball command" src="images/hackaball-sniffing-zoom.png" style="max-height:calc(100vh - 4em)"/>

-- vertical-center

<img alt="Bluez" src="images/bluez-hcitool-gatttool-zoom4.png" width="90%"/>
<p class="caption">[BlueZ](http://www.bluez.org/about/)</p>

-- vertical-center

<img alt="Bluez" src="images/bluez-hcitool-gatttool-zoom5.png" width="90%"/>
<p class="caption">[BlueZ](http://www.bluez.org/about/)</p>

-- vertical-center

![Tools deprecated](images/tools-deprecated.png)

-- vertical-center

## Things we could try next?

* BB8!
* Our Nordic device
* Our freescale device
* `$yourFavouriteBLEDevice`

-- vertical-center

# The physical world is at our command! 🤖

