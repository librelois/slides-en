class: dark, middle, center
background-image: url(../../images/moonbeam-background.png)

## Pallet Identity

_September 3rd, 2021_  
_Moonbeam training sessions_  
_Librelois <elois@purestake.com>_

Follow the presentation on your screen:

https://librelois.github.io/slides-en/moonbeam-training/pallet-identity

---

layout: true
class: dark
background-image: url(../../images/moonbeam-background.png)

.center[Pallet Identity]

---

## Summary

1. [Features](#features)
1. [Federated naming system](#federated)
1. [Judgement](#judgement)
1. [Sub-identities](#subidentities)
1. [Limitations](#limitations)


---

name: features

## .center[Features]

* Address => identity (default fields + any additional field like telegram, or whatever you want)

--

  * Defaut fields: display, legal, web, riot, email, pgp, image, twitter.

* Each field can contain arbitrary bytes or a hash.

???

The protocol only defines a maximum number of additional fields. Each identity owner can create the fields he wants as long as he stays within the limit of the maximum number of additional fields.

--

* Validations of some fields by accredited "third parties"

--

* Sub-identities

---

name: federated

## .center[Federated naming system]

* "third parties" are called registrars and can only be added or removed by a specified origin (An half of the council in the case of moonriver).

--
* Each registrar indicates which fields it checks and how much it charges to perform a check.

--
* Si le registrar n'indique aucun champ, on s'attend à ce qu'il vérifie les champs par défaut.

<div class="center">
  <div class="mermaid">
    graph TD
    R1[[Registrat 1]] -->|Check default fields| I1(Identity 1)
    R1 -->|Check default fields| I2(Identity 2)
    R2[[Registrat 2]] -->|Check default+website| I2
    R2 -->|Check default+website| I3(Identity 3)
  </div>
</div>


???

For instance, a telegram bot that only checks the telegram account of an identity. The registrar who owns this bot can indicate that it only checks the telegram field.

---

name: judgement

## .center[Judgement]

* Any identity can request a judgement from a registrar

--

* The judgment issued by a registrar has only 6 possible values: 
  * Unknown (no opinion is held)
  * Reasonable (data appears to be reasonably acceptable
  * KnownGood 
  * OutOfDate
  * LowQuality
  * Erroneous

???

* Unknown: no opinion is held
* Reasonable: data appears to be reasonably acceptable in terms of its accuracy, however no in depth checks (such asin-person meetings or formal KYC) have been conducted.
* KnownGood : The target is known directly by the registrar and the registrar can fully attest to the data's accuracy.
* OutOfDate: The data was once good but is currently out of date. There is no malicious intent in the inaccuracy. Thisjudgement can be removed through updating the data.
* LowQuality: The data is imprecise or of sufficiently low-quality to be problematic. It is not indicative ofmalicious intent. This judgement can be removed through updating the data.
* Erroneous: The data is erroneous. This may be indicative of malicious intent. This cannot be removed except by theregistrar.

--

* If an identity modifies the value of one of its fields (or adds one), the judgments towards this identity disappear (except those which were `Erroneous`).

---

name: subidentities

## .center[Sub-identities]

* Each identity can define some sub-identities

--

* A sub-identity consists only of an address and a name (no other fields)

--

* For example, a given company that has multiple collators can create a sub-identity for each of its collators.

<div class="center">
  <div class="mermaid">
    graph TD
    B(CompanyName) -->|One| D[CompanyName/One]
    B -->|Two| E[CompanyName/Two]
  </div>
</div>

???

Each identity can define sub-identities, but each sub-identity consists only of a name and address (no other fields).

---

## .center[Thanks you for your attention]

Presentation made with [remark](https://github.com/gnab/remark).  

Graphs realized with [mermaid](https://github.com/knsv/mermaid).

Get the sources of this presentation on github :

.center[[https://github.com/librelois/slides-en](https://github.com/librelois/slides-en)]
