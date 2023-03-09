---
id: port-management
title: नोड्स के लिए तकनीकी बुनियादी ढांचा
sidebar_label: Technical Infrastructure For Nodes
description: पॉलीगॉन नोड्स के पार इस्तेमाल किए गए डिफ़ॉल्ट पोर्ट की सूची
keywords:
  - docs
  - polygon
  - matic
  - port
  - port management
  - infrastructure
  - default ports
image: https://wiki.polygon.technology/img/polygon-wiki.png
---

यहाँ पॉलीगॉन नोड्स पर इस्तेमाल किए गए डिफ़ॉल्ट पॉर्ट्स की सूची दी गई है:

## बोर {#bor}

| ﻿नाम | पोर्ट | टैग्स | वर्णन |
|------------------------|-------|---------------------------|----------------------------------------------------------------------------------------------------------------|
| नेटवर्क लिस्निंग पोर्ट | 30303 | सार्वजनिक | नेटवर्क लिस्निंग पोर्ट. बोर इस पोर्ट का इस्तेमाल पीर्स को कनेक्ट और सिंक करने के लिए करता है |
| RPC सर्वर | 8545 | सार्वजनिक हो सकता है, आंतरिक | RPC पोर्ट बोर को ट्रांज़ैक्शन भेजने और इससे डेटा प्राप्त करने के लिए. हेम्डल चेकपॉइंट के लिए बोर हेडर्स प्राप्त करने के लिए इस पोर्ट का इस्तेमाल करता है |
| डब्ल्यूएस सर्वर | 8546 | सार्वजनिक हो सकता है, आंतरिक | वेबसॉकेट पोर्ट |
| Graphql सर्वर | 8547 | सार्वजनिक हो सकता है, आंतरिक | Graphql पोर्ट |
| प्रोमेथियस सर्वर | 9091 | सार्वजनिक हो सकता है, निगरानी करना | Grafana में डेटासोर्स के रूप में प्रोमेथियस सर्वर API. इसे nginx रिवर्स प्रॉक्सी के माध्यम से 80/443 में मैप किया जा सका है |
| Grafana सर्वर | 3001 | सार्वजनिक हो सकता है, निगरानी करना | Grafana वेब सर्वर. इसे nginx रिवर्स प्रॉक्सी के माध्यम से 80/443 में मैप किया जा सका है |
| Pprof सर्वर | 7071 | आंतरिक, निगरानी करना | बोर से मैट्रिक्स इकट्ठा करने के लिए Pprof सर्वर |
| UDP खोज | 30301 | सार्वजनिक हो सकता है, आंतरिक | बूटनोड डिफ़ॉल्ट पोर्ट (पीर खोज के लिए) |

## हेम्डल {#heimdall}

| ﻿नाम | पोर्ट | टैग्स | वर्णन |
|------------------------|-------|---------------------------|----------------------------------------------------------------------------------------------------------------|
| नेटवर्क लिस्निंग पोर्ट | 30303 | सार्वजनिक | नेटवर्क लिस्निंग पोर्ट. बोर इस पोर्ट का इस्तेमाल पीर्स को कनेक्ट और सिंक करने के लिए करता है |
| RPC सर्वर | 8545 | सार्वजनिक हो सकता है, आंतरिक | RPC पोर्ट बोर को ट्रांज़ैक्शन भेजने और इससे डेटा प्राप्त करने के लिए. हेम्डल चेकपॉइंट के लिए बोर हेडर्स प्राप्त करने के लिए इस पोर्ट का इस्तेमाल करता है |
| डब्ल्यूएस सर्वर | 8546 | सार्वजनिक हो सकता है, आंतरिक | वेबसॉकेट पोर्ट |
| Graphql सर्वर | 8547 | सार्वजनिक हो सकता है, आंतरिक | Graphql पोर्ट |
| प्रोमेथियस सर्वर | 9091 | सार्वजनिक हो सकता है, निगरानी करना | Grafana में डेटासोर्स के रूप में प्रोमेथियस सर्वर API. इसे nginx रिवर्स प्रॉक्सी के माध्यम से 80/443 में मैप किया जा सका है |
| Grafana सर्वर | 3001 | सार्वजनिक हो सकता है, निगरानी करना | Grafana वेब सर्वर. इसे nginx रिवर्स प्रॉक्सी के माध्यम से 80/443 में मैप किया जा सका है |
| Pprof सर्वर | 7071 | आंतरिक, निगरानी करना | बोर से मैट्रिक्स इकट्ठा करने के लिए Pprof सर्वर |
| UDP खोज | 30301 | सार्वजनिक हो सकता है, आंतरिक | बूटनोड डिफ़ॉल्ट पोर्ट (पीर खोज के लिए) |