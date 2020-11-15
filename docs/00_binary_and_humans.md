# 00 Binary and humans

Lots of folks glaze over binary because in programming binary operations are confusing. We can skip binary operations but still understand what binary is. In the same sense you can count and read numbers without knowing how multiplication work.

## What uses binary?

Everything digital, and most electronics. Any time the smallest piece of info transmitted is 1/0 then we're using binary. Otherwise it is likely analog which uses signal strength at a point in time for a smallest piece of info. 

Analog is more complicated (read: harder) for programmers so we like digital inputs and outputs.

This file is a binary text document, just like any other file (mp3, pdf etc), is stored as binary. Many 0s and 1s were expended to make this happen.

## How is text binary? What about audio? Or pictures?

So how do we get from music or images, or text, to binary? First we come up with a way to represent the data as a list of numbers.

### __Text__

ASCII is one way to represent text as numbers. For example in ASCII the letter "a" is the number 97. Ironically number characters are represented by numbers too! For example "1" is 49.

So a `.txt` file with binary representing the number 49 would show "1" when you open it with notepad or some other editor.

Whitespace - tabs, spaces, linebreaks - are all represented by numbers.

This concept of representing data with numbers is "encoding" and sometimes referred to as the "format" of a file - or a "protocol" in networking.

Typically these days we use UTF-8 which is a newer encoding that can handle more languages by counting higher.

Most people do not memorize encodings and instead use libraries or lookup the specification when they need to.

### __Audio__

Sound is a little more complicated than text because it is not obvious how to represent waves with numbers. That is because no one really does!

Programmers don't store all of the audio. We snapshot (sample) the height of the wave (amplitude) every so often and record that as list of numbers instead. MP3 is more complicated than that to keep files small, but the raw data is captured this way. If you want Left/Right stereo you just have two lists of numbers.

To figure out how to reconstruct the sound from that, we need to know how often those snapshots were taken. We put a few numbers at the beginning of the file to describe that frequency.

The "headers" are numbers at the beginning to explain the rest of the numbers. Lots of file formats and protocols need headers to explain things like what version of the spec they are following.

There are many formats for audio, but the raw data is generally the same (a list of amplitudes). You can lookup the spec for your favorite media file extensions to get the gritty details.

### __Images__

The raw data for an image is typically RGB but it can be any set of colors you want. 

To represent one pixel we need three numbers, one for red, green, and blue. To represent a picture we need three numbers for each pixel, and some header numbers at the start of the file which explain the height/width in pixels of the image.

Again that's an example of raw data. Some formats are actually pretty similar to the raw data, but like .mp3 with audio, .jpg files complicate things in order to make the files smaller.

## OK but those numbers were not 1 or 0? How is that binary?

Lets rewind and think about what a real number *is* for a second. Real numbers represent quantities. You can count them. 

There are alternative ways of counting. Imagine humans had 9 fingers. The whole number system could be different.

Computers just have 2 fingers.

Computers represent the *same* quantities with *different* numbers.

Take the number 0123. That could also be calculated like this by someone with 10 fingers. Remember digits represent a multiple of 10. You have 1s, 10s, 100s, 1000s places from right to left:

```
3 * 1
2 * 10 +
1 * 100 (10x10) +
0 * 1000 (10x10x10)
```

A computer would calculate 0123 like this instead. They multiply by 2, so each digit represents 1s, 2s, 4s, 8s, 16s, 32s, 64s, 128s with each digit being 0 or 1:

```
1 * 1 +
1 * 2 +
0 * 4   (2x2) +
1 * 8   (2x2x2) +
1 * 16  (2x2x2x2) +
1 * 32  (2x2x2x2x2) +
1 * 64  (2x2x2x2x2x2) +
0 * 128 (2x2x2x2x2x2x2) +
```

That left column bottom to top 01111011 is binary :) just like the left column was 0123 for a person with 10 fingers.

-------

What is really important to remember is that even though computers use different labels for quantities, they are representing the same quantities that we are in base 10.

## Programming and binary

Memory costs money in computers, so we limit the number of digits used for any given quantity we are representing. Often in programming you will hear programmers talk about "bigint" or "long" versus "int". Or you will hear them describe 32 bit or 64 bit things.

1 bit = 1 digit in binary. These words describing the kind of number or number of bits are just jargon used by programmers to explain how high they want a computer to be able to count.

More jargon, and some trivia:

* bit = one 1 or 0
* byte = 8 bits
* kilobyte = 1024 bytes
* megabyte = 1024 kilobytes
* gigabyte = 1024 megabytes

People are not always using 1024x, sometimes they use 1000x. There is always some confusion about whether someone  about "megabit" versus "megabyte" and they have different representations like Mb or MB.

It usually will not matter because if you need to know how many bytes of something there are I recommend saying it precisely. Like 1,000,692,372 bytes, rather than saying 1GB.

Use GB or MB or Gb or Mb when precision is less important.

## A little example in the shell

By default bash will try to decode binary values as plaintext. So if you `cat` an image you will not see an image in your terminal, instead you get garbage.

Modern CPUs do not typically operate on one bit at a time; because they are so fast 32, 64 even 128 bit operations exist. 8 bits is often the smallest unit.

Data would take up tons of space if we showed 0s and 1s and programmers have a hard time reading that. So instead when we view binary we view it in hexidecimal, which is compact and two digits represents 8 bits or an entire byte.

One hexidecimal digit can represent values 0-15 (this is base 16 instead of base 10 or base 2), but our number system can't do that. We run out at 9! So programmers decided to represent 10, 11, 12, 13, 14, 15 as A, B, C, D, E, F. To indicate a value is hexidecimal we prefix it with 0x, so if you see "0xA9" that is actually one byte of data, representing digits with values 10 and 9. The hex number system (base 16) works just like binary and base 10 to represent 123, but see how fast we get there? Kids would count so high if they had 16 fingers:

```
B * 1
7 * 16
0 * 256 (16x16)
```

> 0x7B

Remember two digits in hex is one byte, which can represent a number as large as 255. In UTF-8 and ASCII one byte is enough to represent basic characters and inputs in english.

__Example__

Remember "1" is 49 when using ASCII or UTF8 to encode text? 49 is 0x31 in hex, which is how we look at binary.

Run `echo -n "1" > sample.txt` to write the character "1" to a file without an extra newline.

We can view the binary with the `hexdump` shell command:

`hexdump -C sample.txt` shows:
```
00000000  31
00000001
```

> [doc for hexdump](https://man7.org/linux/man-pages/man1/hexdump.1.html)

The first number above is the offset, the second is the value at that point.

See our "31" in hex at offset 0? As expected.

-----

[Next: File Systems](01_filesystem.html)