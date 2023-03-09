---
id: validator-staking-operations
title: การ Stake ใน Polygon
description: เรียนรู้วิธีการเดิมพันเป็นตัวตรวจสอบความถูกต้องบนเครือข่าย Polygon
keywords:
  - docs
  - matic
  - polygon
  - stake
  - claim
  - unstake
slug: validator-staking-operations
image: https://wiki.polygon.technology/img/polygon-wiki.png
---
import useBaseUrl from '@docusaurus/useBaseUrl';

## ข้อกำหนดเบื้องต้น {#prerequisites}

### การติดตั้งโหนดเต็มรูปแบบ {#full-node-set-up}

โหนดตัวตรวจสอบความถูกต้องของคุณตั้งค่าและซิงค์ได้อย่างสมบูรณ์ดูเพิ่มเติมที่:

* [เรียกใช้โหนดตัวตรวจสอบความถูกต้อง](run-validator.md)
* [รันโหนดตัวตรวจสอบความถูกต้องด้วย Ansible](run-validator-ansible.md)
* [เรียกใช้โหนดผู้ตรวจสอบความถูกต้องจากไบนารี](run-validator-binaries.md)

### การกำหนดค่าบัญชี {#account-setup}

บนโหนดตัวตรวจสอบความถูกต้องของคุณ ตรวจสอบว่าตั้งค่าบัญชีแล้วหากต้องการตรวจสอบ โปรดเรียกใช้คำสั่ง**ในโหนดผู้ตรวจสอบความถูกต้อง**:

```sh
    heimdalld show-account
```

เอาท์พุตของคุณต้องปรากฏตามรูปแบบดังต่อไปนี้:

```json
{
    "address": "0x6c468CF8c9879006E22EC4029696E005C2319C9D",
    "pub_key": "0x04b12d8b2f6e3d45a7ace12c4b2158f79b95e4c28ebe5ad54c439be9431d7fc9dc1164210bf6a5c3b8523528b931e772c86a307e8cff4b725e6b4a77d21417bf19"
}
```

จะมีการแสดงที่อยู่ของคุณและคีย์สาธารณะสำหรับโหนดผู้ตรวจสอบความถูกต้องของคุณ โปรดทราบว่า**ที่อยู่นี้จะต้องตรงกับที่อยู่ผู้ลงนามของคุณบน Ethereum**

### การแสดงคีย์ส่วนตัว {#show-private-key}

ขั้นตอนนี้ไม่ได้บังคับ

บนโหนดตัวตรวจสอบความถูกต้องของคุณ ตรวจสอบว่าคีย์ส่วนตัวถูกต้องหากต้องการตรวจสอบ โปรดเรียกใช้คำสั่ง**ในโหนดผู้ตรวจสอบความถูกต้อง**:

```sh
heimdalld show-privatekey
```

ต้องมีเอาท์พุตดังต่อไปนี้:

```json
{
    "priv_key": "0x********************************************************"
}
```

## การ Stake ใน Polygon {#stake-on-polygon}

คุณสามารถทำการ Stake ใน Polygon โดยใช้ [แดชบอร์ดของผู้ตรวจสอบ](https://staking.polygon.technology/validators/)

### การ Stake โดยใช้แดชบอร์ดการ Stake {#stake-using-the-staking-dashboard}

1. เข้าถึง [แดชบอร์ดของผู้ตรวจสอบ](https://staking.polygon.technology/validators/)
2. เข้าสู่ระบบด้วยวอลเล็ตของคุณ MetaMask คือกระเป๋าสตางค์ที่แนะนำคุณต้องตรวจสอบให้แน่ใจว่า คุณล็อกอินโดยใช้ที่อยู่เดียวกันกับที่ใช้ Matic ของคุณอยู่
3. คลิก**กลายเป็นตัวตรวจสอบความถูกต้อง**คุณจะถูกขอให้ตั้งโหนดของคุณหากตอนนี้ คุณยังไม่ได้ตั้งค่าโหนดของคุณ คุณจำเป็นต้องดำเนินการดังกล่าว มิฉะนั้นหากคุณดำเนินการต่อไป คุณจะได้รับข้อความแจ้งข้อผิดพลาดเมื่อคุณพยายามทำการ Stake
4. บนหน้าจอถัดไป โปรดเพิ่มรายละเอียดผู้ตรวจสอบของคุณ อัตราค่าคอมมิชชั่น และจำนวนการ Stake
5. คลิก **Stake ตอนนี้**

เมื่อทำธุรกรรมเสร็จแล้ว จะถือว่าคุณได้ทำการ Stake เพื่อเป็นผู้ตรวจสอบได้อย่างสำเร็จ คุณจะได้รับการร้องขอให้ยืนยันธุรกรรมสามครั้ง

* อนุมัติธุรกรรม - การดำเนินการนี้จะอนุมัติธุรกรรม Stake ของคุณ
* Stake - การดำเนินการนี้จะยืนยันธุรกรรม Stake ของคุณ
* บันทึก -ß การดำเนินการนี้จะบันทึกรายละเอียดผู้ตรวจสอบของคุณ

:::note

เพื่อให้การเปลี่ยนแปลงมีผลใน [แดชบอร์ดการ Stake](https://staking.polygon.technology/account) คุณต้องยืนยันบล็อกอย่างน้อย 12 อัน

:::

### ตรวจสอบยอดคงเหลือ {#check-the-balance}

หากต้องการตรวจสอบยอดคงเหลือในที่อยู่ของคุณ:

```sh
heimdallcli query auth account SIGNER_ADDRESS --chain-id CHAIN_ID
```

เมื่อ

* SIGNER_ADDRESS - [ที่อยู่ผู้ลงนาม](/docs/maintain/glossary.md#validator) ของคุณ
* CHAIN_ID — ID เชนของ Polygon Mainnet พร้อมfด้วยคำนำหน้าไคลเอ็นต์: `heimdall-137`

ต้องมีเอาท์พุตดังต่อไปนี้:

```json
address: 0x6c468cf8c9879006e22ec4029696e005c2319c9d
coins:
- denom: matic
amount:
    i: "1000000000000000000000"
accountnumber: 0
sequence: 0
```

### การรับผลตอบแทนในฐานะผู้ตรวจสอบ {#claim-rewards-as-a-validator}

เมื่อคุณปรับการตั้งค่าและได้ทำการ Stake ในฐานะผู้ตรวจสอบแล้ว คุณจะได้รับผลตอบแทนสำหรับการปฏิบัติหน้าที่ในฐานะผู้ตรวจสอบ เมื่อคุณปฏิบัติหน้าที่ในฐานะผู้ตรวจสอบอย่างถูกต้อง คุณจะได้รับผลตอบแทน

หากต้องการขอรับรางวัล คุณสามารถไปที่ [แดชบอร์ดผู้ตรวจสอบ](https://staking.polygon.technology/account) ของคุณ

คุณจะเห็นปุ่มสองอันในโปรไฟล์ของคุณ:

* การถอนผลตอบแทน
* การ Stake ผลตอบแทนอีกครั้ง

#### การถอนผลตอบแทน {#withdraw-reward}

ในฐานะผู้ตรวจสอบคุณจะได้รับผลตอบแทนต่อเมื่อคุณปฏิบัติหน้าที่ในฐานะผู้ตรวจสอบอย่างถูกต้อง

การคลิก **ถอนผลตอบแทน** จะทำให้คุณได้รับผลตอบแทนของคุณเข้ากลับไปในวอลเล็ตของคุณ

แดชบอร์ดจะได้รับการอัปเดต หลังจากการยืนยันบล็อก 12 อัน

#### การ Stake ผลตอบแทนอีกครั้ง {#restake-reward}

การ Stake ผลตอบแทนอีกครั้งเป็นวิธีง่าย ๆ ที่ใช้ในการเพิ่ม Stake ของคุณในฐานะผู้ตรวจสอบ

การคลิก **Stake ผลตอบแทนอีกครั้ง** จะเป็นการทำ Stake ผลตอบแทนของคุณใหม่และเพิ่ม Stake ของคุณ

แดชบอร์ดจะได้รับการอัปเดต หลังจากการยืนยันบล็อก 12 อัน