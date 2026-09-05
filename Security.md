# Security and Privacy Notes

This guide is designed around running ConvertX locally on your own computer.

## Local Access

The Docker command used in this guide binds ConvertX to:

```text
127.0.0.1:3000
```

`127.0.0.1` is the loopback address of your own computer.

The guide intentionally uses:

```powershell
-p 127.0.0.1:3000:3000
```

rather than exposing ConvertX more broadly.

## Do Not Expose ConvertX Publicly

If you are processing private documents, do not expose the ConvertX service using:

- Cloudflare Tunnel
- ngrok
- Router port forwarding
- Public IP addresses

unless you understand the associated security risks and have configured appropriate protections.

## Passwords

Use a unique password for your local ConvertX account.

Do not reuse passwords from:

- Email
- Microsoft
- Google
- GitHub
- Work accounts
- Banking accounts

## Local Does Not Mean Malware-Proof

Running a converter locally can improve privacy by avoiding third-party upload services.

However, local processing does not guarantee that an unknown or malicious file is safe.

Keep Docker Desktop, ConvertX, Windows, and other relevant software updated.

## Backups

Keep backups of important documents before performing conversions.
