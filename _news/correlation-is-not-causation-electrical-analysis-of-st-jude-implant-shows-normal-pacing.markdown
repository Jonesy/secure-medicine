---
title: 'Correlation is Not Causation: Electrical Analysis of St. Jude Implant Shows
  Normal Pacing'
date: 2016-08-30 07:28:00 Z
leadin_text: Here's an abbreviated technical analysis of some claims by Muddy Waters
  and St. Jude regarding pacemaker/defibrillator security. We will show you why correlation
  is not causation in the sense that a scary-looking screen is not a reliable indicator
  of a clinically relevant security problem.
author: Kevin Fu
---

**St. Jude Merlin Error Indicators Are Not Evidence of Malfunction**

![muddy-jude.png](/uploads/muddy-jude.png)

Here's an abbreviated technical analysis of some claims by Muddy Waters and St. Jude regarding pacemaker/defibrillator security. We will show you why correlation is not causation in the sense that a scary-looking screen is not a reliable indicator of a clinically relevant security problem. We did this analysis based on our experience over the last ten years [analyzing pacemaker and defibrillator security](http://www.secure-medicine.org/public/publications/icd-study.pdf) and our experience building cardiac arrhythmia simulators for humanitarian [pacemaker reuse](http://www.secure-medicine.org/public/publications/icd-study.pdf). Read more at our [ancient research website](https://spqr.eecs.umich.edu/publications.php?q=health). Or see our [index of previous blog posts on medical device security](http://blog.secure-medicine.org/p/index.html). This is a fun extracurricular activity for our team at the [University of Michigan](http://ns.umich.edu/new/releases/24153-holes-found-in-report-on-st-jude-medical-device-security) and [Virta Labs](https://virtalabs.com/), and we may post more thoughts before we return to our regular lives baking hearth breads and helping hospitals with cybersecurity risks. 

 The Muddy Waters report of August 25 showed a screenshot which they say shows an “apparent malfunction.” They also say that red error marks “are also indicators that the device is malfunctioning.” We were curious about these claims and decided to see if we could produce the same onscreen displays without causing any malfunction. This summary shows the screenshot is correlated with normal pacing and sensing, suggesting that the Muddy Waters report misinterprets clinical relevance of the screenshot.

![IMG_20160829_081303.jpg](/uploads/IMG_20160829_081303.jpg)
![IMG_20160830_105318.jpg](/uploads/IMG_20160830_105318.jpg)

**Figure 1:** Our experiment shows that a Merlin programmer screenshot from p. 17 of the Muddy Waters report is not supportive evidence of a successful attack. The top photo shows our reproduction of the Merlin programmer screen photo, but without causing changes to the pacing pulses. Our end-to-end oscilloscope measurements (bottom photo) show that pacing pulses continue normally despite the three benign alerts that are expected when not connected to cardiac tissue. 

**Hypothesis:** The Merlin programmer screen photo on page 17 of the Muddy Waters report is not supportive evidence of appearing “to have caused the device to pace at a rapid rate.”

**Approach:** Produce the same on-screen screen output, and externally measure electrical signals to test safety and effectiveness of pacing and sensing.

**Result:** We reliably produced the same screen output while the implant continued to pace normally.

**Material:** St. Jude Medical Fortify Assura ICD, Merlin programmer (software version 22.0.1 rev1)

Clinical validation: Verified by Dr. Thomas Crawford, a cardiologist and a clinical electrophysiologist at the University of Michigan Health System's Frankel Cardiovascular Center.

**Commentary:**
To verify pacing, we configured the device to emit 40 bpm pacing pulses at 2.5 V, then connected a clipped lead (~20 cm) to the V (IS-1 Bi) sense/pace port, connected an oscilloscope to the clipped lead with 50 Ω probes, and visually confirmed that the device was emitting 40 pulses per minute (Figure 1 bottom). To verify sensing, we used a signal generator to produce a 0.5 Hz square wave (consisting of 2 events, a rising then a falling edge, for a total of 1 event per second or 60 pbm) at 2 mV which we fed into the sense/pace port via the same lead; the programmer recognized a 60 bpm beat as expected. We tested other square-wave frequencies between 0.5 Hz and 2 Hz to verify that the sensing worked as expected.

To reproduce the markers that the Muddy Waters report highlights as indicators of a successful attack, we introduced benign electrical noise on the sense/pace port via the clipped lead by connecting the lead to a separately grounded oscilloscope (i.e., not grounded to the “can” of the device, which typically acts as ground). This noise was sufficient to trigger the “VS2” markers on the programmer screen, indicating that the device sensed a “ventricular beat.” While sampling the 40 bpm pacing output as described above, we reproduced the count of three alerts visible in the Muddy Waters report’s screen photo: two alerts from high impedance on two leads (since those were not connected to cardiac tissue), and one indicating “ventricular noise reversion.” The pacing and sensing continued to function normally.