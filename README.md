# **node-lpf2** - A Node.js module to interface with LEGO Power Functions 2.0 components.

### Installation

Node.js v8.0+ required.

```javascript
npm install node-lpf2 --save
```

node-lpf2 uses the Noble BLE library by Sandeep Mistry. On macOS everything should function out of the box. On Linux and Windows there are [certain dependencies which may need installed first](https://github.com/noble/noble#prerequisites).

Note: node-lpf2 has been tested on macOS 10.13 and Debian/Raspbian on the Raspberry Pi 3 Model B.

### Compatibility

While most LPF2 components and Hubs are compatible with each other, there are exceptions. There is limited backwards compatibility between newer components and the WeDo 2.0 Smart Hub. However WeDo 2.0 components are fully forwards compatible with newer Hubs.

| Name                            | Type          | WeDo 2.0 Smart Hub | Boost Move Hub | Powered Up Hub | Availability |
| ------------------------------- | ------------- | ------------------ | -------------- | -------------- | ------------ |
| WeDo 2.0 Tilt Sensor            | Sensor        |         Yes        |       Yes      |       Yes      | <a href="https://brickset.com/sets/45300-1/">45300</a> |
| WeDo 2.0 Motion Sensor          | Sensor        |         Yes        |       Yes      |       Yes      | <a href="https://brickset.com/sets/45300-1/">45300</a> |
| WeDo 2.0 Medium Motor           | Motor         |         Yes        |       Yes      |       Yes      | <a href="https://brickset.com/sets/45300-1/">45300</a><br /> <a href="https://brickset.com/sets/76112-1/">76112</a> |
| Boost Color and Distance Sensor | Sensor        |     *Partial*    |       Yes      |       Yes      | <a href="https://brickset.com/sets/17101-1/">17101</a> |
| Boost Interactive Motor  | Motor/Sensor  |     *Partial*    |       Yes      |       *Partial*      | <a href="https://brickset.com/sets/17101-1/">17101</a> |
| Powered Up Train Motor          | Motor         |         Yes        |       Yes      |       Yes      | <a href="https://brickset.com/sets/60197-1/">60197</a><br /><a href="https://brickset.com/sets/60198-1/">60198</a> |
| Powered Up LED Lights           | Light         |       Unknown      |     Unknown    |     Unknown    | <a href="https://brickset.com/sets/88005-1/">88005</a> |


### Known Issues and Limitations

* The Boost Color and Distance sensor only works in color mode with the WeDo 2.0 Smart Hub.

* When used with the WeDo 2.0 Smart Hub, the Boost Interactive Motor does not support rotating the motor by angle.

* When used with the Powered Up Hub, the Boost Interactive Motor does not support rotating the motor by angle. It also does not support rotation detection.

### Usage

```javascript
const LPF2 = require("node-lpf2").LPF2;
const lpf2 = new LPF2();
```

Examples are available in the "examples" directory.

### Credits

Thanks go to Jorge Pereira ([@JorgePe](https://github.com/JorgePe)), Sebastian Raff ([@hobbyquaker](https://github.com/hobbyquaker)), Valentin Heun ([@vheun](https://github.com/vheun)), and Johan Korten ([@jakorten](https://github.com/jakorten)) for their various works and assistance on figuring out the LEGO Boost, WeDo 2.0, and Powered Up protocols.

## Classes

<dl>
<dt><a href="#LPF2">LPF2</a> ⇐ <code>EventEmitter</code></dt>
<dd></dd>
<dt><a href="#WeDo2SmartHub">WeDo2SmartHub</a> ⇐ <code>Hub</code></dt>
<dd></dd>
<dt><a href="#BoostMoveHub">BoostMoveHub</a> ⇐ <code>LPF2Hub</code></dt>
<dd></dd>
<dt><a href="#PUPHub">PUPHub</a> ⇐ <code>LPF2Hub</code></dt>
<dd></dd>
<dt><a href="#PUPRemote">PUPRemote</a> ⇐ <code>LPF2Hub</code></dt>
<dd></dd>
</dl>

<a name="LPF2"></a>

## LPF2 ⇐ <code>EventEmitter</code>
**Kind**: global class  
**Extends**: <code>EventEmitter</code>  

* [LPF2](#LPF2) ⇐ <code>EventEmitter</code>
    * [.scan()](#LPF2+scan)
    * [.stop()](#LPF2+stop)
    * [.getConnectedHubByUUID(uuid)](#LPF2+getConnectedHubByUUID) ⇒ <code>Hub</code> \| <code>null</code>
    * [.getConnectedHubs()](#LPF2+getConnectedHubs) ⇒ <code>Array.&lt;Hub&gt;</code>
    * ["discover" (hub)](#LPF2+event_discover)

<a name="LPF2+scan"></a>

### lpF2.scan()
Begin scanning for LPF2 Hub devices.

**Kind**: instance method of [<code>LPF2</code>](#LPF2)  
<a name="LPF2+stop"></a>

### lpF2.stop()
Stop scanning for LPF2 Hub devices.

**Kind**: instance method of [<code>LPF2</code>](#LPF2)  
<a name="LPF2+getConnectedHubByUUID"></a>

### lpF2.getConnectedHubByUUID(uuid) ⇒ <code>Hub</code> \| <code>null</code>
Retrieve a LPF2 Hub by UUID.

**Kind**: instance method of [<code>LPF2</code>](#LPF2)  

| Param | Type |
| --- | --- |
| uuid | <code>string</code> | 

<a name="LPF2+getConnectedHubs"></a>

### lpF2.getConnectedHubs() ⇒ <code>Array.&lt;Hub&gt;</code>
Retrieve a list of LPF2 Hubs.

**Kind**: instance method of [<code>LPF2</code>](#LPF2)  
<a name="LPF2+event_discover"></a>

### "discover" (hub)
Emits when a LPF2 Hub device is found.

**Kind**: event emitted by [<code>LPF2</code>](#LPF2)  

| Param | Type |
| --- | --- |
| hub | [<code>WeDo2SmartHub</code>](#WeDo2SmartHub) \| <code>LPF2Hub</code> | 

<a name="WeDo2SmartHub"></a>

## WeDo2SmartHub ⇐ <code>Hub</code>
**Kind**: global class  
**Extends**: <code>Hub</code>  

* [WeDo2SmartHub](#WeDo2SmartHub) ⇐ <code>Hub</code>
    * [new WeDo2SmartHub()](#new_WeDo2SmartHub_new)
    * [.name](#Hub+name)
    * [.uuid](#Hub+uuid)
    * [.rssi](#Hub+rssi)
    * [.batteryLevel](#Hub+batteryLevel)
    * [.setLEDColor(color)](#WeDo2SmartHub+setLEDColor) ⇒ <code>Promise</code>
    * [.setLEDRGB(red, green, blue)](#WeDo2SmartHub+setLEDRGB) ⇒ <code>Promise</code>
    * [.setMotorSpeed(port, speed, [time])](#WeDo2SmartHub+setMotorSpeed) ⇒ <code>Promise</code>
    * [.playSound(frequency, time)](#WeDo2SmartHub+playSound) ⇒ <code>Promise</code>
    * [.connect()](#Hub+connect) ⇒ <code>Promise</code>
    * [.disconnect()](#Hub+disconnect) ⇒ <code>Promise</code>
    * [.subscribe(port, [mode])](#Hub+subscribe) ⇒ <code>Promise</code>
    * [.unsubscribe(port)](#Hub+unsubscribe) ⇒ <code>Promise</code>
    * [.sleep(delay)](#Hub+sleep) ⇒ <code>Promise</code>
    * [.wait(commands)](#Hub+wait) ⇒ <code>Promise</code>
    * ["button" (button, state)](#WeDo2SmartHub+event_button)
    * ["distance" (port, distance)](#WeDo2SmartHub+event_distance)
    * ["color" (port, color)](#WeDo2SmartHub+event_color)
    * ["tilt" (port, x, y)](#WeDo2SmartHub+event_tilt)
    * ["rotate" (port, rotation)](#WeDo2SmartHub+event_rotate)
    * ["attach" (port, type)](#Hub+event_attach)
    * ["detach" (port)](#Hub+event_detach)

<a name="new_WeDo2SmartHub_new"></a>

### new WeDo2SmartHub()
The WeDo2SmartHub is emitted if the discovered device is a WeDo 2.0 Smart Hub.

<a name="Hub+name"></a>

### weDo2SmartHub.name
**Kind**: instance property of [<code>WeDo2SmartHub</code>](#WeDo2SmartHub)  
**Read only**: true  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| name | <code>string</code> | Name of the hub |

<a name="Hub+uuid"></a>

### weDo2SmartHub.uuid
**Kind**: instance property of [<code>WeDo2SmartHub</code>](#WeDo2SmartHub)  
**Read only**: true  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| uuid | <code>string</code> | UUID of the hub |

<a name="Hub+rssi"></a>

### weDo2SmartHub.rssi
**Kind**: instance property of [<code>WeDo2SmartHub</code>](#WeDo2SmartHub)  
**Read only**: true  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| rssi | <code>number</code> | Signal strength of the hub |

<a name="Hub+batteryLevel"></a>

### weDo2SmartHub.batteryLevel
**Kind**: instance property of [<code>WeDo2SmartHub</code>](#WeDo2SmartHub)  
**Read only**: true  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| batteryLevel | <code>number</code> | Battery level of the hub (Percentage between 0-100) |

<a name="WeDo2SmartHub+setLEDColor"></a>

### weDo2SmartHub.setLEDColor(color) ⇒ <code>Promise</code>
Set the color of the LED on the Hub via a color value.

**Kind**: instance method of [<code>WeDo2SmartHub</code>](#WeDo2SmartHub)  
**Returns**: <code>Promise</code> - Resolved upon successful issuance of command.  

| Param | Type | Description |
| --- | --- | --- |
| color | <code>number</code> | A number representing one of the LED color consts. |

<a name="WeDo2SmartHub+setLEDRGB"></a>

### weDo2SmartHub.setLEDRGB(red, green, blue) ⇒ <code>Promise</code>
Set the color of the LED on the Hub via RGB values.

**Kind**: instance method of [<code>WeDo2SmartHub</code>](#WeDo2SmartHub)  
**Returns**: <code>Promise</code> - Resolved upon successful issuance of command.  

| Param | Type |
| --- | --- |
| red | <code>number</code> | 
| green | <code>number</code> | 
| blue | <code>number</code> | 

<a name="WeDo2SmartHub+setMotorSpeed"></a>

### weDo2SmartHub.setMotorSpeed(port, speed, [time]) ⇒ <code>Promise</code>
Set the motor speed on a given port.

**Kind**: instance method of [<code>WeDo2SmartHub</code>](#WeDo2SmartHub)  
**Returns**: <code>Promise</code> - Resolved upon successful completion of command. If time is specified, this is once the motor is finished.  

| Param | Type | Description |
| --- | --- | --- |
| port | <code>string</code> |  |
| speed | <code>number</code> | For forward, a value between 1 - 100 should be set. For reverse, a value between -1 to -100. Stop is 0. |
| [time] | <code>number</code> | How long to activate the motor for (in milliseconds). Leave empty to turn the motor on indefinitely. |

<a name="WeDo2SmartHub+playSound"></a>

### weDo2SmartHub.playSound(frequency, time) ⇒ <code>Promise</code>
Play a sound on the Hub's in-built buzzer

**Kind**: instance method of [<code>WeDo2SmartHub</code>](#WeDo2SmartHub)  
**Returns**: <code>Promise</code> - Resolved upon successful completion of command (ie. once the sound has finished playing).  

| Param | Type | Description |
| --- | --- | --- |
| frequency | <code>number</code> |  |
| time | <code>number</code> | How long the sound should play for (in milliseconds). |

<a name="Hub+connect"></a>

### weDo2SmartHub.connect() ⇒ <code>Promise</code>
Connect to the Hub.

**Kind**: instance method of [<code>WeDo2SmartHub</code>](#WeDo2SmartHub)  
**Overrides**: [<code>connect</code>](#Hub+connect)  
**Returns**: <code>Promise</code> - Resolved upon successful connect.  
<a name="Hub+disconnect"></a>

### weDo2SmartHub.disconnect() ⇒ <code>Promise</code>
Disconnect the Hub.

**Kind**: instance method of [<code>WeDo2SmartHub</code>](#WeDo2SmartHub)  
**Returns**: <code>Promise</code> - Resolved upon successful disconnect.  
<a name="Hub+subscribe"></a>

### weDo2SmartHub.subscribe(port, [mode]) ⇒ <code>Promise</code>
Subscribe to sensor notifications on a given port.

**Kind**: instance method of [<code>WeDo2SmartHub</code>](#WeDo2SmartHub)  
**Returns**: <code>Promise</code> - Resolved upon successful issuance of command.  

| Param | Type | Description |
| --- | --- | --- |
| port | <code>string</code> |  |
| [mode] | <code>number</code> | The sensor mode to activate. If no mode is provided, the default for that sensor will be chosen. |

<a name="Hub+unsubscribe"></a>

### weDo2SmartHub.unsubscribe(port) ⇒ <code>Promise</code>
Unsubscribe to sensor notifications on a given port.

**Kind**: instance method of [<code>WeDo2SmartHub</code>](#WeDo2SmartHub)  
**Returns**: <code>Promise</code> - Resolved upon successful issuance of command.  

| Param | Type |
| --- | --- |
| port | <code>string</code> | 

<a name="Hub+sleep"></a>

### weDo2SmartHub.sleep(delay) ⇒ <code>Promise</code>
Sleep a given amount of time.

This is a helper method to make it easier to add delays into a chain of commands.

**Kind**: instance method of [<code>WeDo2SmartHub</code>](#WeDo2SmartHub)  
**Returns**: <code>Promise</code> - Resolved after the delay is finished.  

| Param | Type | Description |
| --- | --- | --- |
| delay | <code>number</code> | How long to sleep (in milliseconds). |

<a name="Hub+wait"></a>

### weDo2SmartHub.wait(commands) ⇒ <code>Promise</code>
Wait until a given list of concurrently running commands are complete.

This is a helper method to make it easier to wait for concurrent commands to complete.

**Kind**: instance method of [<code>WeDo2SmartHub</code>](#WeDo2SmartHub)  
**Returns**: <code>Promise</code> - Resolved after the commands are finished.  

| Param | Type | Description |
| --- | --- | --- |
| commands | <code>Array.&lt;Promise.&lt;any&gt;&gt;</code> | Array of executing commands. |

<a name="WeDo2SmartHub+event_button"></a>

### "button" (button, state)
Emits when a button is pressed.

**Kind**: event emitted by [<code>WeDo2SmartHub</code>](#WeDo2SmartHub)  

| Param | Type | Description |
| --- | --- | --- |
| button | <code>string</code> |  |
| state | <code>number</code> | A number representing one of the button state consts. |

<a name="WeDo2SmartHub+event_distance"></a>

### "distance" (port, distance)
Emits when a distance sensor is activated.

**Kind**: event emitted by [<code>WeDo2SmartHub</code>](#WeDo2SmartHub)  

| Param | Type | Description |
| --- | --- | --- |
| port | <code>string</code> |  |
| distance | <code>number</code> | Distance, in millimeters. |

<a name="WeDo2SmartHub+event_color"></a>

### "color" (port, color)
Emits when a color sensor is activated.

**Kind**: event emitted by [<code>WeDo2SmartHub</code>](#WeDo2SmartHub)  

| Param | Type | Description |
| --- | --- | --- |
| port | <code>string</code> |  |
| color | <code>number</code> | A number representing one of the LED color consts. |

<a name="WeDo2SmartHub+event_tilt"></a>

### "tilt" (port, x, y)
Emits when a tilt sensor is activated.

**Kind**: event emitted by [<code>WeDo2SmartHub</code>](#WeDo2SmartHub)  

| Param | Type |
| --- | --- |
| port | <code>string</code> | 
| x | <code>number</code> | 
| y | <code>number</code> | 

<a name="WeDo2SmartHub+event_rotate"></a>

### "rotate" (port, rotation)
Emits when a rotation sensor is activated.

**Kind**: event emitted by [<code>WeDo2SmartHub</code>](#WeDo2SmartHub)  

| Param | Type |
| --- | --- |
| port | <code>string</code> | 
| rotation | <code>number</code> | 

<a name="Hub+event_attach"></a>

### "attach" (port, type)
Emits when a motor or sensor is attached to the Hub.

**Kind**: event emitted by [<code>WeDo2SmartHub</code>](#WeDo2SmartHub)  

| Param | Type | Description |
| --- | --- | --- |
| port | <code>string</code> |  |
| type | <code>number</code> | A number representing one of the peripheral consts. |

<a name="Hub+event_detach"></a>

### "detach" (port)
Emits when an attached motor or sensor is detached from the Hub.

**Kind**: event emitted by [<code>WeDo2SmartHub</code>](#WeDo2SmartHub)  

| Param | Type |
| --- | --- |
| port | <code>string</code> | 

<a name="BoostMoveHub"></a>

## BoostMoveHub ⇐ <code>LPF2Hub</code>
**Kind**: global class  
**Extends**: <code>LPF2Hub</code>, <code>Hub</code>  

* [BoostMoveHub](#BoostMoveHub) ⇐ <code>LPF2Hub</code>
    * [new BoostMoveHub()](#new_BoostMoveHub_new)
    * [.current](#LPF2Hub+current)
    * [.name](#Hub+name)
    * [.uuid](#Hub+uuid)
    * [.rssi](#Hub+rssi)
    * [.batteryLevel](#Hub+batteryLevel)
    * [.setLEDColor(color)](#BoostMoveHub+setLEDColor) ⇒ <code>Promise</code>
    * [.setMotorSpeed(port, speed, [time])](#BoostMoveHub+setMotorSpeed) ⇒ <code>Promise</code>
    * [.setMotorAngle(port, angle, [speed])](#BoostMoveHub+setMotorAngle) ⇒ <code>Promise</code>
    * [.connect()](#Hub+connect) ⇒ <code>Promise</code>
    * [.disconnect()](#Hub+disconnect) ⇒ <code>Promise</code>
    * [.subscribe(port, [mode])](#Hub+subscribe) ⇒ <code>Promise</code>
    * [.unsubscribe(port)](#Hub+unsubscribe) ⇒ <code>Promise</code>
    * [.sleep(delay)](#Hub+sleep) ⇒ <code>Promise</code>
    * [.wait(commands)](#Hub+wait) ⇒ <code>Promise</code>
    * ["button" (button, state)](#LPF2Hub+event_button)
    * ["distance" (port, distance)](#LPF2Hub+event_distance)
    * ["color" (port, color)](#LPF2Hub+event_color)
    * ["tilt" (port, x, y)](#LPF2Hub+event_tilt)
    * ["rotate" (port, rotation)](#LPF2Hub+event_rotate)
    * ["attach" (port, type)](#Hub+event_attach)
    * ["detach" (port)](#Hub+event_detach)

<a name="new_BoostMoveHub_new"></a>

### new BoostMoveHub()
The BoostMoveHub is emitted if the discovered device is a Boost Move Hub.

<a name="LPF2Hub+current"></a>

### boostMoveHub.current
**Kind**: instance property of [<code>BoostMoveHub</code>](#BoostMoveHub)  
**Read only**: true  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| current | <code>number</code> | Current usage of the hub (Amps) |

<a name="Hub+name"></a>

### boostMoveHub.name
**Kind**: instance property of [<code>BoostMoveHub</code>](#BoostMoveHub)  
**Read only**: true  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| name | <code>string</code> | Name of the hub |

<a name="Hub+uuid"></a>

### boostMoveHub.uuid
**Kind**: instance property of [<code>BoostMoveHub</code>](#BoostMoveHub)  
**Read only**: true  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| uuid | <code>string</code> | UUID of the hub |

<a name="Hub+rssi"></a>

### boostMoveHub.rssi
**Kind**: instance property of [<code>BoostMoveHub</code>](#BoostMoveHub)  
**Read only**: true  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| rssi | <code>number</code> | Signal strength of the hub |

<a name="Hub+batteryLevel"></a>

### boostMoveHub.batteryLevel
**Kind**: instance property of [<code>BoostMoveHub</code>](#BoostMoveHub)  
**Read only**: true  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| batteryLevel | <code>number</code> | Battery level of the hub (Percentage between 0-100) |

<a name="BoostMoveHub+setLEDColor"></a>

### boostMoveHub.setLEDColor(color) ⇒ <code>Promise</code>
Set the color of the LED on the Hub via a color value.

**Kind**: instance method of [<code>BoostMoveHub</code>](#BoostMoveHub)  
**Returns**: <code>Promise</code> - Resolved upon successful issuance of command.  

| Param | Type | Description |
| --- | --- | --- |
| color | <code>number</code> | A number representing one of the LED color consts. |

<a name="BoostMoveHub+setMotorSpeed"></a>

### boostMoveHub.setMotorSpeed(port, speed, [time]) ⇒ <code>Promise</code>
Set the motor speed on a given port.

**Kind**: instance method of [<code>BoostMoveHub</code>](#BoostMoveHub)  
**Returns**: <code>Promise</code> - Resolved upon successful completion of command. If time is specified, this is once the motor is finished.  

| Param | Type | Description |
| --- | --- | --- |
| port | <code>string</code> |  |
| speed | <code>number</code> | For forward, a value between 1 - 100 should be set. For reverse, a value between -1 to -100. Stop is 0. |
| [time] | <code>number</code> | How long to activate the motor for (in milliseconds). Leave empty to turn the motor on indefinitely. |

<a name="BoostMoveHub+setMotorAngle"></a>

### boostMoveHub.setMotorAngle(port, angle, [speed]) ⇒ <code>Promise</code>
Rotate a motor by a given angle.

**Kind**: instance method of [<code>BoostMoveHub</code>](#BoostMoveHub)  
**Returns**: <code>Promise</code> - Resolved upon successful completion of command (ie. once the motor is finished).  

| Param | Type | Default | Description |
| --- | --- | --- | --- |
| port | <code>string</code> |  |  |
| angle | <code>number</code> |  | How much the motor should be rotated (in degrees). |
| [speed] | <code>number</code> | <code>100</code> | How fast the motor should be rotated. |

<a name="Hub+connect"></a>

### boostMoveHub.connect() ⇒ <code>Promise</code>
Connect to the Hub.

**Kind**: instance method of [<code>BoostMoveHub</code>](#BoostMoveHub)  
**Overrides**: [<code>connect</code>](#Hub+connect)  
**Returns**: <code>Promise</code> - Resolved upon successful connect.  
<a name="Hub+disconnect"></a>

### boostMoveHub.disconnect() ⇒ <code>Promise</code>
Disconnect the Hub.

**Kind**: instance method of [<code>BoostMoveHub</code>](#BoostMoveHub)  
**Returns**: <code>Promise</code> - Resolved upon successful disconnect.  
<a name="Hub+subscribe"></a>

### boostMoveHub.subscribe(port, [mode]) ⇒ <code>Promise</code>
Subscribe to sensor notifications on a given port.

**Kind**: instance method of [<code>BoostMoveHub</code>](#BoostMoveHub)  
**Returns**: <code>Promise</code> - Resolved upon successful issuance of command.  

| Param | Type | Description |
| --- | --- | --- |
| port | <code>string</code> |  |
| [mode] | <code>number</code> | The sensor mode to activate. If no mode is provided, the default for that sensor will be chosen. |

<a name="Hub+unsubscribe"></a>

### boostMoveHub.unsubscribe(port) ⇒ <code>Promise</code>
Unsubscribe to sensor notifications on a given port.

**Kind**: instance method of [<code>BoostMoveHub</code>](#BoostMoveHub)  
**Returns**: <code>Promise</code> - Resolved upon successful issuance of command.  

| Param | Type |
| --- | --- |
| port | <code>string</code> | 

<a name="Hub+sleep"></a>

### boostMoveHub.sleep(delay) ⇒ <code>Promise</code>
Sleep a given amount of time.

This is a helper method to make it easier to add delays into a chain of commands.

**Kind**: instance method of [<code>BoostMoveHub</code>](#BoostMoveHub)  
**Returns**: <code>Promise</code> - Resolved after the delay is finished.  

| Param | Type | Description |
| --- | --- | --- |
| delay | <code>number</code> | How long to sleep (in milliseconds). |

<a name="Hub+wait"></a>

### boostMoveHub.wait(commands) ⇒ <code>Promise</code>
Wait until a given list of concurrently running commands are complete.

This is a helper method to make it easier to wait for concurrent commands to complete.

**Kind**: instance method of [<code>BoostMoveHub</code>](#BoostMoveHub)  
**Returns**: <code>Promise</code> - Resolved after the commands are finished.  

| Param | Type | Description |
| --- | --- | --- |
| commands | <code>Array.&lt;Promise.&lt;any&gt;&gt;</code> | Array of executing commands. |

<a name="LPF2Hub+event_button"></a>

### "button" (button, state)
Emits when a button is pressed.

**Kind**: event emitted by [<code>BoostMoveHub</code>](#BoostMoveHub)  

| Param | Type | Description |
| --- | --- | --- |
| button | <code>string</code> |  |
| state | <code>number</code> | A number representing one of the button state consts. |

<a name="LPF2Hub+event_distance"></a>

### "distance" (port, distance)
Emits when a distance sensor is activated.

**Kind**: event emitted by [<code>BoostMoveHub</code>](#BoostMoveHub)  

| Param | Type | Description |
| --- | --- | --- |
| port | <code>string</code> |  |
| distance | <code>number</code> | Distance, in millimeters. |

<a name="LPF2Hub+event_color"></a>

### "color" (port, color)
Emits when a color sensor is activated.

**Kind**: event emitted by [<code>BoostMoveHub</code>](#BoostMoveHub)  

| Param | Type | Description |
| --- | --- | --- |
| port | <code>string</code> |  |
| color | <code>number</code> | A number representing one of the LED color consts. |

<a name="LPF2Hub+event_tilt"></a>

### "tilt" (port, x, y)
Emits when a tilt sensor is activated.

**Kind**: event emitted by [<code>BoostMoveHub</code>](#BoostMoveHub)  

| Param | Type | Description |
| --- | --- | --- |
| port | <code>string</code> | If the event is fired from the Move Hub's in-built tilt sensor, the special port "TILT" is used. |
| x | <code>number</code> |  |
| y | <code>number</code> |  |

<a name="LPF2Hub+event_rotate"></a>

### "rotate" (port, rotation)
Emits when a rotation sensor is activated.

**Kind**: event emitted by [<code>BoostMoveHub</code>](#BoostMoveHub)  

| Param | Type |
| --- | --- |
| port | <code>string</code> | 
| rotation | <code>number</code> | 

<a name="Hub+event_attach"></a>

### "attach" (port, type)
Emits when a motor or sensor is attached to the Hub.

**Kind**: event emitted by [<code>BoostMoveHub</code>](#BoostMoveHub)  

| Param | Type | Description |
| --- | --- | --- |
| port | <code>string</code> |  |
| type | <code>number</code> | A number representing one of the peripheral consts. |

<a name="Hub+event_detach"></a>

### "detach" (port)
Emits when an attached motor or sensor is detached from the Hub.

**Kind**: event emitted by [<code>BoostMoveHub</code>](#BoostMoveHub)  

| Param | Type |
| --- | --- |
| port | <code>string</code> | 

<a name="PUPHub"></a>

## PUPHub ⇐ <code>LPF2Hub</code>
**Kind**: global class  
**Extends**: <code>LPF2Hub</code>, <code>Hub</code>  

* [PUPHub](#PUPHub) ⇐ <code>LPF2Hub</code>
    * [new PUPHub()](#new_PUPHub_new)
    * [.current](#LPF2Hub+current)
    * [.name](#Hub+name)
    * [.uuid](#Hub+uuid)
    * [.rssi](#Hub+rssi)
    * [.batteryLevel](#Hub+batteryLevel)
    * [.setLEDColor(color)](#PUPHub+setLEDColor) ⇒ <code>Promise</code>
    * [.setMotorSpeed(port, speed, [time])](#PUPHub+setMotorSpeed) ⇒ <code>Promise</code>
    * [.connect()](#Hub+connect) ⇒ <code>Promise</code>
    * [.disconnect()](#Hub+disconnect) ⇒ <code>Promise</code>
    * [.subscribe(port, [mode])](#Hub+subscribe) ⇒ <code>Promise</code>
    * [.unsubscribe(port)](#Hub+unsubscribe) ⇒ <code>Promise</code>
    * [.sleep(delay)](#Hub+sleep) ⇒ <code>Promise</code>
    * [.wait(commands)](#Hub+wait) ⇒ <code>Promise</code>
    * ["button" (button, state)](#LPF2Hub+event_button)
    * ["distance" (port, distance)](#LPF2Hub+event_distance)
    * ["color" (port, color)](#LPF2Hub+event_color)
    * ["tilt" (port, x, y)](#LPF2Hub+event_tilt)
    * ["attach" (port, type)](#Hub+event_attach)
    * ["detach" (port)](#Hub+event_detach)

<a name="new_PUPHub_new"></a>

### new PUPHub()
The PUPHub is emitted if the discovered device is a Powered Up Hub.

<a name="LPF2Hub+current"></a>

### pupHub.current
**Kind**: instance property of [<code>PUPHub</code>](#PUPHub)  
**Read only**: true  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| current | <code>number</code> | Current usage of the hub (Amps) |

<a name="Hub+name"></a>

### pupHub.name
**Kind**: instance property of [<code>PUPHub</code>](#PUPHub)  
**Read only**: true  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| name | <code>string</code> | Name of the hub |

<a name="Hub+uuid"></a>

### pupHub.uuid
**Kind**: instance property of [<code>PUPHub</code>](#PUPHub)  
**Read only**: true  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| uuid | <code>string</code> | UUID of the hub |

<a name="Hub+rssi"></a>

### pupHub.rssi
**Kind**: instance property of [<code>PUPHub</code>](#PUPHub)  
**Read only**: true  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| rssi | <code>number</code> | Signal strength of the hub |

<a name="Hub+batteryLevel"></a>

### pupHub.batteryLevel
**Kind**: instance property of [<code>PUPHub</code>](#PUPHub)  
**Read only**: true  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| batteryLevel | <code>number</code> | Battery level of the hub (Percentage between 0-100) |

<a name="PUPHub+setLEDColor"></a>

### pupHub.setLEDColor(color) ⇒ <code>Promise</code>
Set the color of the LED on the Hub via a color value.

**Kind**: instance method of [<code>PUPHub</code>](#PUPHub)  
**Returns**: <code>Promise</code> - Resolved upon successful issuance of command.  

| Param | Type | Description |
| --- | --- | --- |
| color | <code>number</code> | A number representing one of the LED color consts. |

<a name="PUPHub+setMotorSpeed"></a>

### pupHub.setMotorSpeed(port, speed, [time]) ⇒ <code>Promise</code>
Set the motor speed on a given port.

**Kind**: instance method of [<code>PUPHub</code>](#PUPHub)  
**Returns**: <code>Promise</code> - Resolved upon successful completion of command. If time is specified, this is once the motor is finished.  

| Param | Type | Description |
| --- | --- | --- |
| port | <code>string</code> |  |
| speed | <code>number</code> | For forward, a value between 1 - 100 should be set. For reverse, a value between -1 to -100. Stop is 0. |
| [time] | <code>number</code> | How long to activate the motor for (in milliseconds). Leave empty to turn the motor on indefinitely. |

<a name="Hub+connect"></a>

### pupHub.connect() ⇒ <code>Promise</code>
Connect to the Hub.

**Kind**: instance method of [<code>PUPHub</code>](#PUPHub)  
**Overrides**: [<code>connect</code>](#Hub+connect)  
**Returns**: <code>Promise</code> - Resolved upon successful connect.  
<a name="Hub+disconnect"></a>

### pupHub.disconnect() ⇒ <code>Promise</code>
Disconnect the Hub.

**Kind**: instance method of [<code>PUPHub</code>](#PUPHub)  
**Returns**: <code>Promise</code> - Resolved upon successful disconnect.  
<a name="Hub+subscribe"></a>

### pupHub.subscribe(port, [mode]) ⇒ <code>Promise</code>
Subscribe to sensor notifications on a given port.

**Kind**: instance method of [<code>PUPHub</code>](#PUPHub)  
**Returns**: <code>Promise</code> - Resolved upon successful issuance of command.  

| Param | Type | Description |
| --- | --- | --- |
| port | <code>string</code> |  |
| [mode] | <code>number</code> | The sensor mode to activate. If no mode is provided, the default for that sensor will be chosen. |

<a name="Hub+unsubscribe"></a>

### pupHub.unsubscribe(port) ⇒ <code>Promise</code>
Unsubscribe to sensor notifications on a given port.

**Kind**: instance method of [<code>PUPHub</code>](#PUPHub)  
**Returns**: <code>Promise</code> - Resolved upon successful issuance of command.  

| Param | Type |
| --- | --- |
| port | <code>string</code> | 

<a name="Hub+sleep"></a>

### pupHub.sleep(delay) ⇒ <code>Promise</code>
Sleep a given amount of time.

This is a helper method to make it easier to add delays into a chain of commands.

**Kind**: instance method of [<code>PUPHub</code>](#PUPHub)  
**Returns**: <code>Promise</code> - Resolved after the delay is finished.  

| Param | Type | Description |
| --- | --- | --- |
| delay | <code>number</code> | How long to sleep (in milliseconds). |

<a name="Hub+wait"></a>

### pupHub.wait(commands) ⇒ <code>Promise</code>
Wait until a given list of concurrently running commands are complete.

This is a helper method to make it easier to wait for concurrent commands to complete.

**Kind**: instance method of [<code>PUPHub</code>](#PUPHub)  
**Returns**: <code>Promise</code> - Resolved after the commands are finished.  

| Param | Type | Description |
| --- | --- | --- |
| commands | <code>Array.&lt;Promise.&lt;any&gt;&gt;</code> | Array of executing commands. |

<a name="LPF2Hub+event_button"></a>

### "button" (button, state)
Emits when a button is pressed.

**Kind**: event emitted by [<code>PUPHub</code>](#PUPHub)  

| Param | Type | Description |
| --- | --- | --- |
| button | <code>string</code> |  |
| state | <code>number</code> | A number representing one of the button state consts. |

<a name="LPF2Hub+event_distance"></a>

### "distance" (port, distance)
Emits when a distance sensor is activated.

**Kind**: event emitted by [<code>PUPHub</code>](#PUPHub)  

| Param | Type | Description |
| --- | --- | --- |
| port | <code>string</code> |  |
| distance | <code>number</code> | Distance, in millimeters. |

<a name="LPF2Hub+event_color"></a>

### "color" (port, color)
Emits when a color sensor is activated.

**Kind**: event emitted by [<code>PUPHub</code>](#PUPHub)  

| Param | Type | Description |
| --- | --- | --- |
| port | <code>string</code> |  |
| color | <code>number</code> | A number representing one of the LED color consts. |

<a name="LPF2Hub+event_tilt"></a>

### "tilt" (port, x, y)
Emits when a tilt sensor is activated.

**Kind**: event emitted by [<code>PUPHub</code>](#PUPHub)  

| Param | Type | Description |
| --- | --- | --- |
| port | <code>string</code> | If the event is fired from the Move Hub's in-built tilt sensor, the special port "TILT" is used. |
| x | <code>number</code> |  |
| y | <code>number</code> |  |

<a name="Hub+event_attach"></a>

### "attach" (port, type)
Emits when a motor or sensor is attached to the Hub.

**Kind**: event emitted by [<code>PUPHub</code>](#PUPHub)  

| Param | Type | Description |
| --- | --- | --- |
| port | <code>string</code> |  |
| type | <code>number</code> | A number representing one of the peripheral consts. |

<a name="Hub+event_detach"></a>

### "detach" (port)
Emits when an attached motor or sensor is detached from the Hub.

**Kind**: event emitted by [<code>PUPHub</code>](#PUPHub)  

| Param | Type |
| --- | --- |
| port | <code>string</code> | 

<a name="PUPRemote"></a>

## PUPRemote ⇐ <code>LPF2Hub</code>
**Kind**: global class  
**Extends**: <code>LPF2Hub</code>, <code>Hub</code>  

* [PUPRemote](#PUPRemote) ⇐ <code>LPF2Hub</code>
    * [new PUPRemote()](#new_PUPRemote_new)
    * [.current](#LPF2Hub+current)
    * [.name](#Hub+name)
    * [.uuid](#Hub+uuid)
    * [.rssi](#Hub+rssi)
    * [.batteryLevel](#Hub+batteryLevel)
    * [.setLEDColor(color)](#PUPRemote+setLEDColor) ⇒ <code>Promise</code>
    * [.connect()](#Hub+connect) ⇒ <code>Promise</code>
    * [.disconnect()](#Hub+disconnect) ⇒ <code>Promise</code>
    * [.subscribe(port, [mode])](#Hub+subscribe) ⇒ <code>Promise</code>
    * [.unsubscribe(port)](#Hub+unsubscribe) ⇒ <code>Promise</code>
    * [.sleep(delay)](#Hub+sleep) ⇒ <code>Promise</code>
    * [.wait(commands)](#Hub+wait) ⇒ <code>Promise</code>
    * ["button" (button, state)](#LPF2Hub+event_button)

<a name="new_PUPRemote_new"></a>

### new PUPRemote()
The PUPRemote is emitted if the discovered device is a Powered Up Remote.

<a name="LPF2Hub+current"></a>

### pupRemote.current
**Kind**: instance property of [<code>PUPRemote</code>](#PUPRemote)  
**Read only**: true  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| current | <code>number</code> | Current usage of the hub (Amps) |

<a name="Hub+name"></a>

### pupRemote.name
**Kind**: instance property of [<code>PUPRemote</code>](#PUPRemote)  
**Read only**: true  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| name | <code>string</code> | Name of the hub |

<a name="Hub+uuid"></a>

### pupRemote.uuid
**Kind**: instance property of [<code>PUPRemote</code>](#PUPRemote)  
**Read only**: true  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| uuid | <code>string</code> | UUID of the hub |

<a name="Hub+rssi"></a>

### pupRemote.rssi
**Kind**: instance property of [<code>PUPRemote</code>](#PUPRemote)  
**Read only**: true  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| rssi | <code>number</code> | Signal strength of the hub |

<a name="Hub+batteryLevel"></a>

### pupRemote.batteryLevel
**Kind**: instance property of [<code>PUPRemote</code>](#PUPRemote)  
**Read only**: true  
**Properties**

| Name | Type | Description |
| --- | --- | --- |
| batteryLevel | <code>number</code> | Battery level of the hub (Percentage between 0-100) |

<a name="PUPRemote+setLEDColor"></a>

### pupRemote.setLEDColor(color) ⇒ <code>Promise</code>
Set the color of the LED on the Remote via a color value.

**Kind**: instance method of [<code>PUPRemote</code>](#PUPRemote)  
**Returns**: <code>Promise</code> - Resolved upon successful issuance of command.  

| Param | Type | Description |
| --- | --- | --- |
| color | <code>number</code> | A number representing one of the LED color consts. |

<a name="Hub+connect"></a>

### pupRemote.connect() ⇒ <code>Promise</code>
Connect to the Hub.

**Kind**: instance method of [<code>PUPRemote</code>](#PUPRemote)  
**Overrides**: [<code>connect</code>](#Hub+connect)  
**Returns**: <code>Promise</code> - Resolved upon successful connect.  
<a name="Hub+disconnect"></a>

### pupRemote.disconnect() ⇒ <code>Promise</code>
Disconnect the Hub.

**Kind**: instance method of [<code>PUPRemote</code>](#PUPRemote)  
**Returns**: <code>Promise</code> - Resolved upon successful disconnect.  
<a name="Hub+subscribe"></a>

### pupRemote.subscribe(port, [mode]) ⇒ <code>Promise</code>
Subscribe to sensor notifications on a given port.

**Kind**: instance method of [<code>PUPRemote</code>](#PUPRemote)  
**Returns**: <code>Promise</code> - Resolved upon successful issuance of command.  

| Param | Type | Description |
| --- | --- | --- |
| port | <code>string</code> |  |
| [mode] | <code>number</code> | The sensor mode to activate. If no mode is provided, the default for that sensor will be chosen. |

<a name="Hub+unsubscribe"></a>

### pupRemote.unsubscribe(port) ⇒ <code>Promise</code>
Unsubscribe to sensor notifications on a given port.

**Kind**: instance method of [<code>PUPRemote</code>](#PUPRemote)  
**Returns**: <code>Promise</code> - Resolved upon successful issuance of command.  

| Param | Type |
| --- | --- |
| port | <code>string</code> | 

<a name="Hub+sleep"></a>

### pupRemote.sleep(delay) ⇒ <code>Promise</code>
Sleep a given amount of time.

This is a helper method to make it easier to add delays into a chain of commands.

**Kind**: instance method of [<code>PUPRemote</code>](#PUPRemote)  
**Returns**: <code>Promise</code> - Resolved after the delay is finished.  

| Param | Type | Description |
| --- | --- | --- |
| delay | <code>number</code> | How long to sleep (in milliseconds). |

<a name="Hub+wait"></a>

### pupRemote.wait(commands) ⇒ <code>Promise</code>
Wait until a given list of concurrently running commands are complete.

This is a helper method to make it easier to wait for concurrent commands to complete.

**Kind**: instance method of [<code>PUPRemote</code>](#PUPRemote)  
**Returns**: <code>Promise</code> - Resolved after the commands are finished.  

| Param | Type | Description |
| --- | --- | --- |
| commands | <code>Array.&lt;Promise.&lt;any&gt;&gt;</code> | Array of executing commands. |

<a name="LPF2Hub+event_button"></a>

### "button" (button, state)
Emits when a button is pressed.

**Kind**: event emitted by [<code>PUPRemote</code>](#PUPRemote)  

| Param | Type | Description |
| --- | --- | --- |
| button | <code>string</code> |  |
| state | <code>number</code> | A number representing one of the button state consts. |

