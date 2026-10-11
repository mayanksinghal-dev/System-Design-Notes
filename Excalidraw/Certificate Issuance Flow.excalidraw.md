---

excalidraw-plugin: parsed
tags: [excalidraw]

---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠==


# Excalidraw Data

## Text Elements
1. Server generates
key pair (priv + pub) ^e000023228

2. Create CSR
(pub key + domain,
signed with priv) ^e000041958

3. CA validates
domain (DV/OV/EV)
HTTP-01 / DNS-01 ^e000061432

4. CA signs cert
with CA private key ^e000089088

5. Server installs
cert + chain ^e000101908

6. Client verifies
using CA public key
(trust store) ^e000124423

TLS handshake ^e000187654

Private key NEVER leaves the server; the CA only sees the public key. ^e000195536

%%
## Drawing
```json
{
 "type": "excalidraw",
 "version": 2,
 "source": "https://github.com/zsviczian/obsidian-excalidraw-plugin",
 "elements": [
  {
   "angle": 0,
   "strokeColor": "#1e1e1e",
   "backgroundColor": "#d0bfff",
   "fillStyle": "solid",
   "strokeWidth": 2,
   "strokeStyle": "solid",
   "roughness": 1,
   "opacity": 100,
   "groupIds": [],
   "frameId": null,
   "roundness": {
    "type": 3
   },
   "seed": 1,
   "version": 1,
   "versionNonce": 1,
   "isDeleted": false,
   "boundElements": [
    {
     "id": "e000023228",
     "type": "text"
    }
   ],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000013434",
   "type": "rectangle",
   "x": 0,
   "y": 0,
   "width": 240,
   "height": 80
  },
  {
   "angle": 0,
   "strokeColor": "#1e1e1e",
   "backgroundColor": "transparent",
   "fillStyle": "solid",
   "strokeWidth": 2,
   "strokeStyle": "solid",
   "roughness": 1,
   "opacity": 100,
   "groupIds": [],
   "frameId": null,
   "roundness": null,
   "seed": 1,
   "version": 1,
   "versionNonce": 1,
   "isDeleted": false,
   "boundElements": [],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000023228",
   "type": "text",
   "x": 16.049999999999997,
   "y": 17.5,
   "width": 207.9,
   "height": 45.0,
   "text": "1. Server generates\nkey pair (priv + pub)",
   "originalText": "1. Server generates\nkey pair (priv + pub)",
   "fontSize": 18,
   "fontFamily": 1,
   "textAlign": "center",
   "verticalAlign": "middle",
   "containerId": "e000013434",
   "lineHeight": 1.25,
   "baseline": 18,
   "autoResize": true
  },
  {
   "angle": 0,
   "strokeColor": "#1e1e1e",
   "backgroundColor": "#ffec99",
   "fillStyle": "solid",
   "strokeWidth": 2,
   "strokeStyle": "solid",
   "roughness": 1,
   "opacity": 100,
   "groupIds": [],
   "frameId": null,
   "roundness": {
    "type": 3
   },
   "seed": 1,
   "version": 1,
   "versionNonce": 1,
   "isDeleted": false,
   "boundElements": [
    {
     "id": "e000041958",
     "type": "text"
    }
   ],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000036007",
   "type": "rectangle",
   "x": 330,
   "y": 0,
   "width": 240,
   "height": 80
  },
  {
   "angle": 0,
   "strokeColor": "#1e1e1e",
   "backgroundColor": "transparent",
   "fillStyle": "solid",
   "strokeWidth": 2,
   "strokeStyle": "solid",
   "roughness": 1,
   "opacity": 100,
   "groupIds": [],
   "frameId": null,
   "roundness": null,
   "seed": 1,
   "version": 1,
   "versionNonce": 1,
   "isDeleted": false,
   "boundElements": [],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000041958",
   "type": "text",
   "x": 360.9,
   "y": 6.25,
   "width": 178.20000000000002,
   "height": 67.5,
   "text": "2. Create CSR\n(pub key + domain,\nsigned with priv)",
   "originalText": "2. Create CSR\n(pub key + domain,\nsigned with priv)",
   "fontSize": 18,
   "fontFamily": 1,
   "textAlign": "center",
   "verticalAlign": "middle",
   "containerId": "e000036007",
   "lineHeight": 1.25,
   "baseline": 18,
   "autoResize": true
  },
  {
   "angle": 0,
   "strokeColor": "#1e1e1e",
   "backgroundColor": "#ffc9c9",
   "fillStyle": "solid",
   "strokeWidth": 2,
   "strokeStyle": "solid",
   "roughness": 1,
   "opacity": 100,
   "groupIds": [],
   "frameId": null,
   "roundness": {
    "type": 3
   },
   "seed": 1,
   "version": 1,
   "versionNonce": 1,
   "isDeleted": false,
   "boundElements": [
    {
     "id": "e000061432",
     "type": "text"
    }
   ],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000053783",
   "type": "rectangle",
   "x": 660,
   "y": 0,
   "width": 240,
   "height": 80
  },
  {
   "angle": 0,
   "strokeColor": "#1e1e1e",
   "backgroundColor": "transparent",
   "fillStyle": "solid",
   "strokeWidth": 2,
   "strokeStyle": "solid",
   "roughness": 1,
   "opacity": 100,
   "groupIds": [],
   "frameId": null,
   "roundness": null,
   "seed": 1,
   "version": 1,
   "versionNonce": 1,
   "isDeleted": false,
   "boundElements": [],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000061432",
   "type": "text",
   "x": 695.85,
   "y": 6.25,
   "width": 168.3,
   "height": 67.5,
   "text": "3. CA validates\ndomain (DV/OV/EV)\nHTTP-01 / DNS-01",
   "originalText": "3. CA validates\ndomain (DV/OV/EV)\nHTTP-01 / DNS-01",
   "fontSize": 18,
   "fontFamily": 1,
   "textAlign": "center",
   "verticalAlign": "middle",
   "containerId": "e000053783",
   "lineHeight": 1.25,
   "baseline": 18,
   "autoResize": true
  },
  {
   "angle": 0,
   "strokeColor": "#1e1e1e",
   "backgroundColor": "#ffc9c9",
   "fillStyle": "solid",
   "strokeWidth": 2,
   "strokeStyle": "solid",
   "roughness": 1,
   "opacity": 100,
   "groupIds": [],
   "frameId": null,
   "roundness": {
    "type": 3
   },
   "seed": 1,
   "version": 1,
   "versionNonce": 1,
   "isDeleted": false,
   "boundElements": [
    {
     "id": "e000089088",
     "type": "text"
    }
   ],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000076322",
   "type": "rectangle",
   "x": 660,
   "y": 170,
   "width": 240,
   "height": 80
  },
  {
   "angle": 0,
   "strokeColor": "#1e1e1e",
   "backgroundColor": "transparent",
   "fillStyle": "solid",
   "strokeWidth": 2,
   "strokeStyle": "solid",
   "roughness": 1,
   "opacity": 100,
   "groupIds": [],
   "frameId": null,
   "roundness": null,
   "seed": 1,
   "version": 1,
   "versionNonce": 1,
   "isDeleted": false,
   "boundElements": [],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000089088",
   "type": "text",
   "x": 685.95,
   "y": 187.5,
   "width": 188.10000000000002,
   "height": 45.0,
   "text": "4. CA signs cert\nwith CA private key",
   "originalText": "4. CA signs cert\nwith CA private key",
   "fontSize": 18,
   "fontFamily": 1,
   "textAlign": "center",
   "verticalAlign": "middle",
   "containerId": "e000076322",
   "lineHeight": 1.25,
   "baseline": 18,
   "autoResize": true
  },
  {
   "angle": 0,
   "strokeColor": "#1e1e1e",
   "backgroundColor": "#b2f2bb",
   "fillStyle": "solid",
   "strokeWidth": 2,
   "strokeStyle": "solid",
   "roughness": 1,
   "opacity": 100,
   "groupIds": [],
   "frameId": null,
   "roundness": {
    "type": 3
   },
   "seed": 1,
   "version": 1,
   "versionNonce": 1,
   "isDeleted": false,
   "boundElements": [
    {
     "id": "e000101908",
     "type": "text"
    }
   ],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000093175",
   "type": "rectangle",
   "x": 330,
   "y": 170,
   "width": 240,
   "height": 80
  },
  {
   "angle": 0,
   "strokeColor": "#1e1e1e",
   "backgroundColor": "transparent",
   "fillStyle": "solid",
   "strokeWidth": 2,
   "strokeStyle": "solid",
   "roughness": 1,
   "opacity": 100,
   "groupIds": [],
   "frameId": null,
   "roundness": null,
   "seed": 1,
   "version": 1,
   "versionNonce": 1,
   "isDeleted": false,
   "boundElements": [],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000101908",
   "type": "text",
   "x": 360.9,
   "y": 187.5,
   "width": 178.20000000000002,
   "height": 45.0,
   "text": "5. Server installs\ncert + chain",
   "originalText": "5. Server installs\ncert + chain",
   "fontSize": 18,
   "fontFamily": 1,
   "textAlign": "center",
   "verticalAlign": "middle",
   "containerId": "e000093175",
   "lineHeight": 1.25,
   "baseline": 18,
   "autoResize": true
  },
  {
   "angle": 0,
   "strokeColor": "#1e1e1e",
   "backgroundColor": "#a5d8ff",
   "fillStyle": "solid",
   "strokeWidth": 2,
   "strokeStyle": "solid",
   "roughness": 1,
   "opacity": 100,
   "groupIds": [],
   "frameId": null,
   "roundness": {
    "type": 3
   },
   "seed": 1,
   "version": 1,
   "versionNonce": 1,
   "isDeleted": false,
   "boundElements": [
    {
     "id": "e000124423",
     "type": "text"
    }
   ],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000115904",
   "type": "rectangle",
   "x": 0,
   "y": 170,
   "width": 240,
   "height": 80
  },
  {
   "angle": 0,
   "strokeColor": "#1e1e1e",
   "backgroundColor": "transparent",
   "fillStyle": "solid",
   "strokeWidth": 2,
   "strokeStyle": "solid",
   "roughness": 1,
   "opacity": 100,
   "groupIds": [],
   "frameId": null,
   "roundness": null,
   "seed": 1,
   "version": 1,
   "versionNonce": 1,
   "isDeleted": false,
   "boundElements": [],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000124423",
   "type": "text",
   "x": 25.94999999999999,
   "y": 176.25,
   "width": 188.10000000000002,
   "height": 67.5,
   "text": "6. Client verifies\nusing CA public key\n(trust store)",
   "originalText": "6. Client verifies\nusing CA public key\n(trust store)",
   "fontSize": 18,
   "fontFamily": 1,
   "textAlign": "center",
   "verticalAlign": "middle",
   "containerId": "e000115904",
   "lineHeight": 1.25,
   "baseline": 18,
   "autoResize": true
  },
  {
   "angle": 0,
   "strokeColor": "#1e1e1e",
   "backgroundColor": "transparent",
   "fillStyle": "solid",
   "strokeWidth": 2,
   "strokeStyle": "solid",
   "roughness": 1,
   "opacity": 100,
   "groupIds": [],
   "frameId": null,
   "roundness": {
    "type": 2
   },
   "seed": 1,
   "version": 1,
   "versionNonce": 1,
   "isDeleted": false,
   "boundElements": [],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000139048",
   "type": "arrow",
   "x": 240,
   "y": 40,
   "width": 90,
   "height": 0,
   "points": [
    [
     0,
     0
    ],
    [
     90,
     0
    ]
   ],
   "startBinding": null,
   "endBinding": null,
   "startArrowhead": null,
   "endArrowhead": "arrow",
   "lastCommittedPoint": null
  },
  {
   "angle": 0,
   "strokeColor": "#1e1e1e",
   "backgroundColor": "transparent",
   "fillStyle": "solid",
   "strokeWidth": 2,
   "strokeStyle": "solid",
   "roughness": 1,
   "opacity": 100,
   "groupIds": [],
   "frameId": null,
   "roundness": {
    "type": 2
   },
   "seed": 1,
   "version": 1,
   "versionNonce": 1,
   "isDeleted": false,
   "boundElements": [],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000148771",
   "type": "arrow",
   "x": 570,
   "y": 40,
   "width": 90,
   "height": 0,
   "points": [
    [
     0,
     0
    ],
    [
     90,
     0
    ]
   ],
   "startBinding": null,
   "endBinding": null,
   "startArrowhead": null,
   "endArrowhead": "arrow",
   "lastCommittedPoint": null
  },
  {
   "angle": 0,
   "strokeColor": "#1e1e1e",
   "backgroundColor": "transparent",
   "fillStyle": "solid",
   "strokeWidth": 2,
   "strokeStyle": "solid",
   "roughness": 1,
   "opacity": 100,
   "groupIds": [],
   "frameId": null,
   "roundness": {
    "type": 2
   },
   "seed": 1,
   "version": 1,
   "versionNonce": 1,
   "isDeleted": false,
   "boundElements": [],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000151090",
   "type": "arrow",
   "x": 780,
   "y": 80,
   "width": 0,
   "height": 90,
   "points": [
    [
     0,
     0
    ],
    [
     0,
     90
    ]
   ],
   "startBinding": null,
   "endBinding": null,
   "startArrowhead": null,
   "endArrowhead": "arrow",
   "lastCommittedPoint": null
  },
  {
   "angle": 0,
   "strokeColor": "#1e1e1e",
   "backgroundColor": "transparent",
   "fillStyle": "solid",
   "strokeWidth": 2,
   "strokeStyle": "solid",
   "roughness": 1,
   "opacity": 100,
   "groupIds": [],
   "frameId": null,
   "roundness": {
    "type": 2
   },
   "seed": 1,
   "version": 1,
   "versionNonce": 1,
   "isDeleted": false,
   "boundElements": [],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000163861",
   "type": "arrow",
   "x": 660,
   "y": 210,
   "width": 90,
   "height": 0,
   "points": [
    [
     0,
     0
    ],
    [
     -90,
     0
    ]
   ],
   "startBinding": null,
   "endBinding": null,
   "startArrowhead": null,
   "endArrowhead": "arrow",
   "lastCommittedPoint": null
  },
  {
   "angle": 0,
   "strokeColor": "#1e1e1e",
   "backgroundColor": "transparent",
   "fillStyle": "solid",
   "strokeWidth": 2,
   "strokeStyle": "solid",
   "roughness": 1,
   "opacity": 100,
   "groupIds": [],
   "frameId": null,
   "roundness": {
    "type": 2
   },
   "seed": 1,
   "version": 1,
   "versionNonce": 1,
   "isDeleted": false,
   "boundElements": [],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000179141",
   "type": "arrow",
   "x": 330,
   "y": 210,
   "width": 90,
   "height": 0,
   "points": [
    [
     0,
     0
    ],
    [
     -90,
     0
    ]
   ],
   "startBinding": null,
   "endBinding": null,
   "startArrowhead": null,
   "endArrowhead": "arrow",
   "lastCommittedPoint": null
  },
  {
   "angle": 0,
   "strokeColor": "#1971c2",
   "backgroundColor": "transparent",
   "fillStyle": "solid",
   "strokeWidth": 2,
   "strokeStyle": "solid",
   "roughness": 1,
   "opacity": 100,
   "groupIds": [],
   "frameId": null,
   "roundness": null,
   "seed": 1,
   "version": 1,
   "versionNonce": 1,
   "isDeleted": false,
   "boundElements": [],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000187654",
   "type": "text",
   "x": 250,
   "y": 188.0,
   "width": 114.4,
   "height": 20.0,
   "text": "TLS handshake",
   "originalText": "TLS handshake",
   "fontSize": 16,
   "fontFamily": 1,
   "textAlign": "left",
   "verticalAlign": "top",
   "containerId": null,
   "lineHeight": 1.25,
   "baseline": 16,
   "autoResize": true
  },
  {
   "angle": 0,
   "strokeColor": "#1e1e1e",
   "backgroundColor": "transparent",
   "fillStyle": "solid",
   "strokeWidth": 2,
   "strokeStyle": "solid",
   "roughness": 1,
   "opacity": 100,
   "groupIds": [],
   "frameId": null,
   "roundness": null,
   "seed": 1,
   "version": 1,
   "versionNonce": 1,
   "isDeleted": false,
   "boundElements": [],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000195536",
   "type": "text",
   "x": 0,
   "y": 290,
   "width": 683.1,
   "height": 22.5,
   "text": "Private key NEVER leaves the server; the CA only sees the public key.",
   "originalText": "Private key NEVER leaves the server; the CA only sees the public key.",
   "fontSize": 18,
   "fontFamily": 1,
   "textAlign": "left",
   "verticalAlign": "top",
   "containerId": null,
   "lineHeight": 1.25,
   "baseline": 18,
   "autoResize": true
  }
 ],
 "appState": {
  "gridSize": null,
  "viewBackgroundColor": "#ffffff"
 },
 "files": {}
}
```
%%