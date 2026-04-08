# Notification Flowchart: A Beginner's Guide

This document provides a highly visual, beginner-friendly breakdown of how Push Notifications are set up and delivered in our space-ios application.

## The Two Main Services We Use
1. **Apple Push Notification service (APNs)** – The system built by Apple to send notifications to physical iOS devices.
2. **AWS SNS** – A middleman service that manages notifications from our backend server and routes them perfectly to Apple's APNs.

---

## The Flowchart

```mermaid
flowchart TD
    %% Styling for better readability
    classDef userAction fill:#E3F2FD,stroke:#1565C0,stroke-width:2px,color:#000
    classDef apple fill:#F5F5F5,stroke:#757575,stroke-width:2px,color:#000
    classDef aws fill:#FFF3E0,stroke:#E65100,stroke-width:2px,color:#000
    classDef backend fill:#E8F5E9,stroke:#2E7D32,stroke-width:2px,color:#000

    %% Registration Phase
    subgraph Phase 1: Setting up the connection
        direction TB
        Step1([📱 1. App asks user for notification permission]):::userAction --> Step2
        Step2([🍏 2. Apple gives the App a unique 'Device Token']):::apple --> Step3
        Step3([☁️ 3. App sends Token to AWS SNS]):::aws --> Step3b
        Step3b[AWS creates an 'Endpoint ARN' for the device]:::aws --> Step4
        Step4([💻 4. App sends the ARN to our Backend]):::backend --> Step4b
        Step4b[Backend links the ARN to the User's Profile]:::backend
    end

    %% Waiting
    Step4b -. "An event happens later (e.g., a Box is shipped)" .-> Step5

    %% Delivery Phase
    subgraph Phase 2: Sending a Notification
        direction TB
        Step5([🚀 5. Backend wants to send an alert]):::backend --> Step6
        Step6[Backend tells AWS SNS to notify the ARN]:::aws --> Step7
        Step7[AWS routes the message to Apple APNs]:::apple --> Step8
        Step8([🎉 User's iPhone displays the Notification!]):::userAction
    end
```

## Step-by-Step Summary
1. App asks user for notification permission.
2. Apple gives a device token to the app. 
3. App sends token to AWS SNS, which creates an endpoint ARN in AWS.
4. App sends ARN to backend and links it to user.
5. Backend uses ARN to send notifications via AWS SNS to user's device.
