# Node-RED dimming flow

This code is complementary to [this blog post](https://thepinkowl.org/how-to-best-use-ikea-tradfri-wireless-dimmer-with-home-assistant/).

## How to use it this code

1. Copy this block
2. Open your Node-RED instance (and log in)
3. Click on the burger menu on the top right corner
4. Click "import"
5. Paste what you copied on the clipboard tab
6. Click the "import" button
7. Configure the set of nodes to use the values that suit your setup.

```json
[
    {
        "id": "3330c43e.a9732c",
        "type": "switch",
        "z": "715c9f22.80b84",
        "name": "ON / OFF",
        "property": "payload.event.command",
        "propertyType": "msg",
        "rules": [
            {
                "t": "eq",
                "v": "on",
                "vt": "str"
            },
            {
                "t": "eq",
                "v": "off",
                "vt": "str"
            }
        ],
        "checkall": "true",
        "repair": false,
        "outputs": 2,
        "x": 380,
        "y": 180,
        "wires": [
            [
                "be9be0f4.3655a"
            ],
            [
                "fa19f399.14346"
            ]
        ]
    },
    {
        "id": "c3f309d.9a563f8",
        "type": "api-call-service",
        "z": "715c9f22.80b84",
        "name": "IF ALREADY ON ==> 100%",
        "server": "e7bd0652.9f3af8",
        "version": 1,
        "debugenabled": false,
        "service_domain": "light",
        "service": "turn_on",
        "entityId": "light.sofa_light",
        "data": "{\"brightness_pct\": 100}",
        "dataType": "json",
        "mergecontext": "",
        "output_location": "",
        "output_location_type": "none",
        "mustacheAltTags": false,
        "x": 960,
        "y": 120,
        "wires": [
            []
        ]
    },
    {
        "id": "b6251f12.9fc34",
        "type": "api-call-service",
        "z": "715c9f22.80b84",
        "name": "Turn Sofa Light OFF",
        "server": "e7bd0652.9f3af8",
        "version": 1,
        "debugenabled": false,
        "service_domain": "light",
        "service": "turn_off",
        "entityId": "light.sofa_light",
        "data": "",
        "dataType": "json",
        "mergecontext": "",
        "output_location": "",
        "output_location_type": "none",
        "mustacheAltTags": false,
        "x": 940,
        "y": 200,
        "wires": [
            []
        ]
    },
    {
        "id": "92a54451.ebc8a8",
        "type": "inject",
        "z": "715c9f22.80b84",
        "name": "",
        "props": [],
        "repeat": "0.5",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "",
        "x": 150,
        "y": 260,
        "wires": [
            [
                "62f82a8d.8dcf24"
            ]
        ]
    },
    {
        "id": "62f82a8d.8dcf24",
        "type": "switch",
        "z": "715c9f22.80b84",
        "name": "Should Sofa Light dim?",
        "property": "sofa_light_dim",
        "propertyType": "flow",
        "rules": [
            {
                "t": "eq",
                "v": "move_with_on_off",
                "vt": "str"
            },
            {
                "t": "eq",
                "v": "move",
                "vt": "str"
            }
        ],
        "checkall": "true",
        "repair": false,
        "outputs": 2,
        "x": 330,
        "y": 260,
        "wires": [
            [
                "90413205.e39a6"
            ],
            [
                "f1469f22.1cfba"
            ]
        ]
    },
    {
        "id": "f000bc00.cb551",
        "type": "change",
        "z": "715c9f22.80b84",
        "name": "",
        "rules": [
            {
                "t": "set",
                "p": "sofa_light_dim",
                "pt": "flow",
                "to": "payload.event.command",
                "tot": "msg"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 180,
        "y": 180,
        "wires": [
            [
                "3330c43e.a9732c"
            ]
        ]
    },
    {
        "id": "90413205.e39a6",
        "type": "api-call-service",
        "z": "715c9f22.80b84",
        "name": "Sofa Light +10% ",
        "server": "e7bd0652.9f3af8",
        "version": 1,
        "debugenabled": false,
        "service_domain": "light",
        "service": "turn_on",
        "entityId": "light.sofa_light",
        "data": "{\"brightness_step_pct\": 10}",
        "dataType": "json",
        "mergecontext": "",
        "output_location": "",
        "output_location_type": "none",
        "mustacheAltTags": false,
        "x": 570,
        "y": 240,
        "wires": [
            []
        ]
    },
    {
        "id": "f1469f22.1cfba",
        "type": "api-call-service",
        "z": "715c9f22.80b84",
        "name": "Sofa Light -10%",
        "server": "e7bd0652.9f3af8",
        "version": 1,
        "debugenabled": false,
        "service_domain": "light",
        "service": "turn_on",
        "entityId": "light.sofa_light",
        "data": "{\"brightness_step_pct\": -10}",
        "dataType": "json",
        "mergecontext": "",
        "output_location": "",
        "output_location_type": "none",
        "mustacheAltTags": false,
        "x": 560,
        "y": 280,
        "wires": [
            []
        ]
    },
    {
        "id": "362764af.0bcafc",
        "type": "comment",
        "z": "715c9f22.80b84",
        "name": "SOFA LIGHT",
        "info": "",
        "x": 110,
        "y": 120,
        "wires": []
    },
    {
        "id": "be9be0f4.3655a",
        "type": "api-current-state",
        "z": "715c9f22.80b84",
        "name": "",
        "server": "e7bd0652.9f3af8",
        "version": 1,
        "outputs": 1,
        "halt_if": "",
        "halt_if_type": "str",
        "halt_if_compare": "is",
        "override_topic": false,
        "entity_id": "sofa_light",
        "state_type": "str",
        "state_location": "payload",
        "override_payload": "msg",
        "entity_location": "data",
        "override_data": "msg",
        "blockInputOverrides": false,
        "x": 590,
        "y": 160,
        "wires": [
            [
                "e5e936da.c604a8"
            ]
        ]
    },
    {
        "id": "e5e936da.c604a8",
        "type": "switch",
        "z": "715c9f22.80b84",
        "name": "",
        "property": "payload",
        "propertyType": "msg",
        "rules": [
            {
                "t": "eq",
                "v": "on",
                "vt": "str"
            },
            {
                "t": "eq",
                "v": "off",
                "vt": "str"
            }
        ],
        "checkall": "true",
        "repair": false,
        "outputs": 2,
        "x": 770,
        "y": 160,
        "wires": [
            [
                "c3f309d.9a563f8"
            ],
            [
                "d377f910.368d78"
            ]
        ]
    },
    {
        "id": "d377f910.368d78",
        "type": "api-call-service",
        "z": "715c9f22.80b84",
        "name": "Turn Sofa Light ON",
        "server": "e7bd0652.9f3af8",
        "version": 1,
        "debugenabled": false,
        "service_domain": "light",
        "service": "turn_on",
        "entityId": "light.sofa_light",
        "data": "",
        "dataType": "json",
        "mergecontext": "",
        "output_location": "",
        "output_location_type": "none",
        "mustacheAltTags": false,
        "x": 930,
        "y": 160,
        "wires": [
            []
        ]
    },
    {
        "id": "fa19f399.14346",
        "type": "api-current-state",
        "z": "715c9f22.80b84",
        "name": "",
        "server": "e7bd0652.9f3af8",
        "version": 1,
        "outputs": 1,
        "halt_if": "",
        "halt_if_type": "str",
        "halt_if_compare": "is",
        "override_topic": false,
        "entity_id": "sofa_light",
        "state_type": "str",
        "state_location": "payload",
        "override_payload": "msg",
        "entity_location": "data",
        "override_data": "msg",
        "blockInputOverrides": false,
        "x": 590,
        "y": 200,
        "wires": [
            [
                "c9bbc5c1.e1fbb8"
            ]
        ]
    },
    {
        "id": "c9bbc5c1.e1fbb8",
        "type": "switch",
        "z": "715c9f22.80b84",
        "name": "",
        "property": "payload",
        "propertyType": "msg",
        "rules": [
            {
                "t": "eq",
                "v": "on",
                "vt": "str"
            },
            {
                "t": "eq",
                "v": "off",
                "vt": "str"
            }
        ],
        "checkall": "true",
        "repair": false,
        "outputs": 2,
        "x": 770,
        "y": 200,
        "wires": [
            [
                "b6251f12.9fc34"
            ],
            [
                "bd53051e.250238"
            ]
        ]
    },
    {
        "id": "bd53051e.250238",
        "type": "api-call-service",
        "z": "715c9f22.80b84",
        "name": "IF ALREADY OFF ==> 1%",
        "server": "e7bd0652.9f3af8",
        "version": 1,
        "debugenabled": false,
        "service_domain": "light",
        "service": "turn_on",
        "entityId": "light.sofa_light",
        "data": "{\"brightness_pct\": 1}",
        "dataType": "json",
        "mergecontext": "",
        "output_location": "",
        "output_location_type": "none",
        "mustacheAltTags": false,
        "x": 960,
        "y": 240,
        "wires": [
            []
        ]
    },
    {
        "id": "3906ca9c.a35966",
        "type": "switch",
        "z": "715c9f22.80b84",
        "name": "which device",
        "property": "payload.event.device_ieee",
        "propertyType": "msg",
        "rules": [
            {
                "t": "eq",
                "v": "90:fd:9f:xx:xx:xx:xx:xx",
                "vt": "str"
            },
            {
                "t": "eq",
                "v": "cc:cc:cc:xx:xx:xx:xx:xx",
                "vt": "str"
            }
        ],
        "checkall": "true",
        "repair": false,
        "outputs": 2,
        "x": 330,
        "y": 60,
        "wires": [
            [],
            [
                "f000bc00.cb551"
            ]
        ]
    },
    {
        "id": "f6df66e5.1ef718",
        "type": "server-events",
        "z": "715c9f22.80b84",
        "name": "",
        "server": "e7bd0652.9f3af8",
        "event_type": "zha_event",
        "exposeToHomeAssistant": false,
        "haConfig": [
            {
                "property": "name",
                "value": ""
            },
            {
                "property": "icon",
                "value": ""
            }
        ],
        "waitForRunning": true,
        "x": 130,
        "y": 60,
        "wires": [
            [
                "3906ca9c.a35966"
            ]
        ]
    },
    {
        "id": "e7bd0652.9f3af8",
        "type": "server",
        "z": "",
        "name": "Home Assistant",
        "addon": true
    }
]
```
