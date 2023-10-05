# Port Scanning

## Purpose

- Identify Operating System
- Identify Services

## Identify Operating System

- Revealed by Signatures
- Revealed by Services

When trying to identify operating systems, we use our tools to send requests and wait for responses that will be analyzed to compare them to a signature database.

Some operating systems have very obvious signatures, others not, but we will take our chances when scanning.

## Scan for services

- Try to connect to different ports.
- Check for responses.

Nmap and other port scanning tools use the tcp handshake to know if the connection if possible and a service is running. It has also a stealthy scan where the three way handshake is started but not finished.

## Service enumeration

To perform service enumeration, nmap will grab the banner after the three way handshake instead of closing the connection right away, and then it will drop the connection. Service enumeration is very lousy, but it is ok to perfom it if it doesn't break things.

## Connect to UDP

- Slower.
- Can be open or filtered, if filtered, the connection was not dropped but we don't really know the real state of the connection port.
- Can be sped up with certain flags.

## Nmap

Check for the man page, it is very interesting and complete.

**Note**: NSE is the Nmap Scripting Engine.

## Other tools

- Zenmap - GUI NMAP
- Nmap Automator - Based on the network we scan, it will perform more scans to continue enumeration.
- Masscan - Very fast port scanning, it works with mulithreading.
- Rustscan - Built with rust, works at a lower level, a pretty fast scanner.
- Autorecon - similar to nmap automator.
