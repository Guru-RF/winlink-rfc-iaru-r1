# RFC: Proposal for a Coordinated 2 m Amateur Winlink / DWS (VARA FM) Data Channel for IARU Region 1

| | |
| --- | --- |
| **Draft version** | 0.1 |
| **Prepared by** | Joeri Van Dooren, ON6URE / RF.Guru |
| **Intended audience** | IARU Region 1 national societies and their VHF/UHF managers, the IARU R1 VHF/UHF/Microwaves Committee (C5), repeater and unmanned-station coordinators, and the amateur emergency-communication groups (in Belgium B-EARS, in the Netherlands DARES) |
| **Status** | Request for comments |
| **Comment period** | 60 days from publication of this draft (via [GitHub Issues](https://github.com/Guru-RF/winlink-rfc-iaru-r1/issues)), to allow circulation to IARU Region 1 national societies and their VHF managers |

---

## 1. Purpose of this RFC

This document proposes the coordinated use of a single dedicated 2 m amateur-radio frequency — **144.850 MHz** — for unmanned Winlink / **DWS (Dutch Winlink System)** digital gateway and digipeater stations across IARU Region 1 (Europe). It began as a Belgian proposal (a coordination request from the RST club in Sint-Truiden to the UBA unmanned-station coordination, around the case of ON0BAF) and has been broadened to a Region-1 scope, because emergency and cross-border digital messaging is inherently border-crossing: a channel that stops at a national boundary cannot serve a European Winlink network shared between neighbouring emergency-communication groups.

The goal is to obtain broad technical and organisational backing — from national societies and, ultimately, the IARU Region 1 VHF/UHF/Microwaves Committee (C5) — for **harmonising the unmanned Winlink / DWS 2 m channel on the frequency that has already become the de-facto standard in the Netherlands and that is already in coordinated use in Belgium**, so that the network remains compatible with the existing 2 m band plan and so that a single channel can be used by amateurs and their emergency-communication services on both sides of a border without re-tuning.

This is not a request to invent a new mode or a new band segment. Unlike a spread-spectrum experiment, a Winlink / DWS station transmits an **ordinary narrow-band FM signal** (audio from the Winlink/VARA FM software fed into a standard FM transceiver — see [Section 3](#3-how-winlink-vara-fm-and-dws-work-on-the-air)); it already belongs in the 2 m digital-communications segment. What is missing is *coordination*: agreeing on one common frequency (as APRS long ago agreed on 144.800 MHz), and a **simplified unmanned-station coordination procedure** for these stations, analogous to the one that already exists for APRS (see [Section 10](#10-licensing-and-unmanned-station-status) and [Section 13](#13-coordination-proposal)).

---

## 2. Background

**Winlink** ("Winlink Global Radio Email") is a worldwide radio email and message system, built and operated by licensed radio amateurs (and some authorised government stations), that delivers email over radio where the internet is not available. On VHF/UHF its gateway stations — **RMS (Radio Message Server)** stations — are normally unattended, automatically-controlled stations that relay a client's traffic into the wider network. Winlink is one of the most widely used digital transports for amateur **emergency communications** worldwide.

**VARA FM** is a software (sound-card) modem that carries Winlink traffic over an ordinary FM voice channel far faster than classic packet radio (see [Section 3.2](#32-vara-fm--audio-into-an-ordinary-fm-radio-not-a-new-mode)). It is the mode toward which Winlink VHF activity has been moving, because it is roughly ten to twenty times faster than 1200-baud AX.25 packet while still fitting a standard FM channel.

**DWS (Dutch Winlink System)** is a package of Winlink software plus a station configuration, developed in the Netherlands by Chris PA7RHM, Jan PH3J and Hans PA3GJM, that turns a standard Winlink Express station into an unmanned RMS gateway and/or **digipeater**. Its authors describe it as *"a robust EmComm solution for exchanging email messages over radio for emergency-communication teams."* DWS keeps digipeat mode active for **both** AX.25 packet **and** VARA FM on a single frequency with one sound-modem, and its relay/self-mapping topology is, in its own words, *"based on APRS."* In the context of emergency communications — **B-EARS** (Belgium Emergency Amateur Radio Service, part of the national society **UBA**) and **DARES** (Dutch Amateur Radio Emergency Service, in the Netherlands, whose national society is **VERON**) — DWS is growing quickly into a de-facto standard for reliable amateur data messaging, run as a joint cross-border effort (the shared DWS documentation is hosted under the Belgian UBA, and a monthly NL/BE Winlink exercise already runs on these frequencies).

### 2.1 The Belgian case (ON0BAF)

The proposal that seeded this RFC concerns the Belgian unmanned station **ON0BAF**, which is already documented as a DWS RMS installation. Today ON0BAF beacons and carries DWS data on the 2 m **APRS** frequency (144.800 MHz), and on 70 cm it uses 439.850 MHz (its second 70 cm data registration, 430.850 MHz, is currently unused). While this works technically, it is not operationally ideal: APRS is an AX.25 network, whereas DWS is moving toward VARA FM, and — crucially — **VARA FM does not sense an AX.25 packet transmission and will key over it** (see [Section 8](#8-why-not-simply-stay-on-the-aprs-frequency-144800-mhz)). A DWS station therefore needs its **own** coordinated channel, separate from 144.800 MHz APRS.

### 2.2 Why one common frequency, and why cross-border

Because DWS uses **single-frequency digipeating** (every participating station receives and re-transmits on the same channel, like APRS), the stations that are meant to form one contiguous relay network must operate on **exactly the same frequency**. A station on a different frequency simply cannot participate. This is the same reason APRS harmonised on one channel decades ago. For an emergency-communication network that is expected to keep working across the Belgium–Netherlands border, that common frequency should be the same on both sides — which is why this is proposed as a Region-1 coordination item, not a purely national one.

---

## 3. How Winlink, VARA FM and DWS work on the air

This section is a short primer for band-plan readers and coordinators who may know FM voice and APRS well, but not the Winlink data ecosystem. The key point for band planning is that **none of this is a new RF mode**: on the air it is ordinary narrow-band FM.

### 3.1 What Winlink is

Winlink is a store-and-forward email system carried over radio. A client station connects (over RF) to an **RMS gateway**; the gateway passes the traffic to/from the Winlink network. RMS gateways are typically **unattended, automatically-controlled stations**: the transceiver and modem are computer-controlled, the station answers only when it is called, and — following the amateur automatic-control model — it transmits only after it has sensed the channel clear. On VHF/UHF, an RMS gateway can serve **both** AX.25 packet **and** VARA FM clients.

Winlink amateur traffic is **not encrypted**. Message bodies are carried in the open, publicly documented **B2F** compressed binary format (LZHUF-based). Compression is not encryption: the format is public, so the content is observable and legal on the amateur bands. (Winlink is technically capable of AES-256 encryption, but that is used only on non-amateur services — SHARES / MARS / government — where encryption is permitted; amateur-band traffic stays open, as amateur rules require.)

### 3.2 VARA FM — audio into an ordinary FM radio, not a new mode

**VARA FM** is a proprietary, closed-source sound-card software modem (by José Alberto Nieto Ros, EA5HVK). It is an **OFDM multi-carrier** modem with adaptive modulation (from 4PSK up to 256QAM), which scales its speed to the signal quality. Critically, VARA FM does **not** produce a new kind of RF emission: it generates *audio* that is fed into an ordinary narrow-band FM transceiver through the microphone or data-port path. **On the air, the result is a standard FM channel** — which is exactly why it slots into the existing 12.5 kHz FM channelisation and why the Belgian registration for a VARA FM station on 144.850 MHz carries the ordinary FM telephony-type emission designator **`12K0F3E`** (12.0 kHz occupied bandwidth, F = frequency modulation, telephony-type). No new modulation, no new segment — only a coordinated FM channel.

VARA FM has two interoperable profiles:

- **NARROW** — uses the radio's normal microphone/speaker audio path (≈ 3 kHz audio). It **fits a standard 12.5 kHz FM channel** and reaches roughly **13 kbps**. This is the profile appropriate to a 12.5 kHz 2 m channel.
- **WIDE** — uses the radio's flat, wideband 9600-baud data port (≈ 6 kHz audio) and reaches up to roughly **25 kbps**. WIDE is normally associated with wider (≈ 20–25 kHz) channels and is **not** what this RFC proposes for the 12.5 kHz 144.850 MHz channel.

For reference, either profile is on the order of **10–20× faster than classic 1200-baud AX.25 packet**, with stronger forward error correction and rate adaptation. (The free version of VARA is throttled to ≈ 566 bps; full speed and digipeater use require a paid licence.) Its proprietary, closed, licensed nature is weighed as a strategic consideration in [Section 14](#14-software-openness-and-a-path-to-an-open-modem).

### 3.3 AX.25 packet, and why DWS carries both modes

Classic amateur packet radio uses **AX.25** — commonly 1200-baud AFSK on 2 m — the same family of protocol that APRS uses. It is slow but extremely robust. DWS deliberately keeps AX.25 packet as the **mandatory, robust baseline** on every setup (the first connection is made over AX.25), while promoting **VARA FM as the higher-throughput preferred mode** for moving messages and files. So DWS is a *shift toward* VARA FM, not an overnight replacement of packet: both live on the one channel.

One consequence matters for band planning: **VARA FM and AX.25 do not cooperate as channel-sharing peers unless they are coordinated together.** VARA FM does not detect an in-progress packet transmission and will transmit over it. DWS resolves this by running both modes through **one** sound-modem with coordinated digipeat logic on **one** channel — which is precisely why that channel must be a dedicated, coordinated frequency and not shared with an unrelated network such as APRS on 144.800 MHz.

### 3.4 What a DWS "digipeater" actually is

Unlike an FM voice repeater, a DWS relay is **not** a split input/output pair. It is a **digipeater**: it receives and re-transmits on the **same** frequency (simplex, store-and-forward). Every DWS user station is itself a digipeater, so a client that cannot reach a distant RMS directly can still reach it via one hop through another user — the network maps and relays itself, exactly like APRS on its shared channel. DWS keeps this digipeat mode active for both AX.25 and VARA FM (its default role SSID **-12**), and at RMS sites a **crossband** digipeater (SSID **-11**) can bridge to another band. RMS gateway stations use SSID **-10**.

Because a digipeater is single-frequency simplex, a 144.850 MHz DWS channel needs **no input/output pair** and consumes only **one 12.5 kHz channel** — and it does not touch the 2 m FM repeater-input sub-band (which begins higher up, see [Section 6](#6-compatibility-with-existing-2-m-usage)).

### 3.5 Why a single shared frequency works

A Winlink/DWS channel is a **shared, polite, low-duty-cycle data channel**, not a continuous carrier:

1. **Automatic control senses the channel.** An RMS gateway transmits only after being called and after sensing the frequency clear.
2. **Traffic is bursty and infrequent.** Email/message exchanges and 30-minute-ish status beacons are short; the channel is idle most of the time.
3. **FM capture effect.** When two FM signals overlap, the stronger is captured and decoded — a collision is often not a total loss.
4. **VARA FM adapts and retries.** Rate adaptation and FEC let a VARA FM link back off to a slower, more robust speed rather than fail outright.

This is not collision-free — heavy simultaneous traffic on one channel can still congest — which is exactly why power, siting, node density and coordination matter (see [Section 9](#9-power-proposal)) and why a dedicated channel, separate from APRS, is preferable to piling DWS traffic onto 144.800 MHz.

---

## 4. Proposed operating concept

The proposed system is a European (IARU Region 1) amateur **Winlink / DWS** digital-messaging layer on the 2 m band, built from unmanned RMS gateways and digipeaters sharing one coordinated FM channel.

**The intended use cases are:**

- amateur email and message handling over radio (Winlink);
- **emergency and cross-border communication** for B-EARS, DARES and equivalent national services;
- store-and-forward digipeated coverage where direct paths are marginal;
- network-resilience and interoperability exercises;
- a robust, internet-independent fallback for message traffic.

**The system is *not* intended as:**

- a replacement for commercial or emergency-service networks;
- a general public messaging system;
- encrypted or private communication (amateur Winlink is compressed, not encrypted);
- a high-power, high-duty-cycle wide-area data network;
- a new modulation or a claim on a new band segment — it is ordinary FM in the existing digital segment.

---

## 5. Proposed frequency and on-air mode

The proposed primary channel is:

> **144.850 MHz** (12.5 kHz FM raster)

This is the frequency that has already become the de-facto standard 2 m Winlink channel for DWS/DARES in the Netherlands, and it is already in coordinated use in Belgium (see [Section 7](#7-why-144850-mhz-frequency-selection-rationale) and [Section 13.2](#132-existing-stations-and-initial-test-bed)). It sits inside the IARU Region 1 2 m **MGM / Digital-Communications** segment (144.794–144.9625 MHz, 12 kHz maximum bandwidth), where unmanned digital stations belong.

### 5.1 On-air settings (the coordinated channel)

All participating stations use the same channel so they can hear and relay one another. The proposed profile matches DWS practice on a 12.5 kHz FM channel:

| Parameter | Value |
| --- | --- |
| Modes on the channel | **Winlink** over **AX.25 packet** (1200-baud AFSK, robust baseline) **and VARA FM (NARROW)** (preferred, higher throughput) |
| Station software | Winlink Express + **DWS (Dutch Winlink System)** package |
| Role / topology | Single-frequency **digipeating** (store-and-forward); RMS gateways (SSID -10), digipeaters (SSID -12), crossband bridges at RMS sites (SSID -11) |
| Centre frequency | **144.850 MHz** |
| Channel raster | **12.5 kHz** FM |
| On-air emission | Ordinary narrow-band FM — e.g. **`12K0F3E`** (VARA FM), **`12K0F2D`**-class (AX.25 packet) |
| VARA FM profile | **NARROW** (fits the 12.5 kHz channel, ≈ 13 kbps). WIDE (≈ 25 kbps) needs a wider coordinated channel and is **out of scope** for this 12.5 kHz channel |
| Throughput | AX.25 1200-baud baseline; VARA FM narrow ≈ 13 kbps (≈ 10–20× packet) |
| Content | Ham-only; **no encryption** (Winlink B2F compression only); callsign identification |

Because the on-air signal is ordinary narrow-band FM — occupying a standard 12.5 kHz channel, with an *occupied* bandwidth within the segment's 12 kHz maximum — a 144.850 MHz DWS channel is **fully conformant**, and there is no channel-width problem to resolve. (The 12.5 kHz figure is the channel *raster*/spacing; the segment's 12 kHz limit is on *occupied* bandwidth, which is why the VARA FM emission is designated `12K0F3E` = 12.0 kHz.)

---

## 6. Compatibility with existing 2 m usage

The 144.850 MHz channel sits in the IARU Region 1 2 m **MGM / Digital-Communications** segment, **144.794–144.9625 MHz** (12 kHz maximum bandwidth). Its neighbours are handled explicitly:

- **APRS on 144.800 MHz** sits **50 kHz below**, in the very same digital segment. DWS is deliberately kept **off** 144.800 (see [Section 8](#8-why-not-simply-stay-on-the-aprs-frequency-144800-mhz)). Co-siting a 144.850 station with a 144.800 APRS digipeater is routine in practice — both are intermittent, modest-power data stations, often the same operator and rarely keying at once — though at only 50 kHz the real co-site consideration is transmitter noise and receiver desense, not channel selectivity (see [Section 11.1](#111-co-siting-at-existing-sites)).
- **"DV internet voice gateway" spot frequencies.** In the current IARU R1 plan, 144.8125 / 144.8250 / 144.8375 / **144.8500** / 144.8625 MHz carry the usage annotation *"DV internet voice gateway."* This RFC is candid about that (see [Section 7](#7-why-144850-mhz-frequency-selection-rationale)): DWS/Winlink use of 144.850 is a national **community convention within the digital segment**, not a band-plan-designated Winlink channel — which is exactly why a coordination request is appropriate, and why a **per-country check** for any live DV/voice-gateway use of 144.850 is part of the plan ([Section 13](#13-coordination-proposal)).
- **2 m FM repeater inputs begin at 144.975 MHz** ("Repeater input exclusive," 144.975–145.194 MHz). The channel is **125 kHz below** the lowest repeater input, so it does **not** fall on any 2 m repeater input.
- **The amateur-satellite sub-band (145.800–146.000 MHz)** is far above 144.850 MHz and is not affected. (The 144–146 MHz band is allocated to the amateur *and* amateur-satellite services jointly; the satellite activity lives at the top of the band.)

This proposal therefore aims to avoid:

- direct overlap with APRS (144.800) and with the 2 m repeater-input sub-band (≥ 144.975);
- any unmanaged collision between VARA FM and AX.25 by keeping both under one coordinated DWS channel;
- deployment on top of a live DV/voice-gateway installation on 144.850 in any country (hence the per-country check).

---

## 7. Why 144.850 MHz (frequency selection rationale)

**It is already the standard, and already coordinated.** 144.850 MHz is the primary de-facto 2 m Winlink frequency for DWS/DARES in the Netherlands (the DWS documentation names 144.850 first, alongside a second 2 m frequency 144.825 MHz and a UHF frequency 430.9875 MHz). In Belgium, **ON0AND is already a licensed, coordinated unmanned station on 144.850 MHz registered as "Packet Radio + VARA FM"** (50 W, omnidirectional, 8.5 dBd, emission `12K0F3E`), and **ON0BAF** is documented as a DWS RMS installation. Harmonising on 144.850 codifies what is already happening on both sides of the border rather than imposing a new frequency.

**It is in the right segment, region-wide.** 144.850 MHz sits inside the IARU R1 2 m **MGM / Digital-Communications** segment (144.794–144.9625 MHz, 12 kHz max), the part of the band intended for machine-generated / digital modes and unmanned digital stations — the correct home for an unmanned data gateway/digipeater. And because the on-air signal is a standard 12.5 kHz FM emission, the mode is fully conformant with the segment's 12 kHz maximum.

**It is legally available to amateurs across Region 1.** The 144–146 MHz band is allocated to the amateur and amateur-satellite services on a **primary** basis across all three ITU Regions and is effectively **exclusive** — no non-amateur service holds a primary allocation, and its only footnote (5.216) merely adds a secondary aeronautical-mobile allocation in China. No Region-1 country is excluded from amateur use of 144–146 MHz. This is a materially cleaner starting point than, for example, the 70 cm band, where in Region 1 the amateur service is only **secondary** to radiolocation and footnotes 5.274 (Denmark, Norway, Sweden) and 5.275 (Croatia, Estonia, Finland and others) give parts of 430–432 / 438–440 MHz to fixed/mobile services in specific countries.

**The honest caveats, and how they are handled.**

- *It is a community convention, not (yet) a band-plan designation.* The plan's current spot annotation for 144.8500 MHz is *"DV internet voice gateway."* DWS/Winlink use is a de-facto DARES/B-EARS convention within the digital segment. This RFC therefore asks IARU R1 (and each national society) to **recognise and coordinate 144.850 MHz as the 2 m channel for unmanned Winlink / DWS (packet + VARA FM) stations**, and to confirm before deployment that no live DV/voice-gateway installation already occupies 144.850 MHz nationally (a per-country check, [Section 13](#13-coordination-proposal)).
- *ITU allocation is not the same as authorised unmanned use.* The ITU allocation makes 144.850 MHz **available** to amateurs region-wide, but whether an **unmanned/automatic** station may operate there is governed by each country's **national band plan and licence conditions**. Some administrations restrict which frequencies an automatic station may use. That national step is explicit in the coordination proposal.
- *It is not a single nationwide channel the way APRS is.* DWS in practice spans more than one frequency (144.850 and 144.825 on 2 m, plus 430.9875 on UHF) and uses crossband bridging at some RMS sites. The APRS parallel is to the **shared-channel, single-frequency-relay principle** — not a claim that one frequency serves every purpose. This RFC harmonises the **primary 2 m channel** (144.850) and defers 70 cm to a later phase ([Section 12.2](#122-70-cm-harmonisation--a-later-phase)).

---

## 8. Why not simply stay on the APRS frequency (144.800 MHz)?

The Belgian case (ON0BAF) currently rides on 144.800 MHz APRS. That the technique works there does not make it the right long-term home:

1. **Different network, different protocol.** 144.800 MHz is the coordinated **APRS** channel — an AX.25 position/telemetry network with its own users and its own coordination. DWS is a separate message-handling network moving toward VARA FM.
2. **VARA FM would key over APRS.** VARA FM does not sense an in-progress AX.25 packet and will transmit over it. Running DWS VARA FM on the APRS channel would make DWS a disproportionate interferer to the dense, nationally-coordinated population of unmanned APRS stations that already shares 144.800 MHz.
3. **Coordination clarity.** A dedicated 144.850 MHz channel keeps the two networks — and their coordination, registration and troubleshooting — cleanly separated, exactly as APRS itself was once separated out onto its own channel.

A dedicated channel, 50 kHz away in the same digital segment, is the clean solution — and it is the frequency the Netherlands already uses.

---

## 9. Power proposal

The RF-power policy is intentionally conservative. On a **shared, single-frequency, digipeated** channel, excessive power from any one station raises the noise floor for everyone, worsens the hidden-transmitter problem, and desensitises co-sited receivers — while adding little to a network whose coverage comes mostly from good siting and antenna height.

### 9.1 Normal recommended output power

> **A modest ERP — of the order of a few watts to ~25 W to a modest omni** — sufficient for reliable digipeated coverage from a good site.

Existing coordinated stations bracket this range (Belgian APRS/data unmanned stations run from ~2 W to ~50 W; ON0AND runs 50 W on 144.850 MHz). The exact recommended figure is posed as an open question ([Section 17](#17-open-questions-for-comments)), to be agreed in coordination; the **principle** matters more than the number.

### 9.2 ERP / EIRP consideration

Because antenna gain varies widely between sites, the network should not focus only on transmitter-module power. Every fixed station should document at least:

- conducted RF output power;
- antenna gain and type (omni/directional);
- feedline loss;
- estimated ERP;
- antenna height and site locator;
- responsible callsign / contact.

A modest omni (≈ 0 dBd) from a tall mast is often the better default for a digipeater — it fills local and valley coverage and keeps ERP modest — with higher gain justified only by a specific coverage need and its ERP documented.

### 9.3 Recommended principle

> **Use the lowest power that provides reliable coverage.**

The network should be engineered as a coordinated amateur data network, not a maximum-power contest between digipeaters on a shared channel.

---

## 10. Licensing and unmanned-station status

A Winlink/DWS RMS gateway or digipeater that relays traffic automatically, without an operator present, is an **unmanned (automatically-controlled) amateur station** in the regulatory sense — not merely a station operated under a personal licence.

Key consequences:

1. **A personal amateur licence is not sufficient.** A personal licence authorises *you* to operate a station under your direct control. An unattended automatic RMS gateway or digipeater generally requires a separate **unmanned-station authorisation** from the national regulator (in Belgium, BIPT/IBPT) before it may operate.
2. **The channel is single-frequency and digipeated.** Every relaying node receives and re-transmits on the same coordinated frequency; there is no input/output pair as on an FM voice repeater (see [Section 3.4](#34-what-a-dws-digipeater-actually-is)).
3. **Register every unmanned node.** Each authorised RMS gateway / digipeater and its responsible operator should be registered nationally, so the node list stays coordinated (see [Section 13](#13-coordination-proposal)).
4. **Attended portable/handheld Winlink stations** operated under the direct control of a licensed amateur are not unmanned stations and fall under the normal personal licence. A portable station configured to relay automatically, however, takes on digipeater behaviour and should be treated accordingly.

### 10.1 A simplified coordination procedure — analogous to APRS

Because these stations all share **one** coordinated frequency and are functionally uniform (an FM channel, a documented emission, an unmanned data role), they do not need the case-by-case, pair-by-pair coordination of duplex voice repeaters. This RFC proposes that national societies and regulators introduce — or extend — a **simplified, lightweight coordination procedure for unmanned Winlink / DWS stations, modelled on the existing procedure for APRS unmanned stations**: a common frequency, a standard set of technical parameters to declare, and a national register. This lowers the barrier to bringing a compliant station on the air while keeping the network coordinated and visible.

---

## 11. Technical requirements for participating stations

Participating fixed RMS gateway / digipeater stations should meet the following minimum expectations:

1. A valid unmanned-station authorisation for the node (see [Section 10](#10-licensing-and-unmanned-station-status)).
2. Operation on the coordinated frequency (144.850 MHz) with the agreed 12.5 kHz FM raster.
3. Callsign identification according to amateur-radio requirements (DWS SSID conventions: -10 RMS, -11 crossband digi, -12 digi).
4. No encryption of amateur traffic (Winlink B2F compression only).
5. Automatic control that senses the channel clear before transmitting.
6. Clean transmitter spectrum; no overdriven RF stages; correct FM deviation for the data audio.
7. Suitable filtering where needed, especially at shared sites.
8. Stable frequency reference appropriate for narrow-band FM.
9. Documented antenna, power, ERP, location and responsible operator (see [Section 9.2](#92-erp--eirp-consideration)).
10. Remote shutdown capability for unattended stations where practical.
11. Willingness to reduce power or change configuration if interference is reported.
12. Registration of the node and its responsible operator with the relevant national coordination (see [Section 13](#13-coordination-proposal)).

### 11.1 Co-siting at existing sites

A 144.850 MHz digipeater is often installed at a site that already hosts other unmanned stations — very commonly a 144.800 MHz APRS digipeater, and sometimes a 2 m FM voice repeater whose input is ≥ 144.975 MHz. Two neighbours matter:

- **A co-sited 144.800 MHz APRS station (50 kHz away).** At only 50 kHz the real co-site issue is the digipeater's transmitter broadband noise into — and blocking/desensitisation of — the co-located receiver, *not* receiver channel selectivity: a strong local carrier 50 kHz away can desense a nearby receiver whatever its adjacent-channel selectivity figure. In practice this pair co-sites easily because both are intermittent, modest-power data stations that rarely key simultaneously (often the same operator); with a clean transmitter, vertical antenna separation, and — where simultaneous transmit/receive is genuinely required — a **band-reject (notch) cavity tuned to the neighbour's frequency** (or a pass-reject duplexer), it is generally straightforward. Two intermittent, modest-power data stations co-site far more easily than two high-power duplex voice repeaters.
- **A co-sited 2 m FM repeater input (≥ 144.975 MHz, i.e. ≥ 125 kHz away).** The digipeater's transmitter noise must not fall on the repeater's receive frequency: clean the signal at the source (a band-pass cavity on the digipeater TX to suppress wideband noise, a PA that is not overdriven, and — if needed — a band-reject notch at the repeater's receive frequency), keep power modest, and use antenna separation. At ≥ 125 kHz the filter skirts have room to work.

Every co-located installation should document its co-siting arrangement (antenna separation, TX filtering) alongside the technical parameters in [Section 9.2](#92-erp--eirp-consideration). And, as always on a shared channel, **turning the power down is often the simplest and most effective fix** — it reduces both blocking and transmitter noise into a neighbour by the same amount, and a digipeater on a good mast can usually afford it.

---

## 12. Proposed frequency plan

Initial proposal:

| Use | Frequency | Raster | Notes |
| --- | --- | --- | --- |
| Primary Region-1 2 m unmanned Winlink / DWS channel | **144.850 MHz** | 12.5 kHz FM | In the 144.794–144.9625 MHz MGM/Digital segment (12 kHz max); already the NL DWS standard and in coordinated BE use |
| Secondary 2 m Winlink / DWS frequency (as used in NL) | 144.825 MHz | 12.5 kHz FM | Co-listed DWS standard; noted for awareness, not the harmonisation target |
| 70 cm harmonisation | **to be determined (later phase)** | — | See [Section 12.2](#122-70-cm-harmonisation--a-later-phase) |

**Segments to respect across the 2 m band (IARU R1):**

| Range / frequency | Reason |
| --- | --- |
| 144.000–144.794 MHz | CW/EME, SSB, beacons, and the lower "All mode" segment (144.500–144.794, 20 kHz) — not for an unmanned digital channel |
| 144.800 MHz | APRS — keep DWS off this channel (see [Section 8](#8-why-not-simply-stay-on-the-aprs-frequency-144800-mhz)) |
| 144.794–144.9625 MHz | MGM / Digital-Communications segment (12 kHz max) — **this is where 144.850 belongs** |
| 144.975–145.194 MHz | 2 m FM repeater inputs ("Repeater input exclusive") — do not encroach |
| 145.200–145.794 MHz | FM/DV simplex and repeater outputs |
| 145.800–146.000 MHz | Amateur-satellite sub-band — keep clear |

### 12.1 Frequency-selection rationale (summary)

144.850 MHz is chosen because it is (a) already the de-facto NL standard and already coordinated in Belgium; (b) inside the correct 2 m digital segment, region-wide, with the mode fully conformant to the 12 kHz maximum; and (c) legally available to amateurs across Region 1 on a primary (and effectively exclusive) basis. Its one soft spot — that the plan currently annotates the spot as *"DV internet voice gateway"* rather than Winlink/packet — is handled by asking IARU R1 and national societies to **coordinate** the frequency for this use and to run a per-country check for any live DV/voice-gateway occupancy. See [Section 7](#7-why-144850-mhz-frequency-selection-rationale) for the full argument and caveats.

### 12.2 70 cm harmonisation — a later phase

The Belgian proposal explicitly defers 70 cm to a later phase, and this RFC follows suit. The relevant inputs to that future decision are already on the table: **ON0BAF holds 70 cm digital-data registrations on 439.850 MHz (in use) and 430.850 MHz (currently unused)**, while the NL DWS standard UHF frequency is **430.9875 MHz**. A harmonised 70 cm channel — analogous to what this RFC proposes on 2 m — should be agreed **after** the 2 m channel is settled, using the same coordination route. No 70 cm frequency is fixed by this draft.

---

## 13. Coordination proposal

This RFC proposes that IARU Region 1 national societies and repeater/unmanned-station coordinators agree on a common 2 m Winlink / DWS channel before wider deployment, and that the request be carried to the IARU Region 1 VHF/UHF/Microwaves Committee (C5). Coordination, registration and the known-node list are proposed to run **per country** — through each national society or its unmanned-station coordinator — keeping each country's node list, responsible-operator contacts and technical parameters in one authoritative, publicly visible place.

> **Initial consultation.** This draft grew out of a constructive Belgian coordination proposal from the RST club (Radio Elektronica club Sint-Truiden, secretary Walter ON4AWM) to the UBA unmanned-station coordination, forwarded by Rudy ON6VDS — offered, in the club's words, in the open and collaborative spirit long associated with the late Filip ON4PC. The re-scope to a Region-1 channel invites fresh consultation at European level, in the same spirit.

**Suggested coordination steps:**

1. Circulate this RFC among IARU Region 1 national societies (via their VHF/UHF managers) — for the network's current cross-border footprint the **UBA** (Belgium) and **VERON** (the Netherlands) in particular, whose national band-plan positions are what an IARU R1 coordination ultimately rests on — their repeater/technical coordinators, and the amateur emergency-communication groups (B-EARS, DARES and equivalents) — see the [IARU R1 VHF Managers Handbook](https://www.iaru-r1.org/wp-content/uploads/2024/11/VHF_Handbook_V10_02.pdf) and the [VHF/UHF/Microwaves Committee (C5)](https://www.iaru-r1.org/about-us/committees-and-working-groups/vhf-uhf-shf-committee-c5/).
2. Collect objections, local conflicts, and alternative proposals.
3. **Per-country check before deployment.** Confirm that no live DV/voice-gateway or other deployed station occupies 144.850 MHz nationally, and confirm that national unmanned-station rules permit an automatic station on this frequency (some administrations restrict automatic-station frequencies).
4. **Ask IARU R1 and national societies to recognise/coordinate 144.850 MHz** as the 2 m channel for unmanned Winlink / DWS (packet + VARA FM) stations — the single change that turns a de-facto convention into a coordinated channel — and to introduce a **simplified unmanned-station coordination procedure** for these stations, modelled on APRS ([Section 10.1](#101-a-simplified-coordination-procedure--analogous-to-aprs)).
5. Maintain a per-country list of known RMS gateways / digipeaters and responsible operators.
6. Start with modest-power deployments and monitor for interference.
7. Adjust power or configuration if interference or complaints arise.
8. Document the final recommendation and make it publicly available.
9. Where appropriate, use the coordinated position in communication with national regulators (in Belgium, BIPT/IBPT) and served emergency-management agencies.

### 13.1 Comment period and next steps

1. **Comment period — 60 days.** Comments, objections, and reports of national conflicts are invited for **60 days** from publication of this draft, via GitHub Issues (see [Section 16](#16-how-to-comment-and-contribute)) — a longer window than a purely national draft, to allow circulation to IARU Region 1 national societies and their VHF managers.
2. **Confirm/authorise test sites.** From the close of the comment period, participating countries can confirm existing stations and, where needed, apply for unmanned-station authorisations for additional RMS gateways / digipeaters on 144.850 MHz.
3. **Deploy and evaluate.** The network will be evaluated on how it performs in practice — coverage, interference, throughput and congestion behaviour, node density, and cross-border interoperability — and this RFC will be revised accordingly before any wider roll-out.

### 13.2 Existing stations and initial test-bed

The 2 m channel is not a green-field proposal — stations are already on it. In **Belgium**, the following are the natural starting point:

- **ON0AND** — already licensed and operating on **144.850 MHz** as "Packet Radio + VARA FM" (50 W, omni, 8.5 dBd, 75 m mast) — the existing reference station on the channel. Its parameters imply an estimated ERP on the order of ~350 W, which exceeds the modest-ERP default recommended in [Section 9](#9-power-proposal); as an already-coordinated station with an established coverage need it stands, with its ERP documented exactly as [Section 9.2](#92-erp--eirp-consideration) requires — but new deployments should follow the modest-ERP default rather than take ON0AND's power and gain as the model.
- **ON0BAF** — documented as a DWS RMS installation; the station whose coordination case seeded this proposal (to move its DWS activity off the 144.800 MHz APRS channel onto 144.850 MHz).

In the **Netherlands**, DWS/DARES already run multiple RMS gateways and digipeaters on 144.850 MHz (for example the DARES Midden-Nederland gateways and others), with a recurring joint NL/BE Winlink exercise on the channel. Exact node counts are not centrally published; the live DWS "RADAR" status map is the reference.

These existing stations, plus any additional coordinated nodes, form the initial cross-border test bed that will drive the evaluation in [Section 13.1](#131-comment-period-and-next-steps).

---

## 14. Software openness and a path to an open modem

The proposal above adopts VARA FM as the on-air data mode because it is what DWS uses today and what already works on 2 m. That is a deliberate, pragmatic, short-term choice — but it carries a strategic dependency an emergency-communication network should weigh openly: **VARA FM is proprietary, closed-source software with a per-user licence model, and its usual client (Winlink Express) is Windows-only.** For a network whose whole purpose is resilience, long-term dependence on closed binaries, single-vendor licences, and one operating system is itself a point of fragility.

This section records that concern and proposes a **two-track approach**: keep deploying what is practically available today (VARA FM), while investigating an open, auditable modem for the longer term. The frequency-coordination request in this RFC (144.850 MHz) is deliberately **separable from the modem question** — the coordinated channel is an ordinary FM channel, and the modem that rides on it can evolve without re-opening the frequency coordination.

### 14.1 What is already open

Much of an open station already exists and can be used now — the closed layer is narrower than it first appears:

- **Client.** **Pat** is a free, open-source Winlink client written in Go that runs on Linux, macOS and Windows (including Raspberry Pi). It replaces the Windows-only Winlink Express on the *client* side, so a small Raspberry Pi with Linux, an audio interface and a transceiver can serve as a field station. (Caveat: when Pat is used *with* VARA, VARA is still the closed *modem* layer — an open client alone does not make the on-air chain open.)
- **TNC.** A separate hardware TNC is no longer required. The TNC function runs entirely in software on a PC or Raspberry Pi; toward the transceiver one needs only an audio interface (USB audio from the radio, a SignaLink / DigiRig-class interface, or home-brew) plus PTT/CAT/VOX.

So the client and TNC layers can already be fully open and cross-platform. The one remaining closed layer is the **modem** itself.

### 14.2 Mercury — an open modem, and a possible fork base

**Mercury** (from the Rhizomatica / HERMES project) is a fully open-source (GPL-3.0, written in C), OFDM, ARQ-based modem for reliable email and file transfer. It deserves an honest assessment:

- **Today it is primarily an HF modem.** Its design point and its data rates sit in the HF range, not the VARA FM range. In principle a sound-card modem can run on any transceiver that passes the audio correctly — VHF FM included — but there is, as far as we can find today, **no ready-made VARA-FM-class VHF/FM implementation of Mercury with digipeating** of the kind DWS builds on VARA FM. So Mercury is **not** an immediate drop-in replacement for DWS / VARA FM on 2 m.
- **But it is open and forkable.** Precisely because it is open source, Mercury can be forked and extended. The interesting question is whether, building on the work already done, one could develop a **more wideband VHF/UHF variant that approaches VARA FM speeds on FM while remaining fully open, auditable, and free of any per-volunteer licence.** That is a development project, not a switch to flip — someone has to write, test and maintain the code. Guru-RF has now started exactly this fork as **MercuryFM** (see [Section 14.5](#145-mercuryfm--a-call-for-co-developers-and-testers)).

As far as we can see today, **no mature open-source modem plays the same role on FM as VARA FM**, with comparable speed and the same practical availability. Other open and older packet solutions exist, but they do not solve exactly the same problem. That is why Mercury, or a Mercury-derived open modem, is attractive as a *starting point*: not because it replaces VARA FM now, but because it could become the basis of an open VHF/UHF modem later.

### 14.3 Two hard constraints on any modem choice

- **Modems do not interoperate over the air.** A VARA modem cannot decode a Mercury signal, and vice-versa. A VARA-like TCP/TNC interface may let application software talk to a modem at the *application* level, but that is not RF compatibility. On a single-frequency digipeated network every station must use the **same on-air modem**, so any move from VARA FM to an open modem would be a **coordinated changeover** across the network — not a gradual mix of both on the one channel.
- **No encryption on the amateur channel — whatever the modem.** Independently of the modem (VARA, DWS, Mercury, Pat or anything else), encryption is **not** permitted on the ordinary amateur service in Belgium, and generally across the amateur bands. AES-128 or similar may sound useful for emergency traffic, but it is not allowed on amateur frequencies as a matter of course. Genuinely confidential traffic must go via another channel, or within an explicitly authorised crisis-management / regulator (BIPT/IBPT) framework — never as encryption on the amateur channel. (This restates, from the software angle, the no-encryption requirement in [Section 3.1](#31-what-winlink-is) and [Section 5.1](#51-on-air-settings-the-coordinated-channel).)

### 14.4 Openness over origin

The useful test is not where a tool comes from but whether it serves a resilient network. Winlink is not a European development; VARA is written by a Spanish amateur but is closed, licensed software; Mercury comes from the Rhizomatica / HERMES context and is open source. Geographic origin matters far less than whether a tool is **open, auditable, decodable, licence-free for volunteers, legally usable nationally, and maintainable by the community itself.**

### 14.5 MercuryFM — a call for co-developers and testers

To turn the open-modem track from an idea into working code, ON6URE / RF.Guru has started **MercuryFM**, an open fork of Mercury aimed specifically at VHF/UHF FM:

> <https://github.com/Guru-RF/MercuryFM>

**Where the idea comes from.** Mercury ([Section 14.2](#142-mercury--an-open-modem-and-a-possible-fork-base)) is an open, proven OFDM / ARQ modem, but its design point is HF and its data rates sit in the HF range. VARA FM, by contrast, reaches its speed by pushing a wide OFDM waveform through the audio path of an ordinary FM transceiver — but it is closed and licensed. **MercuryFM takes Mercury's open OFDM / ARQ foundation and adapts it for the flat audio path of an FM radio**, going more wideband so it can approach VARA FM's throughput on 2 m / 70 cm while staying **fully open, auditable and licence-free** — no closed binary, no per-volunteer licence, no Windows-only tooling. It is the concrete attempt at the open, VARA-FM-class modem this section argues the network will eventually need. It is early and openly experimental: it makes no claim to match VARA FM today — which is exactly why help is wanted.

**We are looking for co-developers and testers:**

- **Developers** with experience in **C / C++, DSP, SDR, OFDM / modem design, FEC, Linux, network programming or embedded systems** — to help shape the waveform, the ARQ layer, the FM audio interfacing, and the TNC / TCP integration.
- **Testers** with a 2 m / 70 cm FM station and a sound-card / USB-audio interface (SignaLink / DigiRig-class or home-brew) who can run on-air trials, log results and report back — over real paths and sites, including the 144.850 MHz DWS test-bed.

To contribute code, test on the air, or simply follow along, open an issue on the [MercuryFM repository](https://github.com/Guru-RF/MercuryFM), or reach out via [Section 16](#16-how-to-comment-and-contribute). Contributions from within B-EARS, DARES and the wider Region-1 community are especially welcome — an open emergency-communications modem is best built and owned by the community that depends on it.

---

## 15. Why a coordinated frequency helps regulators and served agencies

A dedicated and coordinated amateur channel for unmanned Winlink / DWS stations helps prevent future friction and strengthens the emergency-communication case:

- it keeps the DWS network **off** the APRS channel and out of unmanaged co-channel conflict;
- it shows amateurs **respecting and openly coordinating** the 2 m band plan (asking to recognise the frequency rather than simply occupying it);
- it keeps the network **ham-only and non-encrypted**, with documented technical parameters and a public node list;
- it gives B-EARS, DARES and their served agencies **one predictable, harmonised, cross-border channel** to plan around — the property an emergency network most needs;
- it lets national regulators see a coordinated, registered, lightweight-to-authorise class of unmanned station rather than ad-hoc deployments.

This is a proactive coordination effort, not a reaction to a problem.

---

## 16. How to comment and contribute

This RFC is maintained as a living document on GitHub:

> <https://github.com/Guru-RF/winlink-rfc-iaru-r1>

There are two ways to take part. You do **not** need to be a software developer for either.

### 16.1 Comments and objections — open an Issue

For comments, questions, objections, or local frequency conflicts, open a **GitHub Issue**:

> <https://github.com/Guru-RF/winlink-rfc-iaru-r1/issues>

An Issue is simply a public discussion thread attached to the document. Click "New issue," type your point in plain language (English, please — see below), and submit. The maintainer and other contributors can then reply and discuss. This is the easiest route and requires only a free GitHub account.

### 16.2 Proposing concrete text changes — Issue or Pull Request

Specific wording changes can be proposed in either of two ways:

- **The easy way:** open an Issue (as above) describing the change you want, and the maintainer will edit the document for you.
- **The direct way:** submit a **Pull Request (PR)**.

**What is a Pull Request?** A PR is GitHub's mechanism for proposing an exact edit to a document. You make your own copy of the file (a "fork" or branch), change the text there, and open a PR. The PR shows your proposed change side-by-side against the current text as a **diff** — added lines in green, removed lines in red — so everyone can see precisely what you are suggesting. The maintainer can review it, discuss it, and finally **merge** (accept) or decline it. Nothing in the official document changes until a PR is merged, so it is a safe, transparent, fully reviewable way to suggest concrete wording. GitHub lets you do all of this in the browser, with no special software installed.

If GitHub is unfamiliar to you, do not let that stop you: send your comment by your usual channel to ON6URE / RF.Guru and it will be entered into the tracker on your behalf.

### 16.3 Language

Please keep Issues and Pull Requests in **English**, so the discussion stays accessible across Region 1 language communities and to any IARU / national-regulator readers who later review the record.

---

## 17. Open questions for comments

Feedback is requested on the following points:

1. Is **144.850 MHz** acceptable as the harmonised Region-1 2 m channel for unmanned Winlink / DWS (packet + VARA FM) stations?
2. Should IARU R1 be asked to **recognise/coordinate** 144.850 MHz for this use within the MGM/Digital-Communications segment, given that its current spot annotation is "DV internet voice gateway"?
3. Are there national conflicts at 144.850 MHz (e.g. live DV/voice-gateway installations), and does your administration permit an **unmanned/automatic** station there?
4. Is a **simplified, APRS-style coordination procedure** for unmanned Winlink / DWS stations supported in your country?
5. What should the **recommended** and **maximum** conducted RF output (and ERP) be for these stations?
6. Should the channel profile be **VARA FM NARROW + AX.25 packet** (as proposed for 12.5 kHz), or is there a case for a wider coordinated channel for VARA FM WIDE elsewhere?
7. Should the **secondary NL frequency 144.825 MHz** be part of any harmonisation, or left as a national matter?
8. Should fixed RMS gateways / digipeaters be **registered** through each national society / unmanned-station coordinator?
9. When should the **70 cm harmonisation** ([Section 12.2](#122-70-cm-harmonisation--a-later-phase)) be taken up, and around which frequency (e.g. the NL 430.9875 MHz, or ON0BAF's 439.850 / 430.850 MHz)?
10. Should a small technical working group be created to maintain the frequency and node list, jointly with the emergency-communication groups (B-EARS, DARES)?
11. Should the network pursue a parallel **open-modem track** — for example a Mercury-derived (HERMES / Rhizomatica) open VHF/UHF modem — alongside VARA FM, so it is not tied long-term to closed binaries, Windows-only tooling, or per-volunteer licences (see [Section 14](#14-software-openness-and-a-path-to-an-open-modem))?
12. Are there developers and testers — within B-EARS, DARES or the wider Region-1 community — willing to help build and on-air-test the **MercuryFM** open-modem project ([Section 14.5](#145-mercuryfm--a-call-for-co-developers-and-testers))?

---

## 18. Proposed conclusion

The proposed starting point is:

- **144.850 MHz** as the harmonised Region-1 2 m channel for unmanned Winlink / DWS stations, on a **12.5 kHz FM** raster
- Channel carrying **AX.25 packet (1200-baud, robust baseline)** and **VARA FM NARROW (preferred, ≈ 13 kbps)**, DWS single-frequency **digipeating**
- Ordinary narrow-band FM on the air (e.g. `12K0F3E`) — no new mode, fully conformant with the segment's 12 kHz maximum
- Ham-only use; **no encryption** (Winlink B2F compression only); callsign identification
- Every fixed RMS gateway / digipeater licensed as an **unmanned station**; all nodes sharing the one coordinated frequency
- A **simplified, APRS-style coordination procedure** for these unmanned stations, with a per-country register
- A coordination request to IARU R1 to **recognise/coordinate 144.850 MHz** for this use, plus a per-country check for any live DV/voice-gateway occupancy
- **70 cm harmonisation deferred** to a later phase
- **VARA FM adopted now for pragmatism, with a parallel open-modem track** — the **MercuryFM** fork of Mercury / HERMES ([Section 14.5](#145-mercuryfm--a-call-for-co-developers-and-testers)), plus open tooling such as Pat — pursued for the long term, so the network is not permanently tied to closed binaries, Windows-only tooling, or per-volunteer licences (see [Section 14](#14-software-openness-and-a-path-to-an-open-modem))

This approach gives radio amateurs and their emergency-communication services across Region 1 a coordinated, technically defensible, cross-border channel for Winlink / DWS messaging on a single harmonised 2 m frequency — codifying the standard the Netherlands already uses and Belgium already coordinates, cleanly separated from the APRS channel, and squarely inside the existing 2 m digital segment.

---

## 19. References

- **IARU Region 1 VHF band plan (incl. 144–146 MHz / 2 m)** — segment 144.794–144.9625 MHz "MGM / Digital Communications," 12 kHz max; 144.800 APRS; repeater inputs from 144.975 MHz
  <https://www.iaru-r1.org/reference/band-plans/>
  Direct VHF band plan (eff. Dec 2020): <https://www.iaru-r1.org/wp-content/uploads/2020/12/VHF-Bandplan.pdf>
- **RSGB 144 MHz band plan** (R1 implementation, corroborating segment boundaries and repeater-input start)
  <https://rsgb.org/main/operating/band-plans/vhf-uhf/144mhz-band/>
- **ITU Radio Regulations — 144–146 MHz allocation and footnote 5.216; 70 cm footnotes 5.274 / 5.275**
  <https://life.itu.int/radioclub/rr/vhfband.htm> · <https://life.itu.int/radioclub/rr/arsfoot.htm>
- **Winlink Global Radio Email — project, RMS gateway (unmanned) operation, VHF modes, WL2K FAQ (compression, not encryption)**
  <https://winlink.org/> · <https://winlink.org/content/rms_packet> · <https://winlink.org/sites/default/files/download/wl2k_faq_20230311.pdf>
- **VARA FM — the modem (EA5HVK / Ros Modem)** — proprietary, closed-source, licensed
  <https://rosmodem.wordpress.com/>
- **Mercury — open-source (GPL-3.0) OFDM / ARQ HF modem, Rhizomatica / HERMES project** — candidate open-modem fork base ([Section 14](#14-software-openness-and-a-path-to-an-open-modem))
  <https://github.com/Rhizomatica/mercury> · <https://www.rhizomatica.org/>
- **Pat — open-source cross-platform Winlink client (LA5NTA)** — Linux / macOS / Windows / Raspberry Pi
  <https://getpat.io/> · <https://github.com/la5nta/pat>
- **MercuryFM — open VHF/UHF FM fork of Mercury (Guru-RF / ON6URE)** — seeking co-developers and testers ([Section 14.5](#145-mercuryfm--a-call-for-co-developers-and-testers))
  <https://github.com/Guru-RF/MercuryFM>
- **DWS — Dutch Winlink System (documentation and software portal)**
  <https://sites.google.com/myuba.be/dws-dutch-winlink-system> · <https://dws.pa7rhm.nl>
- **DARES — Dutch Amateur Radio Emergency Service (incl. Winlink/DWS)**
  <https://dares.nl/about-dares/> · <https://dares.nl/dws-winlink/>
- **B-EARS — Belgium Emergency Amateur Radio Service (UBA)** — lists WINLINK among its digital modes
  <https://www.uba.be/en/b-ears/our-mission>
- **National regulator — radio amateur information (example: BIPT/IBPT, Belgium)**
  <https://www.bipt.be/consumers/radio-frequencies/private-use-hobby/radioamateurs>
- **IARU Region 1 VHF/UHF/Microwaves Committee (C5) and VHF Managers Handbook**
  <https://www.iaru-r1.org/about-us/committees-and-working-groups/vhf-uhf-shf-committee-c5/>

---

## Contributing

See [Section 16 — How to comment and contribute](#16-how-to-comment-and-contribute). Comments via [GitHub Issues](https://github.com/Guru-RF/winlink-rfc-iaru-r1/issues); proposed text changes via Issues or Pull Requests. English only.
