---
author: "Jonathan Roth"
title: "Bumbling"
date: "2022-01-27"
description: ""
tags: []
ShowToc: false
ShowBreadCrumbs: true
---
### Introduction
I've encountered the following scenario several times:

My family and I have a vacation of some sort and we each take pictures throughout the entire length of the trip. Afterwards, we share them by uploading them to a shared server. However, all of the photos are all out of order because different phones and cameras use different conventions for naming images. Organizing the photos afterwards can be tedious because the photos are often not sorted in chronological order.  

Modern operating systems allow you to sort any file by name or by the date that the file was created but that date refers to the current machine (i.e. when you transferred the files from your phone to your computer) and not when the image was created by the camera. Although some files contain date information in the name, for example "IMG\_20211014\_175621.jpg", not all of them do. There is no good way to sort images using only a file manager.

Fortunately, most image formats (eg jpg, png, heic, nef) allow the camera to include metadata such as the data that the image was taken along with the actual image itself. Bumbling is a tool that uses that metadata to rename images so that they are in chronological order.

Necessity is the mother of invention. I designed bumbling to organize photos from an arbitrary amount of sources (ie phones). This makes creating a photo album much easier. I can choose the best pictures from an event without searching everywhere to see if there are any more. I often leave the date prefix and give the photo a friendly name, for example IMG\_0864.HEIC --> 2021-12-03\_xmas-tree.HEIC.

Source Code available [here](https://github.com/JonathanRoth13/bumbling "here")

### Tutorial

Here are some photos taken by an IPhone.

```text
$ ls
IMG_0864.HEIC
IMG_0928.HEIC
IMG_0930.HEIC
IMG_0931.HEIC
IMG_0933.HEIC
IMG_0937.HEIC
IMG_0938.HEIC
IMG_0939.HEIC
IMG_0946.HEIC
IMG_0947.HEIC
```

We could include the date in the filename. 

```text
$ bumbling . .
IMG_0864.HEIC	-->	2021-12-03_IMG_0864.HEIC
IMG_0928.HEIC	-->	2021-12-12_IMG_0928.HEIC
IMG_0930.HEIC	-->	2021-12-12_IMG_0930.HEIC
IMG_0931.HEIC	-->	2021-12-12_IMG_0931.HEIC
IMG_0933.HEIC	-->	2021-12-12_IMG_0933.HEIC
IMG_0937.HEIC	-->	2021-12-14_IMG_0937.HEIC
IMG_0938.HEIC	-->	2021-12-14_IMG_0938.HEIC
IMG_0939.HEIC	-->	2021-12-14_IMG_0939.HEIC
IMG_0946.HEIC	-->	2021-12-15_IMG_0946.HEIC
IMG_0947.HEIC	-->	2021-12-15_IMG_0947.HEIC
```

Or we could rename all the files
```text
$ bumbling -x --y="winter '%y " . .
IMG_0864.HEIC	-->	winter '21 00.HEIC
IMG_0928.HEIC	-->	winter '21 01.HEIC
IMG_0930.HEIC	-->	winter '21 02.HEIC
IMG_0931.HEIC	-->	winter '21 03.HEIC
IMG_0933.HEIC	-->	winter '21 04.HEIC
IMG_0937.HEIC	-->	winter '21 05.HEIC
IMG_0938.HEIC	-->	winter '21 06.HEIC
IMG_0939.HEIC	-->	winter '21 07.HEIC
IMG_0946.HEIC	-->	winter '21 08.HEIC
IMG_0947.HEIC	-->	winter '21 09.HEIC
```

However, bumbling's main purpose is to combine images from two sources. Here are photos taken from two iphones.
```text
$ ls iphone_00/
IMG_0964.HEIC
IMG_0965.HEIC
IMG_0966.HEIC
IMG_0971.HEIC
IMG_0973.HEIC
IMG_0976.HEIC
IMG_0977.HEIC
IMG_0978.HEIC
IMG_0979.HEIC
IMG_1005.HEIC
IMG_1010.HEIC
IMG_1011.HEIC
IMG_1012.HEIC
IMG_1013.HEIC
IMG_1014.HEIC

$ ls iphone_01/
IMG_7047.HEIC
IMG_7049.HEIC
IMG_7104.HEIC
IMG_7105.HEIC
IMG_7108.HEIC
IMG_7114.HEIC
IMG_7115.HEIC
IMG_7339.HEIC
IMG_7340.HEIC
IMG_7341.HEIC
IMG_7342.HEIC
IMG_7343.HEIC
IMG_7346.HEIC
IMG_7347.HEIC
IMG_7348.HEIC
IMG_7349.HEIC
IMG_7350.HEIC
IMG_7351.HEIC
IMG_7352.HEIC
IMG_7353.HEIC
IMG_7354.HEIC
```

Although the photos are in order on both phones, they will not be in order once they are combined into the same directory. All of the photos from phone 0 will be before phone 1. If you wanted to make a album for example, you would constantly be looking back and forth. This is what bumbling was designed for. 
```text
$ bumbling -x iphone_00/ iphone_01 .
iphone_00/IMG_0964.HEIC	-->	2021-12-17_00.HEIC
iphone_00/IMG_0965.HEIC	-->	2021-12-17_01.HEIC
iphone_00/IMG_0966.HEIC	-->	2021-12-17_02.HEIC
iphone_00/IMG_0971.HEIC	-->	2021-12-18_03.HEIC
iphone_00/IMG_0973.HEIC	-->	2021-12-18_04.HEIC
iphone_01/IMG_7047.HEIC	-->	2021-12-18_05.HEIC
iphone_01/IMG_7049.HEIC	-->	2021-12-19_06.HEIC
iphone_00/IMG_0976.HEIC	-->	2021-12-19_07.HEIC
iphone_00/IMG_0977.HEIC	-->	2021-12-19_08.HEIC
iphone_00/IMG_0978.HEIC	-->	2021-12-19_09.HEIC
iphone_00/IMG_0979.HEIC	-->	2021-12-19_10.HEIC
iphone_01/IMG_7104.HEIC	-->	2021-12-21_11.HEIC
iphone_01/IMG_7105.HEIC	-->	2021-12-21_12.HEIC
iphone_01/IMG_7108.HEIC	-->	2021-12-21_13.HEIC
iphone_00/IMG_1005.HEIC	-->	2021-12-22_14.HEIC
iphone_01/IMG_7114.HEIC	-->	2021-12-22_15.HEIC
iphone_01/IMG_7115.HEIC	-->	2021-12-22_16.HEIC
iphone_00/IMG_1010.HEIC	-->	2021-12-26_17.HEIC
iphone_00/IMG_1011.HEIC	-->	2021-12-26_18.HEIC
iphone_00/IMG_1012.HEIC	-->	2021-12-26_19.HEIC
iphone_00/IMG_1013.HEIC	-->	2021-12-26_20.HEIC
iphone_00/IMG_1014.HEIC	-->	2021-12-26_21.HEIC
iphone_01/IMG_7339.HEIC	-->	2021-12-26_22.HEIC
iphone_01/IMG_7340.HEIC	-->	2021-12-26_23.HEIC
iphone_01/IMG_7341.HEIC	-->	2021-12-26_24.HEIC
iphone_01/IMG_7342.HEIC	-->	2021-12-26_25.HEIC
iphone_01/IMG_7343.HEIC	-->	2021-12-26_26.HEIC
iphone_01/IMG_7346.HEIC	-->	2021-12-27_27.HEIC
iphone_01/IMG_7347.HEIC	-->	2021-12-27_28.HEIC
iphone_01/IMG_7348.HEIC	-->	2021-12-27_29.HEIC
iphone_01/IMG_7349.HEIC	-->	2021-12-27_30.HEIC
iphone_01/IMG_7350.HEIC	-->	2021-12-27_31.HEIC
iphone_01/IMG_7351.HEIC	-->	2021-12-27_32.HEIC
iphone_01/IMG_7352.HEIC	-->	2021-12-27_33.HEIC
iphone_01/IMG_7353.HEIC	-->	2021-12-27_34.HEIC
iphone_01/IMG_7354.HEIC	-->	2021-12-27_35.HEIC
```
Now all the photos, regardless of origin, are nicely organized.
