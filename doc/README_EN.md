# homebridge-mi-acpartner
[![npm version](https://badge.fury.io/js/homebridge-mi-acpartner.svg)](https://badge.fury.io/js/homebridge-mi-acpartner)

XiaoMi AC Partner plugins for HomeBridge.

Thanks for [takatost's project](https://github.com/takatost/homebridge-mi-ac-partner),  [miio](https://github.com/aholstenson/miio), [YinHangCode's project](https://github.com/YinHangCode/homebridge-mi-aqara) and all other developer and testers.

**Note: I don't have much time to get AC command for presets. You can commit your customize setting to [issues](https://github.com/LASER-Yi/homebridge-mi-acpartner/issues) or ly0007@yeah.net. I will write a Commit Format later.**

**WARN: This plugin will not support Miio Auto Discover feature after 0.2.2. Please add your ac partner's ip address to config.json as quick as possible, Thanks.**

### Feature

* Switch on / off.

* Control modes:

  - Use AC signal or IR signal to control your AC.
  - Change temperature between 17 - 30(default).
  - HEAT mode, COOL mode, AUTO mode support.
  - Wind Force, Wind Sweep control support.(Basic on iOS 11, Coming sooooon)
  - Customize IR Signal Support.(Coming sooooooooon)

* Customize your AC's Signal

* Sync AC State bewteen AC Partner and Home App.~~(Coming soon)~~

* Auto get AC signal.(may not work for all AC)

* Temperature Sensor Support.~~(Coming soon)~~


### Installation

1. Install [Homebridge](https://github.com/nfarina/homebridge)

2. Install required packages(include miio).

```
npm install -g homebridge-mi-acpartner miio
```

3. Add plugin configuration to your config.json file, please see ``Config`` and ``Config Example`` for more detail.

4. Start Homebridge.

### Config

* Necessary

    * "accessory": "XiaoMiAcPartner"

    * "token": "Your AC Partner token"

      Follow this [Document](https://github.com/aholstenson/miio/blob/master/docs/management.md#getting-the-token-of-a-device) get your AC Partner's token.

            If you are using Android device, you can get token by using MIJIA app.

    * "name": "Name show in Home App"

    * "ip": "your_ac_partner_ip_address"

* Optional

    * "customize":

        Use this [method](https://github.com/aholstenson/miio/blob/master/docs/protocol.md#) to get your AC's command.

        Please see Config Example for more detail.

        Not every AC need "on" signal, please check your AC's command for more infomation.

        If "auto" signal undefined, plugin will send signal(cool/heat) basic on current temperature.

        You can add "type": "IR" to send customize IR command.

    * "maxTemp": "Set max temperature"

    * "minTemp": "Set min temperature"

    * "sensorSid": "Your Temperature Sensor Series ID, that sensor must connected with AC Partner"

### Config Example

Basic setting

```
"accessories": [
        {
            "accessory": "XiaoMiAcPartner",
            "token": "token-as-hex",
            "name": "AcPartner",
            "ip": "your_ac_partner_ip_address"
        }
    ]
```

Using outer Temperature Sensor

```
"accessories": [
        {
            "accessory": "XiaoMiAcPartner",
            "token": "token-as-hex",
            "name": "AcPartner_1",
            "ip": "192.168.1.1",
            "sensorSid": "lumi.158d000156e667"
        }
]
```

Using customize AC command.

```
"accessories": [
        {
            "accessory": "XiaoMiAcPartner",
            "token": "token-as-hex",
            "name": "AcPartner",
            "minTemp": "18",
            "ip": "your_ac_partner_ip_address",
            "customize": {
                "off": "AC off signal(Necessary)",
                "on": "Some_AC_need_this(Optional)",
                "auto": "AC auto mode signal(Optional)",
                "heat":{
                    "30": "(Optional)",
                    "29": "",
                    "17": ""
                },
                "cool":{
                    "30": "Necessary",
                    "29": "",
                    "17": ""
                }
            }
        }
    ]
```

Using customize IR command.

```
"accessories": [
        {
            "accessory": "XiaoMiAcPartner",
            "token": "token-as-hex",
            "name": "AcPartner",
            "minTemp": "18",
            "ip": "your_ac_partner_ip_address",
            "customize": {
                "type": "IR",
                "off": "AC off signal(Necessary)",
                "on": "Some_AC_need_this(Optional)",
                "auto": "AC auto mode signal(Optional)",
                "heat":{
                    "30": "(Optional)",
                    "29": "",
                    "17": ""
                },
                "cool":{
                    "30": "Necessary",
                    "29": "",
                    "17": ""
                }
            }
        }
    ]
```

### Changelog

0.2.6

Remove Gateway temperature sensor support. Add automatic preset detection.

0.2.5

Outer temperature sensor support. 

0.2.3

Gree 2 preset support, customize IR control support.

0.2.0

Sync State between hk and AC Partner. maxTemp & minTemp Support. Add gree 2 preset for testing.

0.1.5

Presets reconstruction.

0.0.9

Auto mode support, "on" signal support, code reconstruction, presets reconstruction.

0.0.1

ADD Basic File.