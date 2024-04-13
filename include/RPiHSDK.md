# Building a Raspberry Pi based ultrasound imaging development platform

![](/elmo/data/arduinoffset/LineImageEnveloppe.jpg)

[](@description Using a Raspberry Pi to image)


## Disclaimers

* __Disclaimer #0__: __This is not a medical ultrasound scanner__! It's a development kit that can be used for pedagogical and academic purposes - possible immediate use as a non-destructive testing ([NDT](/include/NDT.md)) tool, for example in metallurgical crack analysis. As in all electronics, be [careful](/WordOfCaution.md).
* __Disclaimer #1__: though an engineer, this project is the first of its sort, I never did something related. It's all but a finalized product.
* __Disclaimer #2__: Ultrasound raises questions. In case you build a scanner, use caution and good sense!



## Experiments

### What can be done with this hardware?

This dev kit has been developped for pedagogical purposes, to understand how ultrasound imaging and non-desctrucive testing work. This structure can be used to develop:

* other modalities of ultrasound imaging - and be used as a platform for A-mode, or B-mode imaging; 
* it can also be used for array imaging - the modules can be used with a multiplexer for do synthetic aperture beamforming; 
* new signal processing methods;
* test transducers - which can be used as well for maintenance and repairs of ultrasound probes;
* other non-destructive testing apparatus.


Why are you doing this ? or besides pedagogical uses of your prototype, we want to know if you are thinking about other applications ? Where your prototype can be more useful? In Africa for example, can your prototype solve some problems? 


### Benchmark of acquisition

The first acquisition, used as a reference, is through the ADCs of a STM32F205 ([feather WICED](/retired/croaker/)) - reaching a whooping 1.7Msps (didn't master the interleaved mode..). Even at these speeds, one can see some features of an ultrasound image, on a wire-phantom. However, resolution isn't that great, let's see if that can be improved?

![](/retired/croaker/data/20161217/20161217-222737-commented.png)

### The Raspberry Pi experiment setup

It can be noted that the ADC used in the experiments below is running at half its acquisition speed, due to a blunder - soldering two pins of the second ADC together. However, the 9-bit, 11Msps ADC works relatively well to analyse the raw signal as well as the enveloppe.

![](/elmo/data/arduino/setup.png)

This is a picture from a [first test](/elmo/data/arduino/20170611-arduino.md) with all custom made modules, including raspberry ADC.

The image is created from a wire phantom, based on a stripboard with a 2.54mm pitch. Wire phantoms are often used as calibration devices, and to assess the lateral and axial resolution of a sensor.

### Costs of the materials



### Some results: signals and images

I'm getting similar images using the analog enveloppe detection (acquired by the [DAQ](/elmo/), through a track exposed on the Analog Processing Module), compared to the digital enveloppe detection, as described below, again on the wire phantom:

![](/elmo/data/arduinoffset/LineImageEnveloppe.jpg) 

The same procedure was applied to acquire the enveloppe created through the analog enveloppe detection, exposed on the Analog Processing Module:

![](/elmo/data/arduino/EnveloppeLineEnveloppe.jpg) 

### Plugging the Pi to an existing probe

A beaglebone black had been used with its [high-speed DAQ](/retired/toadkiller/) to be connected to an existing [mechanical probe](/retroATL3/), with [some results](https://kelu124.gitbooks.io/echomods/content/Chapter2/basicdevkit.html). The next step has been to interface the Pi to this probe through the [24Msps Pi ADC pHAT](/elmo/), to see if one can get the same quality of image, and produce a ultrasound loop. The setup looks as below:

![](/elmo/images/20170717_210209.jpg)

It produced in the end actually good images:

![](/elmo/data/Imgs/pic_probeX.data.jpg)

along with details of the processing chain (see the [work jupyter notebook](/elmo/data/20170715-ProbeTest.ipynb)):

![](/elmo/data/Imgs/Processing_probeX.data.jpg)

### Lessons on the way

* __Start with common elements and modules__: I had been _quite_ presumptuous to try and create something from scratch. Do your homeworks, review
* __Modular design__ is the way to go. Discussing in various communities, there are only so many designs that didn't fail in the first time. Make modules out of your designs, so that if one part fails, you aren't left with nothing but a new invoice from the PCBA.
* __Share__: the world of open-source is awesome. There are plenty of good ideas around, and people don't have the time to implement them. There are other persons who like to implement stuff. Merge the two. Enjoy!
* __Do what you like__: don't do what you don't like. Find support - even if it's PCBA - for your designs. Sometimes, it's good to rely on pros to do your designs cleanly. Or maybe someone will be happy to review the designs. It does count.
* __Document__: an easy thing to say.. but it has to be repeated. Don't hesitate to use/make tools to support this quest, it makes your life soooo much easy. All of this gitbook is generated on the fly - my rule of thumb is: _Don't write anything twice_.

## What's next?

On a __hardware side__:

* The pulser-module design uses only two inputs and one high voltage source. However, the chip enables more complex uses as a pulser, which can be further explored.
* A multiplexer module can be used, to interface this single channel kit with an array probe. Doing this would permit to do synthetic aperture imaging, and to characterize as well each element in the array.
* A whole field left unexplored so far is that of the transducer. As the key sensor in the kit, it would be interesting to explore relevant technologies to develop an open and accessible transducer.
* Quite interestingly, I would love to merge all modules once again on one RaspberryPi3-compatible hat. I want still to cut some costs on the pulser side and increase its robustness.

On a __software side__:

* The Raspberry Pi can be used a bit more. From a software point of view, the modules could be wirelessly controlled, leveraging the existing wireless communication channel, so that researchers can use a single unit for a laboratory, controlled from personal computers.
* The images will need to be stored in a DICOM-compatible format. 

On the __OSH side project__ - the contribution of a tool to the community:

* A campaign should start soon to make the ADC accessible. It seems there's a demand for high speed DAQ there. Just need to confirm the PCBA.


### Who's working on this?

A summary of the contributors using the modules (or having ordered them) is detailed below. Some continents are still to be represented!

![](/include/community/map.jpg)

# And you?

Want to learn more? You can join the [slack channel](https://join.slack.com/usdevkit/shared_invite/MTkxODU5MjU0NjI1LTE0OTY1ODgxMDEtMmYyZTliZDBlZA) if you want to discuss, but there are plenty of other sources:

* Obviously, you can __read the [online manual/book](https://www.gitbook.com/book/kelu124/echomods/details)__ for a easily readable and searchable archive of the whole work
* You can also __fork the [project repo](https://github.com/kelu124/echomods/)__, for the source files, raw data and raw experiment logs or explore the [hackaday page](https://hackaday.io/project/9281-murgen-open-source-ultrasound-imaging), where I tried to blog day-to-day experiments in a casual format
* __Want a scientific article?__ Have a look at the [article summarizing the experiment on the Journal of Open Hardware](http://openhardware.metajnl.com/articles/10.5334/joh.2/) - [DOI:10.5334/joh.2]( http://doi.org/10.5334/joh.2)
* __Want to buy the modules and make your own setup?__ Visit the Tindie store for the [analog processing unit](https://www.tindie.com/products/kelu124/ultrasound-imaging-analog-processing-module/) and the [pulser](https://www.tindie.com/products/kelu124/ultrasound-imaging-pulser-module/) or [the motherboard](https://www.tindie.com/products/kelu124/ultrasound-modules-motherboard/). Ping me on [Slack](https://join.slack.com/usdevkit/shared_invite/MTkxODU5MjU0NjI1LTE0OTY1ODgxMDEtMmYyZTliZDBlZA) if there's no stock remaining.

#### Articles

Under CC-BY-4.0, [main article here](https://openhardware.metajnl.com/articles/10.5334/joh.2/) 


#### Some stats






[](@autogenerated - invisible comment)