---
title: Quickstart - Add volume indicator to your Web calling app
titleSuffix: An Azure Communication Services quickstart
description: In this quickstart, you'll learn how to check call volume within your Web app when using Azure Communication Services.
author: sloanster

ms.author: micahvivion
ms.date: 1/18/2023
ms.topic: quickstart
ms.service: azure-communication-services
ms.subservice: calling
ms.custom: mode-other
---

# Accessing call volume level
As a developer you can have control over checking microphone volume in JavaScript. This quickstart shows examples of how to accomplish this within the ACS WebJS.

## Prerequisites
[!INCLUDE [Public Preview](../../includes/public-preview-include-document.md)]

>[!IMPORTANT]
> The quick start examples here are available starting on the public preview version [1.9.1-beta.1](https://www.npmjs.com/package/@azure/communication-calling/v/1.9.1-beta.1) of the calling Web SDK. Make sure to use that SDK version or newer when trying this quickstart.

## Checking the audio stream volume
As a developer it can be nice to have the ability to check and display to end users the current microphone volume. ACS calling API exposes this information using `getVolume`. The `getVolume` value is a number ranging from 0 to 100 (with 0 noting zero audio detected, 100 as the max level detectable). This value iss sampled every 200 ms to get near real time value of volume.

### Example usage
Sample code to get volume of selected microphone. This example shows how to generate the volume level by accessing `getVolume`.

```javascript
//Get the vaolume of the local audio source
const volumeIndicator = await new SDK.LocalAudioStream(deviceManager.selectedMicrophone).getVolume();
volumeIndicator.on('levelChanged', ()=>{
    console.log(`Volume is ${volumeIndicator.level}`)
})

//Get the volume level of the remote incoming audio source
const remoteAudioStream = call.remoteAudioStreams[0];
const volumeIndicator = await remoteAudioStream.getVolume();
volumeIndicator.on('levelChanged', ()=>{
    console.log(`Volume is ${volumeIndicator.level}`)
})

```

