---
id: getting-started
title: पॉस ब्रिज
sidebar_label: Introduction
description: पॉलीगॉन पॉस के साथ ज़्यादा सुविधा और तेज निकासी.
keywords:
  - docs
  - matic
  - pos bridge
  - deposit
  - withdraw
  - mapping
  - state sync
image: https://matic.network/banners/matic-network-16x9.png
---

कृपया शुरू करने के लिए सबसे नया [पॉस का Matic.js डॉक्यूमेंटेशन](../matic-js/get-started.md) देखें.

ब्रिज असल में अनुबंध का एक सेट है जो एसेट को रूट चेन से चाइल्ड चेन तक ले जाने में सहायता करता है. एथेरेयम और पॉलीगॉन के बीच एसेट को मूव करने के लिए मुख्य रूप से दो ब्रिज हैं. पहला एक प्लाजमा ब्रिज है और दूसरा को **PoS ब्रिज** या **स्टोक ब्रिज** कहा जाता है. **प्लाज़्मा ब्रिज** प्लाज़्मा एग्ज़िट मैकेनिज्म से बढ़ी हुई सुरक्षा गारंटी देता है.

हालाँकि, चाइल्ड टोकन पर कुछ प्रतिबंध हैं और प्लाज़्मा ब्रिज पर पॉलीगॉन से एथेरेयम तक सभी एग्ज़िट /निकासी से जुड़ी 7-दिन की निकासी अवधि है.

यह उन DApps/यूज़र्स के लिए काफ़ी दुखद है, जो कुछ **लचीलापन** और **तेज़ निकासी**, चाहते हैं, और पॉलीगॉन भागीदारी के सबूत ब्रिज की दी गई बेहतर सुरक्षा से खुश हैं, जो बाहरी सत्यापनकर्ताओं के एक मजबूत सेट से सुरक्षित है.

भागीदारी का सबूत आधारित एसेट पॉस सुरक्षा देता है और एक चेकपॉइंट अंतराल के साथ तेज़ी से निकासी करता है.

## PoS ब्रिज को इस्तेमाल करने के स्टेप {#steps-to-use-the-pos-bridge}

डॉक्स के इस सेक्शन में प्रवेश करने से पहले, यह कुछ शर्तों की पूरी तरह से समझ लेने में मदद कर सकता है क्योंकि आप ब्रिज का इस्तेमाल करने की कोशिश करते समय उनसे बातचीत करेंगे: [मैपिंग](https://docs.polygon.technology/docs/develop/ethereum-polygon/submit-mapping-request/) और [स्टेट सिंक मैकेनिज्म ](https://docs.polygon.technology/docs/pos/state-sync/state-sync/).

फिर, PoS ब्रिज का इस्तेमाल करने का पहला स्टेप **रूट टोकन** और **चाइल्ड** टोकन का मैपिंग कर रहा है. इसका मतलब है कि रूट चेन पर टोकन कॉन्ट्रैक्ट और चाइल्ड चेन पर टोकन कॉन्ट्रैक्ट को अपने बीच की संपत्ति को transfer र करने के लिए एक कनेक्शन (जिसे मैपिंग) को बनाए रखना पड़ता है. अगर आप एक मैपिंग अनुरोध को जमा करने में रुचि रखते हैं, तो कृपया [इस गाइड](/docs/develop/ethereum-polygon/submit-mapping-request/) का इस्तेमाल करके करें.

निचले स्तर पर और अधिक विवरण के साथ, यह है:

### डिपाज़िट करें {#deposit}

  1. एसेट **(ERC20/ERC721/ERC1155)** टोकन के मालिक को ट्रांसफ़र किए जाने वाले टोकन की रकम को खर्च करने के लिए PoS ब्रिज पर एक विशिष्ट कॉन्ट्रैक्ट को मंज़ूरी देनी होगी. इस विशिष्ट अनुबंध को **प्रिडिकेट अनुबंध (एथे**रेयम नेटवर्क पर डिप्लॉय किया गया) कहा जाता है जो असल में ड**िपॉज़िट किए जाने वाले टोकन की रकम को लॉक कर देता है.**
  2. एक बार मंज़ूरी मिल जाने के बाद, अगला स्टेप **असेट को डिपॉज़िट करना है**. `RootChainManager`कॉन्ट्रैक्ट पर एक फंक्शन कॉल करना होता है जो बदले में पॉलीगॉन चेन पर `ChildChainManager`कॉन्ट्रैक्ट को ट्रिगर करता है.
  3. यह एक स्टेट सिंक मैकेनिज़्म के ज़रिए होता है जिसे अच्छे से [यहाँ](/docs/pos/state-sync/state-sync/) समझा जा सकता है.
  4. आंतरिक रूप `ChildChainManager`से बच्चे के टोकन कॉन्ट्रैक्ट के `deposit`फंक्शन को कॉल करता है और परिसंपत्ति टोकन की संबंधित राशि **को यूजर के खाते में मिंट किया** जाता है. यह ध्यान देना जरूरी है कि केवल बच्चे टोकन कॉन्ट्रैक्ट पर ही `deposit`समारोह को एक्सेस कर `ChildChainManager`सकते हैं.
  5. एक बार जब यूज़र को टोकन मिल जाते हैं, तो उन्हें **पॉलीगॉन चेन पर कम फ़ीस के साथ लगभग तुरंत ट्रांसफ़र किया जा सकता है**.

### निकासी {#withdrawals}

  1. Ethereum में वापस आस्तियों को वापस लेना एक 2 स्टेप की प्रक्रिया है जिसमें एसेट टोकन **को पहले पॉलीगॉन चेन पर जला** दिया जाना होता है और फिर **इस बर्न transaction transaction का सबूत** Ethereum चेन पर प्रस्तुत करना पड़ता है.
  2. बर्न ट्रांज़ैक्शन को एथेरेयम चेन में चेकपॉइंट होने में लगभग 20 मिनट से 3 घंटे तक लगते हैं. ये भागीदारी के सबूत वाले वैलिडेटर्स द्वारा किया जाता है.
  3. एक बार transaction the को चेकपॉइंट में जोड़ा जा चुका है, तो एक्टिंग को कॉल करके Ethereum पर `RootChainManager`कॉन्ट्रैक्ट पर प्रस्तुत किया जा सकता `exit`है.
  4. यह फ़ंक्शन कॉल **चेकपॉइंट समावेशन को सत्यापित करता है** और फिर प्रिडिकेट कॉन्ट्रैक्ट को ट्रिगर करता है जिसने शुरूआत में असेट डिपॉज़िट किए जाने के दौरान असेट टोकन को लॉक कर दिया था.
  5. अंतिम स्टेप के रूप में, **भविष्यवाणी कॉन्ट्रैक्ट लॉक टोकन्स को रिलीज़ करता** है और उन्हें Ethereum. पर यूजर्स के खाते में वापस कर देता है.

:::tip

एक बार मैपिंग हो जाने के बाद, आप या तो कॉन्ट्रैक्ट के साथ इंटरैक्ट करने के लिए **matic.js SDK** का इस्तेमाल कर सकते हैं या आप SDK के बिना भी ऐसा कर सकते हैं. हालाँकि, matic.js SDK को बहुत ही यूज़र फ़्रेंडली तरीके से डिज़ाइन किया गया है ताकि किसी भी एप्लिकेशन के साथ एसेट ट्रांसफ़र मैकेनिज्म को जोड़ना बहुत आसान हो जाए.

:::