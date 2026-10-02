# CTFLearn — WOW.... So Meta

## Challenge Link: https://ctflearn.com/challenge/348

## Challenge Description

> WOW.... So Meta
> This photo was taken by our target. See what you can find out about him from it.

**Category:** Forensics / Metadata

---

## Objective

The goal is to inspect the provided image and discover information hidden within its metadata.

---

## Step 1 — Download the Image

Download the image from the challenge and save it locally.

Example filename:

```bash
3UWLBAUCb9Z2.jpg
```

Move into the directory containing the image:

```bash
cd ~/Downloads
```

---

## Step 2 — Identify the File

Use the `file` command to verify that the downloaded file is a JPEG image:

```bash
file 3UWLBAUCb9Z2.jpg
```

Expected output:

```text
JPEG image data
```

---

## Step 3 — Inspect EXIF Metadata

Use `exiftool` to examine the image metadata:

```bash
exiftool 3UWLBAUCb9Z2.jpg
```

The output contains several metadata fields, including:

```text
Software              : Photos 1.5
Modify Date           : 2014:12:27 16:45:55
Date/Time Original    : 2014:12:27 16:45:55
Camera Serial Number  : flag{EEe_x_I_FFf}
```

The unusual value in the **Camera Serial Number** field is the flag.

---

## Step 4 — Extract the Flag Directly

Instead of reading the complete metadata, we can search for the word `flag`:

```bash
exiftool 3UWLBAUCb9Z2.jpg | grep -i flag
```

Output:

```text
Camera Serial Number           : flag{EEe_x_I_FFf}
```

---

## Flag

```text
flag{EEe_x_I_FFf}
```

---

## Key Takeaway

The challenge demonstrates why **metadata should not be overlooked during image forensics**.

Images can contain information such as:

* Camera information
* Creation and modification dates
* GPS coordinates
* Software used to edit the image
* Author information
* Comments
* Custom metadata fields

For CTF image-forensics challenges, useful tools include:

```bash
exiftool
exif
strings
file
binwalk
```

For this challenge, `exiftool` was sufficient to identify the hidden flag.