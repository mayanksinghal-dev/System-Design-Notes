---

excalidraw-plugin: parsed
tags: [excalidraw]

---
==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠==


# Excalidraw Data

## Text Elements
Root CA
(self-signed, in OS/browser trust store) ^e000027178

Intermediate CA
(signed by Root's private key) ^e000041499

Leaf / Server Certificate
CN=example.com (signed by Intermediate) ^e000069911

signs ^e000084538

signs ^e000109764

Certificate contains:
• Subject (domain / SAN)
• Subject's PUBLIC key
• Issuer
• Validity (not before/after)
• Issuer's digital signature ^e000128819

Client verifies bottom → up:
signature valid? not expired? domain matches?
not revoked (CRL/OCSP)? chain ends at trusted Root? ^e000143407

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
     "id": "e000027178",
     "type": "text"
    }
   ],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000015997",
   "type": "rectangle",
   "x": 0,
   "y": 0,
   "width": 300,
   "height": 90
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
   "id": "e000027178",
   "type": "text",
   "x": -48.00000000000003,
   "y": 22.5,
   "width": 396.00000000000006,
   "height": 45.0,
   "text": "Root CA\n(self-signed, in OS/browser trust store)",
   "originalText": "Root CA\n(self-signed, in OS/browser trust store)",
   "fontSize": 18,
   "fontFamily": 1,
   "textAlign": "center",
   "verticalAlign": "middle",
   "containerId": "e000015997",
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
     "id": "e000041499",
     "type": "text"
    }
   ],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000031958",
   "type": "rectangle",
   "x": 0,
   "y": 170,
   "width": 300,
   "height": 90
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
   "id": "e000041499",
   "type": "text",
   "x": 1.5,
   "y": 192.5,
   "width": 297.0,
   "height": 45.0,
   "text": "Intermediate CA\n(signed by Root's private key)",
   "originalText": "Intermediate CA\n(signed by Root's private key)",
   "fontSize": 18,
   "fontFamily": 1,
   "textAlign": "center",
   "verticalAlign": "middle",
   "containerId": "e000031958",
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
     "id": "e000069911",
     "type": "text"
    }
   ],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000051502",
   "type": "rectangle",
   "x": 0,
   "y": 340,
   "width": 300,
   "height": 90
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
   "id": "e000069911",
   "type": "text",
   "x": -43.05000000000001,
   "y": 362.5,
   "width": 386.1,
   "height": 45.0,
   "text": "Leaf / Server Certificate\nCN=example.com (signed by Intermediate)",
   "originalText": "Leaf / Server Certificate\nCN=example.com (signed by Intermediate)",
   "fontSize": 18,
   "fontFamily": 1,
   "textAlign": "center",
   "verticalAlign": "middle",
   "containerId": "e000051502",
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
   "id": "e000078870",
   "type": "arrow",
   "x": 150,
   "y": 90,
   "width": 0,
   "height": 80,
   "points": [
    [
     0,
     0
    ],
    [
     0,
     80
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
   "id": "e000084538",
   "type": "text",
   "x": 160,
   "y": 130.0,
   "width": 44.0,
   "height": 20.0,
   "text": "signs",
   "originalText": "signs",
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
   "id": "e000094918",
   "type": "arrow",
   "x": 150,
   "y": 260,
   "width": 0,
   "height": 80,
   "points": [
    [
     0,
     0
    ],
    [
     0,
     80
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
   "id": "e000109764",
   "type": "text",
   "x": 160,
   "y": 300.0,
   "width": 44.0,
   "height": 20.0,
   "text": "signs",
   "originalText": "signs",
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
     "id": "e000128819",
     "type": "text"
    }
   ],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000119976",
   "type": "rectangle",
   "x": 420,
   "y": 330,
   "width": 330,
   "height": 190
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
   "id": "e000128819",
   "type": "text",
   "x": 441.45,
   "y": 357.5,
   "width": 287.1,
   "height": 135.0,
   "text": "Certificate contains:\n\u2022 Subject (domain / SAN)\n\u2022 Subject's PUBLIC key\n\u2022 Issuer\n\u2022 Validity (not before/after)\n\u2022 Issuer's digital signature",
   "originalText": "Certificate contains:\n\u2022 Subject (domain / SAN)\n\u2022 Subject's PUBLIC key\n\u2022 Issuer\n\u2022 Validity (not before/after)\n\u2022 Issuer's digital signature",
   "fontSize": 18,
   "fontFamily": 1,
   "textAlign": "center",
   "verticalAlign": "middle",
   "containerId": "e000119976",
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
   "id": "e000132972",
   "type": "arrow",
   "x": 300,
   "y": 385,
   "width": 120,
   "height": 15,
   "points": [
    [
     0,
     0
    ],
    [
     120,
     15
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
   "roundness": null,
   "seed": 1,
   "version": 1,
   "versionNonce": 1,
   "isDeleted": false,
   "boundElements": [],
   "updated": 1,
   "link": null,
   "locked": false,
   "id": "e000143407",
   "type": "text",
   "x": 0,
   "y": 470,
   "width": 504.90000000000003,
   "height": 67.5,
   "text": "Client verifies bottom \u2192 up:\nsignature valid? not expired? domain matches?\nnot revoked (CRL/OCSP)? chain ends at trusted Root?",
   "originalText": "Client verifies bottom \u2192 up:\nsignature valid? not expired? domain matches?\nnot revoked (CRL/OCSP)? chain ends at trusted Root?",
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