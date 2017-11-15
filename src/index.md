title: Bluetooth for Web Developers
output: public/index.html
style: styles.css
controls: false

-- vertical-center

# Bluetooth for <br> Web Developers

### Special l33t training session <br> (awesome Samsung Internet peeps only)

<img src="images/sbrowser5.4.png" alt="Samsung Internet logo" class="w-100"/>

--

<h2 class="vertical-center">The physical world and the digital world are merging...</h2>

--

<h2 class="vertical-center">...And your (shiny Samsung) smartphone is at the centre.</h2>

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

## Bluetooth Low Energy

![BLE](images/ble-phone.png)

-- vertical-center

<img src="images/ble-logo.png" alt="BLE logo" class="w-200"/>

* Can constantly advertise presence
* Can last years on coin cell batteries
* ~100 kbps throughput (vs 24 Mbps!)

-- vertical-center

<p class="media-container fill-h">![BLE profiles etc.](images/bluetooth-profiles-etc.png)</p>

-- vertical-center

<p class="media-container vertical-center fill-w">![BLE characteristic properties](images/ble-characteristic-props.png)</p>
<p class="caption">Generic ATTribute profile (GATT)</p>

-- vertical-center

## Comms based on Hex

* `0xff === 255`
* `parseInt('ff', 16) === 255`
* Uint8Array useful for data buffers
* [github.com/pebblecode/hex-utils](https://github.com/pebblecode/hex-utils)

--

<h2 class="vertical-center">Here's one I helped make earlier...</h2> 

-- vertical-center

<p class="media-container fill-h">![ByBox](images/bybox-stockonnect.gif)</p>
<p class="caption">[ByBox Stockonnect app developed by pebble {code}](https://www.bybox.com/)</p>

-- vertical-center

<p class="media-container vertical-center fill-w">![BLE comms](images/bybox-comms.png)</p>

-- vertical-center previously-now

## *Previously...*
 
### Web developers had to use Cordova, React Native etc.

<img src="images/crowd-boo.jpg" alt="Angry crowd" style="width: 70%;"/>

-- vertical-center

## *Now...*

## Web Bluetooth! 🎉

<img src="images/ble-logo.png" alt="BLE logo" class="w-300"/>

-- vertical-center

![caniuse.com](images/web-bluetooth-caniuse.png)
<p class="caption">caniuse.com</p>

-- vertical-center

## And this awesome browser called Samsung Internet has it behind a flag!

-- vertical-center

## Part 1: Cutting our (Blue)teeth

-- vertical-center code-bigger

```javascript
let options = {filters: [{
                 services: ['battery_service'] }] };
                 
navigator.bluetooth.requestDevice(options)
```

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

## Part 2: Sniff It!

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

<p class="media-container">![CySmart](images/cysmart.png)</p>
<p class="caption">CySmart with CySmart BLE dongle (Windows)</p>

-- vertical-center

<p class="media-container">![Wireshark](images/adafruit-ble-sniff.jpg)</p>
<p class="caption">Wireshark with Bluefruit BLE sniffer</p>


