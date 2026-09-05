# Useful commands for troubleshooting

This page contains common problems you may encounter while installing or running ConvertX.

## Docker Command Is Not Recognized

If:

```powershell
docker --version
```

returns an error such as:

```text
docker is not recognized...
```

make sure Docker Desktop is installed and restart PowerShell.

---

## Cannot Connect to Docker

If Docker commands report that they cannot connect to the Docker daemon or engine:

1. Open Docker Desktop.
2. Wait for Docker Desktop to finish starting.
3. Try the command again.

---

## ConvertX Does Not Appear in `docker ps`

Run:

```powershell
docker ps -a
```

This displays containers even if they are stopped.

Check the status of:

```text
convertx
```

To view its logs:

```powershell
docker logs convertx
```

---

## localhost:3000 Does Not Open

First check whether ConvertX is running:

```powershell
docker ps
```

Look for:

```text
convertx
```

If it is stopped, run:

```powershell
docker start convertx
```

Then try:

```text
http://localhost:3000
```

again.

---

## Port 3000 Is Already in Use

Another application may already be using port 3000.

You can create ConvertX using another local port, for example:

```powershell
-p 127.0.0.1:3001:3000
```

Then open:

```text
http://localhost:3001
```

---

## ConvertX Container Stops Unexpectedly

Check the logs:

```powershell
docker logs convertx
```

The logs may provide information about why the container stopped.

---

## I Closed PowerShell and ConvertX Still Works

This is normal.

ConvertX was created using:

```text
-d
```

which tells Docker to run the container in the background.

You can stop it with:

```powershell
docker stop convertx
```
