# Introduction

[Home](../README.md) · [Section index](README.md)

> Adapted from the original notes, lines 67–77. Examples are lab-specific and need verification.

## What is information gathering?

Information gathering is the first phase of an assessment: building a picture of the target before touching it with anything intrusive. It splits into two types:

1. **Passive information gathering** — collecting data without directly interacting with the target (e.g., WHOIS lookups, search engines, public DNS records).
2. **Active information gathering** — directly interacting with the target to collect data (e.g., host discovery, port scanning).

## Where will I find the target IPs?

A natural first question is whether you can just read `/etc/hosts` for target IPs. In the INE labs used throughout this course, the IP addresses are provided for you. On the actual eJPT exam, however, you start from a host-discovery phase and have to find the targets yourself.

The `netdiscover` tool works well for this and is covered in the INE course material.
