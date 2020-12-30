## Data Transmission With Optical Vortices

This project was my first undertaking in the Optics lab at Stout as well as my first foray into scientific work in general. 
### Introduction
As optical data transfer begins to approach its apparent limit, we must find new characteristics of laser light to encode data with. One such way is use of the optical vortex which gives us a multitude of new readable characteristics for data transfer. This project seeks develop a proof of concept system that uses this phenomenon created with a spatial light modulator, paired with programmable Arduino Boards in order to transmit data through a laser beam.
<br>
Data is a fundamental and ever-growing aspect of our society and with that comes the need to move large amounts of data as quickly as possible. Optical data transfer has increased internet speeds exponentially, but as the sheer amount of data increases, we are finding  that we must be able to send larger amounts or packets of data at a time.  Information is encoded using various aspects and characteristics of a laser, which means that the more of these characteristics you can control and modify the more information you can send at one time. The optical vortex is one way to increase the encodable characteristics of a laser and by extension increase internet speeds

### What's an Optical Vortex?
An optical vortex is a phenomenon that occurs when a beam of light is given Orbital Angular Momentum (OAM), in other words the beam “twists” itself around its axis of propagation. This causes the beam’s intensity at the very center to drop to zero creating what would look like a “tube” of light. There are several new measurable properties the beam gains, such as topological charge which describes how many times the beam twists in one wavelength. Methods to create optical vortices include using computer generated holograms, deformable mirrors, as well as a spatial light modulator (SLM). We opted to use the SLM.

### Methodology
The	first step to	tackling this	question is	to use a	spatial	light	modulator	to	generate	an	optical	vortex	in	the	laboratory.	The	spatial	light	modulator	allows	me	to	create any	number	of	diffraction	patterns	but,	will	require	a	bit	of	trial	and	error	in	order	to	produce	an	optical	vortex.	Once	I	can reliably	generate	the	optical	vortex the	next step	is	to	design	a	system	that	can	take	in	data,	encode	it	into	laser	light using	only	intensity,	decode	that laser,	and	read	it	on	a	different	computer. A	large	portion	of	this	would	be	programming	the	Arduino	boards.	Algorithms	would	have	to	be	made	to	convert	alpha-numeric data	into	binary,	then	turn	the	ones	and zeros	into	on	and	off,	and	finally	for	the	reverse	to happen	on	a	second	Arduino. I	would	then	take	that	existing	system and	try	to	incorporate	the	generation and	use	of an optical	vortex for the	data	transfer.

### Poster
<img src="https://github.com/nroyce7/nroyce7.github.io/blob/master/research.JPG?raw=true" width="1000">
