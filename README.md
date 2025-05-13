Treat this less like the next dropbox and more like a "party trick" or a set of techniques to learn to pass data through compression. I do not endorse high volume use of this tool. I will also refrain from approving more commits to make the tool more convenient to use. There are several bugs that limit the use like the poor use of RAM limiting the size of files to about 100mb and they will remain. If you wish to fix these, you are on your own.

If Youtube sends me a Cease and Desist I'll gladly shut this down.

Infinite-Storage-Glitch
ezgif com-gif-maker

AKA ISG (written entirely in Rust my beloved) lets you embed files into video and upload them to youtube as storage.

This has been quite heavily inspired by suckerpinch's Harder Drive video and discord as a filesystem. Unfortunately no filesystem functionality as of right now.

Now, you might be asking yourself:
But is this against YouTube TOS ?
Installation
The source way (building from source with manually installing dependencies)
=== Please note: building from source takes a lot of CPU and RAM usage. ===
You need to have installed:

Rust
opencv
If having any issues also try installing:

ffmpeg
clang
qt
If you want to or already have went through the hassle of installing Rust, you can git clone this repository, then cargo build --release. Cd to /target/release directory and run the program ./isg_4real.

The easiest way (Docker)
Trying to make anything work on other people's computers is a nightmare so I'll use docker from now on
Trend Oceans wrote a neat article on how to use this method as well.

Install Docker if you haven't already.
Clone this repository
Change into the repository cd Infinite-Storage-Glitch
Run docker build -t isg . to build the docker image.
Run docker run -it --rm -v ${PWD}:/home/Infinite-Storage-Glitch isg cargo build --release to build the project.
That's it. You will find the executable in the target/release directory.

ℹ️ Please Note: The binary will be a linux executable, so you will need to run it in a linux environment. If you do not have a linux environment, you can use WSL or run it using the docker container called isg we just built using a Linux shell or PowerShell:

docker run -it --rm -v ${PWD}:/home/Infinite-Storage-Glitch isg ./target/release/isg_4real
Note: If you are using cmd on Windows, you will need to use %cd% instead of ${PWD}.

How to use
Archive to zip all the files you will be uploading
Run the executable
Use the embed option on the archive (THE VIDEO WILL BE SEVERAL TIMES LARGER THAN THE FILE, 4x in case of optimal compression resistance preset)
Upload the video to your YouTube channel. You probably want to keep it up as unlisted
Use the download option to get the video back
Use the dislodge option to get your files back from the downloaded video
PROFIT
2023-02-16_22-12

Demo
Flashing lights warning !!!1!1 - YouTube Link

Try to use the program on this video and find the files hidden inside.

No it's not just a rick roll.

Explanation 4 nerds
The principle behind this is pretty simple. All files are made of bytes and bytes can be interpreted as numbers ranging from 0-255. This number can be represented with pixels using one of two modes: RGB or binary.

RGB: The cooler mode. Every byte perfectly fits inside one of the colors of an rgb pixel. One rgb pixel can contain 3 bytes at a time. You just keep adding pixels like this until you run out of data. It is leagues more efficient and quick than binary.

Binary: Born from YouTube compression being absolutely brutal. RGB mode is very sensitive to compression as a change in even one point of one of the colors of one of the pixels dooms the file to corruption. Black and white pixels are a lot harder to mess up. Every pixel is either bright representing a 1 or dark representing a 0. We string these bits together to get bytes and continue until we run out of data.

Both of these modes can be corrupted by compression, so we need to increase the size of the pixels to make it less compressable. 2x2 blocks of pixels seem to be good enough in binary mode.

To make it easier on the user, we also include all the relevant settings used to create the video on the first frame of the video. This allows the program to know what mode the video is in and what size to use in order to avoid making the user remember.

Final comments
I appreciate any and all roasting of the code so I can improve.

Do what you want with the code, but credit 
