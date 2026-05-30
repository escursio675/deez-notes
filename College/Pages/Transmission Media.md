#college 

Transmission media are actually located below the physical layer and are directly controlled by the physical layer. We could assume that
transmission media belong to layer zero.

A **transmission medium** can be broadly defined as anything that can carry information from a source to a destination.

# Guided Media
These include twisted-pair cable, coaxial cable, and fiber-optic cable. Twisted-pair and coaxial cable use metallic (copper) conductors that accept and transport signals in the form of electric current. Optical fiber is a cable that accepts and transports signals in the form of light.

## Twisted Pair Cables
A twisted pair consists of two conductors (normally copper), each with its own plastic insulation, twisted together. One of the wires is used to carry signals to the receiver, and the other is used only as a ground reference.

In addition to the signal sent by the sender on one of the wires, interference (noise) and crosstalk may affect both wires and create unwanted signals. If the two wires are parallel, the effect of these unwanted signals is not the same in both wires because they are at different locations relative to the noise or crosstalk sources
(e,g., one is closer and the other is farther). This results in a difference at the receiver. By twisting the pairs, it makes it probable that both wires are equally affected by external influences. This means that the receiver, which calculates the difference between the two, receives no unwanted signals. The unwanted signals are mostly canceled out.

### Unshielded Versus Shielded Twisted-Pair Cable
The most common twisted-pair cable used in communications is referred to as unshielded twisted-pair (UTP). IBM has also produced a version of twisted-pair cable for its use called shielded twisted-pair (STP). STP cable has a metal foil or braided-mesh covering that encases each pair of insulated conductors. Although metal casing improves the quality of cable by preventing the penetration of noise or crosstalk, it is bulkier and more expensive.
==STP is seldom used outside of IBM.==
![[Pasted image 20260402093008.png]]

### Categories
The Electronic Industries Association (EIA) has developed standards to classify unshielded twisted-pair cable into seven categories. Categories are determined by cable quality, with 1 as the lowest and 7 as the highest. Each EIA category is suitable for specific uses.
![[Pasted image 20260402093040.png|608]]

### Applications
Twisted-pair cables are used in telephone lines to provide voice and data channels. The local loop-the-line that connects subscribers to the central telephone office commonly consists of unshielded twisted-pair cables. 
The DSL lines that are used by the telephone companies to provide high-data-rate connections also use the high-bandwidth capability of unshielded twisted-pair cables.

Local-area networks also use twisted-pair cables.

### Performance 
Twisted Cables can pass a wide range of frequencies, however, with frequencies above 100kHz, the attenuation(dB/km) sharply increases.

## Coaxial Cables
Coaxial cable (or coax) carries signals of higher frequency ranges than those in twisted-pair cable. Instead of having two wires, coax has a central core conductor of solid or stranded wire (usually copper) enclosed in an insulating sheath, which is, in turn, encased in an outer conductor of metal foil, braid, or a combination of the two. The outer metallic wrapping serves both as a shield against noise and as the second conductor, which completes the circuit. This outer conductor is also enclosed in an insulating sheath, and the whole cable is
protected by a plastic cover.
![[Pasted image 20260402093510.png]]

### Performance
Although coaxial cable has a much higher bandwidth, the signal weakens rapidly and requires the frequent use of repeaters. The attenuation is much higher in coaxial cables than in twisted-pair cable.

### Applications
Coaxial cable was widely used in analog telephone networks where a single coaxial network could carry 10,000 voice signals. Later it was used in digital telephone networks where a single coaxial cable could carry digital data up to 600 Mbps. However, coaxial cable in telephone networks has largely been replaced today with fiber-optic cable.
Cable TV networks also use coaxial cables. In the traditional cable
TV network, the entire network used coaxial cable. 

Another common application of coaxial cable is in traditional Ethernet LANs; because of its high bandwidth, and consequently high data rate, coaxial cable was chosen for digital transmission in early Ethernet LANs. 

## Fiber-Optic Cables
A fiber-optic cable is made of glass or plastic and transmits signals in the form of light.

Optical fibers use reflection to guide light through a channel. A glass or plastic core is surrounded by a cladding of less dense glass or plastic. The difference in density of the two materials must be such that a beam of light moving through the core is reflected off
the cladding instead of being refracted into it.

![[Pasted image 20260402094339.png]]

==Note that the critical angle is a property of the substance, and its value differs from one substance to another.==

The outer jacket is made of either PVC or Teflon. Inside the jacket are Kevlar strands to strengthen the cable.Below the Kevlar is another plastic coating to cushion the fiber. The fiber is at the center of the cable, and it consists of cladding and core.

### Propagation Modes
Current technology supports two modes (multimode and single mode) for propagating light along optical channels, each requiring fiber with different physical characteristics. Multimode can be implemented in two forms: step-index or graded-index.

Multimode Multimode is so named because multiple beams from a light source move through the core in different paths. How these beams move within the cable depends on the structure of the core. 

In multimode step-index fiber, the density of the core remains constant from the center to the edges. A beam of light moves through this constant density in a straight line until it reaches the interface of the core and the cladding. At the interface, there is an abrupt change due to a lower density; this alters the angle of the beam's motion. This contributes to the distortion of the signal as it passes through the fiber.

A second type of fiber, called multimode graded-index fiber, decreases this distortion of the signal through the cable. In graded-index fiber, density is highest at the center of the core and decreases gradually to its lowest at the edge.

Single-mode uses step-index fiber and a highly focused source of light
that limits beams to a small range of angles, all close to the horizontal. The single-mode fiber itself is manufactured with a much smaller diameter than that of multimode fiber, and with substantially lower density (index of refraction). In this case, propagation of different beams is almost identical, and delays are negligible. All the beams arrive at the destination "together" and can be recombined with little distortion to the signal.
![[Pasted image 20260402094922.png|527]]

### Fiber Sizes
Optical fibers are defined by the ratio of the diameter of their core to the diameter of their cladding, both expressed in micrometers.
![[Pasted image 20260402095019.png]]

### Performance
Attenuation is flatter than in the case of twisted-pair cable and coaxial cable. The performance is such that we need fewer repeaters when we use fiber-optic cable.

### Applications
Fiber-optic cable is often found in backbone networks because its wide bandwidth is cost-effective.
Some cable TV companies use a combination of optical fiber and coaxial cable, thus creating a hybrid network. Optical fiber provides the backbone structure while coaxial cable provides the connection to the user premises.
LANs also use fiber-optic cables.

### Advantages
1. Higher bandwidth and data rates than either twisted-pair or coaxial cable. 
2. Less signal attenuation and greater transmission distance than that of other guided media. A signal can run for 50 km without requiring regeneration. We need repeaters every 5 km for coaxial or twisted-pair cable.
3. Immunity to electromagnetic interference
4. Resistance to corrosive materials. Glass is more resistant to corrosive materials than copper.
5. Light weight
6. Greater immunity to tapping

### Disadvantages
1. Expertise required for installation and maintenance
2. Unidirectional light propagation makes it so two fibers are needed for bidirectional communication
3. Cost

# Unguided(Wireless) Media

Unguided media transport electromagnetic waves without using a physical conductor. Signals are normally broadcast through free space and thus are available to anyone who has a device capable of receiving them.
The electromagnetic spectrum, ranging from 3 kHz to 900 THz, is  used for wireless communication.

Unguided signals can travel from the source to destination in several ways: ground propagation, sky propagation, and line-of-sight propagation. In ground propagation, radio waves travel through the lowest portion of the atmosphere, hugging the earth. Distance depends on the amount of power in the signal: The greater the power, the greater the distance. In sky propagation, higher-frequency radio waves radiate upward into the ionosphere where they are reflected back to earth. This type of transmission allows for greater distances with lower output power. In line-or-sight propagation, very high-frequency signals are transmitted in straight lines directly from antenna to antenna. Antennas must be directional, facing each other, and either tall enough or close enough together not to be affected by the curvature of the earth. Line-of-sight propagation is tricky because radio transmissions cannot be completely focused.

The section of the electromagnetic spectrum defined as radio waves and microwaves is divided into eight ranges, called bands, each regulated by government authorities. These bands are rated from very low frequency (VLF) to extremely highfrequency (EHF).

Wireless transmission into three broad groups: radio waves, micro-
waves, and infrared waves.

## Radio Waves
Although there is no clear-cut demarcation between radio waves and microwaves, electromagnetic waves ranging in frequencies between 3 kHz and 1 GHz are normally called radio waves; waves ranging in frequencies between 1 and 300 GHz are called microwaves.

However, the behavior of the waves, rather than the frequencies, is a better criterion for classification. Radio waves, for the most part, are omnidirectional. When an antenna transmits radio waves, they are propagated in all directions. This means that the sending and receiving antennas do not have to be aligned. A sending antenna sends waves that can be received by any receiving antenna. The omnidirectional property has a disadvantage, too. The radio waves transmitted by one antenna are susceptible to interference by another antenna that may send signals using the same frequency or band. Radio waves, particularly those waves that propagate in the sky mode, can travel long distances. This makes radio waves a good candidate for long-distance broadcasting such as AM radio. Radio waves, particularly those of low and medium frequencies, can penetrate walls. This characteristic can be both an advantage and a disadvantage. It is an advantage because, for example, an AM radio can receive signals inside a building. It is a disadvantage because we cannot isolate a communication to just inside or outside a building. The radio wave band is relatively narrow, just under 1 GHz, compared to the microwave band. When this band is divided into subbands, the subbands are also narrow, leading to a low data rate for digital communications. Almost the entire band is regulated by authorities. Using any part of the band requires permission from the authorities.

### Applications
The omnidirectional characteristics of radio waves make them useful for multicasting, in which there is one sender but many receivers. AM and FM radio, television, maritime radio, cordless phones, and paging are examples of multicasting.

## Microwaves
Electromagnetic waves having frequencies between I and 300 GHz are called microwaves. Microwaves are unidirectional. When an antenna transmits microwave waves, they can be narrowly focused. This means that the sending and receiving antennas need to be aligned. The unidirectional property has an obvious advantage. A pair of antennas can be aligned without interfering with another pair of aligned antennas.

Microwave propagation is line-of-sight. Since the towers with the mounted antennas need to be in direct sight of each other, towers that are far apart need to be very tall. The curvature of the earth as well as other blocking obstacles do not allow two short towers to communicate by using microwaves. Repeaters are often needed for long-distance communication. Very high-frequency microwaves cannot penetrate walls. This characteristic can be a disadvantage if receivers are inside buildings. The microwave band is relatively wide, almost 299 GHz. Therefore wider subbands can be assigned, and a high data rate is possible. Use of certain portions of the band requires permission from authorities.

### Applications
Microwaves, due to their unidirectional properties, are very useful when unicast (one-to-one) communication is needed between the sender and the receiver. They are used in cellular phones, satellite networks, and wireless LANs.

# Infrared
Infrared waves, with frequencies from 300 GHz to 400 THz, can be used for short-range communication. Infrared waves, having high frequencies, cannot penetrate walls. This advantageous characteristic prevents interference between one system and another; a short-range communication system in one room cannot be affected by another system in the next room. However, this same characteristic makes infrared signals useless for long-range communication. In addition, we cannot use infrared waves outside a building because the sun's rays contain
infrared waves that can interfere with the communication.

### Applications
The infrared band, almost 400 THz, has an excellent potential for data transmission. Such a wide bandwidth can be used to transmit digital data with a very high data rate. The standard originally defined a data rate of 75 kbps for a distance up to 8 m. The recent standard defines a data rate of 4 Mbps.
Infrared signals defined by IrDA transmit through line of sight; the IrDA port on the keyboard needs to point to the PC for transmission to occur.