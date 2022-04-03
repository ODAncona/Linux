---
description: How To Check RAM Speed
---

# About RAM

Basically, RAM dictates how many applications your system can have running at any given time or simply how many tabs and processes Chrome can have running. So the more RAM you have, the more processes and programs you can run. This is why the RAM size is important.



And how do you actually check your RAM speed? Well, first of all, we need to understand how RAM Speed is measured and quantified.



When shopping for a RAM kit to go into your gaming PC, the first figure you’ll notice is the size of the RAM, which these days is in gigabytes. Since the most popular type of RAM is double data rate synchronous dynamic RAM (DDR SDRAM), you’ll probably notice the DDR version too.



Another figure you’re most likely to come across is the number of MHz the RAM has. Often this figure is erroneously assigned to the speed of the RAM when in truth it’s only part of the equation. What you also have to look out for is the Column Access Strobe (CAS) Latency or CL. So why are both figures important?

### Frequency

Frequency refers to bandwidth, which is the amount of data that can be transferred to and from the module at any given time. It’s also known as clock cycles. As you may know, it’s measured in hertz which relates to how many cycles per second the RAM completes.

For instance, if the RAM’s frequency is graded at 3600 MHz, this means it can complete 3.6 billion cycles per second (mega transfers). Theoretically, the higher the frequency, the more data can be transferred per second and thus the faster data can be written and read from the stick. Unfortunately, as I’ve mentioned before, this isn’t the only figure that dictates the RAM’s speed.

### **CAS Latency (CL) – Memory Timings**

The CL refers to how quickly the RAM can respond to commands and requests issued to it. In SDRAM, the delay between reception and response is usually specified in clock cycles. It’s arguably the most important figure in determining memory timing. It’s usually written as CLn, with ‘n’ representing the numeric value of the latency e.g. CL16.

Sometimes a manufacturer won’t make the CL obvious. Instead, they’ll use four figures to denote the memory timing e.g. 16-16-16-35. (AA-TRCD-TRP-TRAS (cycles))

* The first figure in the parameter represents the CAS latency.&#x20;
* The second figure represents the row address to column address delay (TRCD). This relates to the number of clock cycles needed between the opening of a row of memory and reading the columns in it.
* The third parameter represents row precharge (TRP) time which refers to the minimum amount of clock cycles between sending out a precharge request and moving on to the next row.&#x20;
* The fourth parameter represents row active time (TRAS) which refers to the minimum number of clock cycles between an active row command and issuing the per-charge command.

![](<../.gitbook/assets/image (4).png>)

Sometimes you may encounter five parameters with the fifth one representing the command rate. These figures can also be increased (not decreased).

To simplify things, in this guide we’ll be focusing our attention on the CL. Both the frequency (mega transfer rate) and CAS latency are important in determining the speed of your RAM. Having a latency too high can create a bottleneck effect and stifle the speed of your RAM, no matter how high the frequency is.

What this means is that RAM with low mega transfer rates but fast memory timings can actually outperform RAM with high mega transfer rates but slow memory timings.

Often, with higher frequency RAM, the latency is sacrificed. However, RAM with higher latency tends to give you a drop in frequency. So you need to strike a balance.

### **How to Check RAM Frequency in Linux**

The best way to check RAM Frequency is by using the biosdecode command-line utility. With the following steps, I’ll show you how.

1. Open a terminal or console window. Alternatively, you could log in using SSH
2. Once you have the terminal window open, type _`sudo dmidecode –type 1`_

Scan the list of results to find the speed (frequency) for each RAM module you have installed

![](<../.gitbook/assets/image (5).png>)

### How to Find Your RAM CAS Latency <a href="#t-1648918260323" id="t-1648918260323"></a>

Finding your RAM’s frequency is only one part of the equation. In order to calculate your RAM’s true speed, you need to find the CAS latency as well. This is a little trickier. You can find the latency and other timing information under your BIOS settings. You can even adjust them.

However, you may not feel comfortable with tinkering with your computer that way. What if something goes wrong? In this section, I’ll show you how you can find the CAS latency without going into your BIOS settings.

With Linux, the best way to check your latency is by using [i2c-tools.](https://www.richud.com/wiki/Ubuntu\_See\_Live\_RAM\_Timings\_Decode\_DIMMS) You can read more about them on the linked Richud.com wiki page. Once you’ve installed the i2c-tools, you need to run this command:&#x20;

```
sudo modprobe eeprom decode-dimms
```

Alternatively, you can use this command out-of-the-box to find your total RAM speed in nano-seconds:&#x20;

```
lshw -C memory | grep clock
```

### How to Calculate Your RAM’s True Speed <a href="#t-1648918260326" id="t-1648918260326"></a>

So now that you have the frequency and latency, how do you actually find your RAM’s true speed? Another factor to consider is your RAM’s type. These days most people are running DDR (Double Date Rate) SDRAM on their PCs. With DDR5 being the latest.

DDR basically means that the RAM transfers data at both ends of the clock cycle. So it essentially transfers data twice in a single cycle.

Our formula looks like this:&#x20;

(CL x (Cycle ÷ (frequency ÷ data rate))) = Total Latency (Nanoseconds)

$$
\dfrac{CAS \cdot 2000}{Frequency}=Latency (ns)
$$

With my PC CAS = 13.75 and Freq = 3200. Then the latency is 8.6ns.

So this will give us the total latency which is ultimately the delay in nanoseconds between cycles. This is a better representation of your RAM’s speed than frequency is.

### Does RAM Speed Really Matter? <a href="#t-1648918260327" id="t-1648918260327"></a>

If you’re shopping for RAM purely based on frequency/mega transfer rate, you need to remember that with higher frequencies you get higher latency. Which means you aren’t really benefiting from higher transfer speeds. Most manufacturers use this value to try to trick you into buying more expensive RAM. Your module size matters more than the frequency. Never pay extra for RAM kits with higher frequencies.

If you’re gaming on a PC with a dedicated graphics card with its own memory, then the speed of your RAM isn’t really going to affect your computer’s gaming performance in a noticeable way – whether we’re using the total latency or not.

It’s only when we look at systems with integrated graphics where we might see a more apparent difference. Faster RAM may also provide you with a more stable experience if you plan on overclocking. Just like your CPU and GPU, your [RAM can be overclocked](https://gamegavel.com/how-to-overclock-ram/).

### Conclusion

While RAM speed isn’t very important for gaming, if you do processor-intensive work on your computer, then it may count. Either way, whether you’re reading this guide for practical or educational reasons, by the end of it, I hope you know how to check your RAM’s speed as well some of the nuances that go into checking and calculating RAM speed.

[https://gamegavel.com/how-to-check-ram-speed/](https://gamegavel.com/how-to-check-ram-speed/)
