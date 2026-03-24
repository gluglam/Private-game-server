# Minecraft Server Setup

Minecraft Java Edition server created for private use in June 2025.

## About the project

This documentation was prepared about a year after the server was created and on a different computer. Because of that, the screenshots are included only to demonstrate familiarity with the completed steps.

The project was created so that players could play together on a private Minecraft server, both inside the same local network and from different networks.

## Features

- private Minecraft Java Edition game server
- local access through `localhost`
- external access through public IP address and a forwarded port
- static IPv4 configuration for stable routing
- Windows Firewall configuration for inbound and outbound traffic

## Table of contents

- [Minecraft Server Setup](#minecraft-server-setup)
  - [About the project](#about-the-project)
  - [Features](#features)
  - [Table of contents](#table-of-contents)
  - [Technologies](#technologies)
  - [Downloading the server package](#downloading-the-server-package)
  - [Server installation](#server-installation)
  - [Connection test](#connection-test)
  - [Configuration for devices outside the LAN](#configuration-for-devices-outside-the-lan)
    - [1. Configure firewall rules](#1-configure-firewall-rules)
    - [2. Configure a static IP address](#2-configure-a-static-ip-address)
    - [3. Update `server.properties`](#3-update-serverproperties)
    - [4. Configure port forwarding on the router](#4-configure-port-forwarding-on-the-router)
    - [5. Check the public IP address](#5-check-the-public-ip-address)
  - [Sources](#sources)

## Technologies

- Minecraft Launcher
- Java
- Windows Command Prompt
- Windows Firewall
- static IPv4 addressing
- NAT/PAT
- port forwarding
- `server.properties`
- router configuration

## Downloading the server package

To set up the server, the `server.jar` file is required.

1. Open the **Minecraft Launcher** application.
2. Go to the **Installations** tab.
3. Select the installation of the game version on which you want to set up the server.
4. Click the **three-dot icon** and choose **Edit**.
5. Click the **SERVER** link to download the server package.

![Minecraft Launcher](images/image1.png)
![Installation edit view](images/image2.png)
![Server download link](images/image3.png)

## Server installation

> [!WARNING]
> Before continuing, make sure that the latest version of **Java** is installed on the device.
> If it is not installed, download it from the official website:
> https://www.java.com/pl/download/

You can verify the Java version in Command Prompt with:

```bash
java -version
```

![Java version check](images/image4.png)

The server installation process is as follows:

1. Create a new folder and move the `server.jar` file into it.
2. Run `server.jar` once so that the initial files and directories are generated.
3. Open the `eula.txt` file, change:
   ```txt
   eula=false
   ```
   to:
   ```txt
   eula=true
   ```
4. Save the file and run `server.jar` again.
5. The server should now start locally on the device.

By default, the Minecraft server runs on port `25565`.

![Server folder](images/image5.png)
![Generated files and directories](images/image6.png)
![EULA accepted](images/image7.png)
![Local server startup](images/image8.png)

## Connection test

To connect to the server from the client application:

1. Launch Minecraft in the correct game version, in this case **1.21.7**.
2. Open **Multiplayer**.
3. Enter the server address in the format:

```txt
localhost:25565
```

template:

```txt
localhost:[server port]
```

![Add server screen](images/image9.png)
![Multiplayer connection setup](images/image10.png)

Successful connection views:

- client application after a successful connection
- server console after a successful connection with the client

![Client connected to the server](images/image11.png)

## Configuration for devices outside the LAN

To allow players outside the local network to connect to the server, the following steps must be completed.

### 1. Configure firewall rules

Create inbound rules for the server traffic in **Windows Firewall**. The outbound rule is configured in the same way.

![Inbound rule step 1](images/image12.png)
![Inbound rule step 2](images/image13.png)
![Inbound rule step 3](images/image14.png)
![Inbound rule step 4](images/image15.png)
![Inbound rule step 5](images/image16.png)
![Inbound rule step 6](images/image17.png)
![Created firewall rule](images/image18.png)
![Outbound rule configured the same way](images/image19.png)

### 2. Configure a static IP address

A static IP address should be configured both on the router and on the server device.

**Static address on the router**

![Static address on the router](images/image20.png)
![Router DHCP reservation / address details](images/image21.png)

**Static IPv4 address on the server**

![Static IPv4 configuration on Windows](images/image22.png)

Verify the address with:

```bash
ipconfig
```

![IP verification with ipconfig](images/image23.png)

### 3. Update `server.properties`

In the `server.properties` file, enter the local address of the server.

![server.properties configuration](images/image24.png)

### 4. Configure port forwarding on the router

Forward the appropriate external port to the server device and the Minecraft server port.

![Port forwarding configuration](images/image25.png)
![Forwarded port summary](images/image26.png)

### 5. Check the public IP address

Check the public IP address that external players will use to connect.

Command:
```txt
nslookup myip.opendns.com resolver1.opendns.com
```

![Checking the public IP address](images/image27.png)

A client outside the local network should use the server address in the following format:

```txt
[public_ip]:[external_port]
```

## Sources

- https://minecraft.wiki/w/Tutorial:Setting_up_a_Java_Edition_server
