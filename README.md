# YUV2RGB

Author: [Robin Watts](robin@wss.co.uk)
Source: http://wss.co.uk/pinknoise/yuv2rgb/

This page gives various optimised implementations of YUV to RGB conversion routines (8 bit YUV 4:2:0/4:2:2/4:4:4 -> 16 bit RGB). The original version (targetting 15bit RGB) was originally written in response to a forum posting from Michael "Chishm" Chisholm, on [gbadev.org](http://forum.gbadev.org/viewtopic.php?t=15528). Later revisions (targetting 16 bits) were developed from this for use with [Therorarm](http://wss.co.uk/pinknoise/theorarm).

My attempt uses an algorithm originally due to Sophie Wilson of Acorn/e-14/Broadcomm, with additional tweaks from Paul Gardiner in the fast fixup code. Thanks are due to Sophie and Paul for allowing the release of this algorithm into the wild.

# Note

The code given here will work on any ARM that supports halfword stores, regardless of architecture, all the way back to the ARM 7.

The most commonly encountered YUV format is 4:2:0; that's 4 Y values for each pair of UV values. Code is also included for 4:2:2 (2 Y's for each pair of UV's) and 4:4:4 (1 Y for every U V). Similar code can easily be produced to do other YUV flavours; [contact me](robin@wss.co.uk) if you need such code.

As well as ARM assembly versions of each of these variants, there are C equivalents, that may be useful on other architectures. There is no C equivalent given to the 15bit code (though one could trivially be created). Use the ARM assembly versions if you can. If not, use the C. Again, [contact me](robin@wss.co.uk) if you'd like versions done for a different architecture.

A single colourtable is provided in this version, but it's simple to generate the tables at runtime; this can give colour/brightness/contrast control etc for free. [Contact me](robin@wss.co.uk) if you'd like details of this.

All the code here is in ARM assembler format. GCC format is different, but it should be trivial to convert between the two. Again, [Contact me](robin@wss.co.uk) if you need help with this.

# I Am Not A Lawyer

This code is released under the BSD license.

If you do use use this code as part of a piece of software (or hardware), please let me know, purely for my own interest.

# Timings etc.

You'd probably like some timings, to show how much better this code is than all the other alternatives, right?

I don't really have any timings for this code, other than those given in the [forum thread](http://forum.gbadev.org/viewtopic.php?t=15528) on which it was discussed.

To save you hunting through the thread the pertinent bits are probably:

>axxie:

>I have measured Chishm's and Robin's last code.

>Setup was: 256x192, Y,U and V buffers were set to [be random], but constant data, output data was a 4 byte aligned malloced block.

>Tested 100 runs and middled the measurement. (33MHz cycles)

>Chishm's: 1 279 959

>Robin's: 393 571

>Both measurements include the very same calling instructions (Push & copy of arguments, pop afterwards).

Then a bit later:

>Tepples:
>
>There are 560,190 ARM7 cycles between vblanks. A 12fps video takes 5 vblanks or 2,800,950 cycles to present a new frame. So Chishm's YUV decoder takes 45.7% CPU while yours takes 14.1%.

I'd advise you to take all timings with a pinch of salt, because they are bound to vary from application to application, but I think it's clear that the code is significantly better than even a good hand coding of the "obvious" algorithm.

# Warranty

I warrant absolutely nothing about this code. The Tremor lib says the following, and it sounds like the kind of thing I should be saying here too:

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS ``AS IS'' AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE REGENTS OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

In particular, I warrant absolutely nothing about how patent free this method is. It is your responsibility to ensure that this code does not infringe any patents that apply in your area before you ship it!

# ChangeLog

* v0.01: First archive version released to net (GPL license).
* v0.02: Identical version, but rereleased as BSD after Google funded the Theorarm work.
* v0.03: Version with more functions, both C and assembler.
