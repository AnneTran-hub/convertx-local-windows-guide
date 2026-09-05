# ConvertX Local Installation and Usage Guide

This guide explains how to install and run **ConvertX locally on Windows using Docker Desktop**.

ConvertX allows you to convert files such as **DOCX, XLSX, PPTX, and PDF** on your own computer instead of uploading them to an online file-conversion website.

> This guide uses drive `D:` for Docker storage and ConvertX data to reduce unnecessary usage of the Windows `C:` drive.
>
> You may use another drive or folder if you prefer.

---

## 1. Install Docker Desktop

ConvertX runs inside a Docker container, so **Docker Desktop must be installed first**.

Download and install Docker Desktop for Windows from the official Docker website.

After installation, open **Docker Desktop** and wait until Docker is running.

### Optional: Move Docker Storage to Drive D

Docker images and containers can consume several gigabytes of disk space.

By default, Docker Desktop may store this data on the Windows `C:` drive.

If you want to store Docker data on another drive:

1. Open **Docker Desktop**.
2. Go to:

```text
Settings → Resources → Advanced
```

3. Find:

```text
Disk image location
```

4. Click **Browse**.
5. Select a folder on drive `D:`.

For example:

```text
D:\DockerData
```

6. Click **Apply** and allow Docker Desktop to restart.

> If you already have Docker containers, changing the disk image location may move Docker's existing images, containers, and Docker-managed volumes to the new location.
>
> Do not manually delete Docker's old storage folder during the migration.

---

## 2. Verify Docker Installation

Open **PowerShell**.

Run:

```powershell
docker --version
```

If Docker is installed correctly, PowerShell will display the installed Docker version.

For example:

```text
Docker version 29.7.2, build ...
```

> Your version number may be different.

You can also run:

```powershell
docker info
```

If Docker is running correctly, PowerShell will display information about your Docker installation.

### Docker Is Ready

If both commands work without errors, Docker is ready to use.

---

## 3. Download ConvertX

ConvertX does not need to be downloaded manually as a ZIP file or Windows `.exe`.

Docker can download the ConvertX image automatically.

Make sure **Docker Desktop is running**.

Then open **PowerShell** and run:

```powershell
docker pull ghcr.io/c4illin/convertx:latest
```

Docker will begin downloading the ConvertX image.

You may see messages such as:

```text
Pulling...
Downloading...
Pull complete
```

Wait until the download finishes.

> The ConvertX Docker image is relatively large because it includes multiple components required for file conversion.

---

## 4. Verify the ConvertX Image

After the download is complete, run:

```powershell
docker images
```

Look for:

```text
ghcr.io/c4illin/convertx
```

with the tag:

```text
latest
```

For example:

```text
REPOSITORY                    TAG
ghcr.io/c4illin/convertx      latest
```

If the ConvertX image appears in the list, the download was successful.

---

## 5. Create a Folder for ConvertX Data

Create the following folder on drive `D:`:

```text
D:\Programs\ConvertX\data
```

Your folder structure should look like:

```text
D:\
└── Programs
    └── ConvertX
        └── data
```

ConvertX will use this folder to store its persistent application data.

> This folder is different from the Docker image storage configured earlier.
>
> Docker's image/container storage may be located in `D:\DockerData`, while ConvertX application data is stored in `D:\Programs\ConvertX\data`.

---

## 6. Create and Start the ConvertX Container

Make sure **Docker Desktop is running**.

Open **PowerShell** and run:

```powershell
docker run -d --name convertx -p 127.0.0.1:3000:3000 -v "D:\Programs\ConvertX\data:/app/data" ghcr.io/c4illin/convertx:latest
```

This command creates a Docker container named:

```text
convertx
```

### What Does This Command Mean?

```text
docker run
```

Creates and starts a Docker container.

```text
-d
```

Runs ConvertX in the background.

```text
--name convertx
```

Names the container `convertx`.

```text
-p 127.0.0.1:3000:3000
```

Makes ConvertX available locally on your computer through port `3000`.

The address:

```text
127.0.0.1
```

means **your own computer**.

```text
-v "D:\Programs\ConvertX\data:/app/data"
```

Connects the local ConvertX data folder on drive `D:` to the data folder inside the container.

```text
ghcr.io/c4illin/convertx:latest
```

Uses the ConvertX image downloaded earlier.

---

## 7. Verify the ConvertX Container

Run:

```powershell
docker ps
```

You should see a container named:

```text
convertx
```

with a status similar to:

```text
Up ...
```

You should also see a port mapping similar to:

```text
127.0.0.1:3000->3000/tcp
```

For example:

```text
NAMES       STATUS        PORTS
convertx    Up ...        127.0.0.1:3000->3000/tcp
```

If the status shows `Up`, ConvertX is running successfully.

---

## 8. Open ConvertX

Open your web browser.

Go to:

```text
http://localhost:3000
```

You can also use:

```text
http://127.0.0.1:3000
```

Both addresses point to ConvertX running locally on your computer.

> `localhost` does not mean that your files are being uploaded to an online ConvertX website.
>
> In this setup, your browser is connecting to the ConvertX container running on your own computer.

---

## 9. Create Your Local ConvertX Account

The first time you open ConvertX, you will see:

```text
Welcome to ConvertX!
Create your account
```

Create an email-style username and password for your local ConvertX installation.

For additional privacy, you do not need to use your real personal or work email address.

For example:

```text
admin@convertx.local
```

Create a **unique password** that you do not use for your Google, Microsoft, GitHub, work, banking, or other important accounts.

Then click:

```text
Create account
```

> This account belongs to your local ConvertX installation. Keep the login information somewhere safe.

---

## 10. Convert a File

After signing in to ConvertX, select or drag the file you want to convert.

For example:

```text
document.docx
      ↓
   ConvertX
      ↓
document.pdf
```

Select the available output format and start the conversion.

Depending on the source file and supported conversion method, ConvertX can work with document formats such as:

```text
DOCX
XLSX
PPTX
PDF
```

> Conversion quality depends on the source and destination formats.
>
> For example, converting DOCX, XLSX, or PPTX to PDF is generally more straightforward than reconstructing an editable Office document from a PDF.

---

## 11. Stop ConvertX

You do not need to keep ConvertX running when you are not using it.

To stop ConvertX, open **PowerShell** and run:

```powershell
docker stop convertx
```

The container and your ConvertX data will remain on your computer.

This does **not** uninstall ConvertX.

---

## 12. Start ConvertX Again

The next time you want to use ConvertX:

1. Open **Docker Desktop**.
2. Wait until Docker is running.
3. Open **PowerShell**.
4. Run:

```powershell
docker start convertx
```

5. Open your browser and go to:

```text
http://localhost:3000
```

You do **not** need to run `docker pull` or `docker run` again.

---

## Installation Complete

Your local setup should now look approximately like:

```text
Windows
│
├── Docker Desktop
│   │
│   └── ConvertX Container
│        │
│        └── 127.0.0.1:3000
│
├── D:\DockerData
│   └── Docker images and containers
│
└── D:\Programs\ConvertX\data
    └── ConvertX persistent application data
```

You can now convert supported files locally without relying on a third-party online conversion website.
