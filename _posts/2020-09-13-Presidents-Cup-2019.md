---
layout: post
title: "Presidents Cup Challenges September 2019"
categories: CTF
tags: CTF
---

I have been participating in Capture the Flags for a few years now, I highly recommend Pico CTF if you are just getting started!
(https://picoctf.org/). This is achallenge from the first season I participated in Presidents Cup which is a CTF hosted by Cybersecurity & Infrastructure Security Agency(https://www.cisa.gov/presidents-cup-supporting-materials) 


### The Curious Case of the Matryoshka
#### Category: Collect and Operate
#### Difficulty Level: 1000
#### Executive Order Category: Cyber Analysis

### Background
Intelligence sources have captured data from a notorious APT and malicious actor in the cyber realm. This suspect also offers his services by writing custom malware for clients he deems worthy. This data and the relevant intelligence report are available to you. You must analyze this data to find the APT’s ultimate password which is the flag for this challenge.

**Hint!** Your intelligence is very important in this challenge.

### Getting Started

This challenge will require various investigative and cyber analysis skills. 

*Note: When extracting zip files with 7-zip, you may need to explicitly choose to “Extract to ...” somewhere on the local machine in order to view the files inside.*


*Level 1*

The zip file is named `Who Am I`. The password to the Level 1 zip file is the nickname 'Warlock' from the Intelligence Report document. 

*Level 2*

I inspected the metadata info attached to each of the images, the clue to review is `You're so meta`.  Exiftool is a command line option, or we can use the classic Cyberchef!  https://gchq.github.io/CyberChef/#recipe=Extract_EXIF()   Placing `Luigi's Mansion image` into Cyberchef input reveals the password as `2q89vzqrfova` and it will unlock the Level 2 zip file.

*Level 3*

You may notice the timestamps in the `Password Table.csv` file are in Epoch time. The suspect's birthday is also `January 1st, 1970`, which is when epoch time began. After converting the U.S. release date of Luigi's Mansion (`November 18, 2001`) from Level 2 to the corresponding Epoch time (`1006095155`), there was a similar time in the csv. The corresponding string (`imevap4o18ej`) to this timestamp will unlock Level 3's zip file.

*Level 4*

The numbers present are Longitude and Latitude coordinate pairs. Many of them matched his dislikes, so it us unlikely he would want to meet there. The password is `Puerto Rico` as shown by the coordinates that do not match. This will unlock Level 4's zip.

*Level 5*

The five files are encoded with `Caesar/ROT shift cipher`. The shift value is the opposite of the suspects fav number. Another helpful resource is dcode which I often use to decode during CTFs. (https://www.dcode.fr/rot-13-cipher) The file with the password was `x2n0wuh9sue1.txt' and it has a `ROT shift of -7/19`. The password is `yaqitkcuyrgx` found in the file will open the Level 5's zip file.

*Level 6*

Lastly hash the album cover image and use this as the password to the final zip. I tried the MD5 hash (`818532970e654e26d76e27858c508346`) of the album cover image since it is one of the most common types. It is the password to the 6th and final zip file.

Found Flag! - `We're leaving together, but still it's farewell`
