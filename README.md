## Smart Refrigerator System (Raspberry Pi + YOLOv11 + AWS)

## Overview

The Smart Refrigerator System is an edge-computing and cloud-integrated inventory management platform that uses computer vision to detect food items in real time and synchronize inventory data to AWS services.

The system performs local object detection on a Raspberry Pi 4 using YOLOv11 and OpenCV, publishes inventory updates securely via MQTT to AWS IoT Core, processes updates with AWS Lambda, stores records in DynamoDB, and exposes inventory data through a REST API consumed by a mobile application built with MIT App Inventor.

This project demonstrates a full edge-to-cloud distributed architecture.

## System Architecture

Edge Layer (Raspberry Pi 4)
Pi Camera captures real-time images.
YOLOv11 model performs object detection locally.
Detected items (milk, eggs, apples, oranges, gatorade) are counted per frame.
A Python script publishes inventory updates via MQTT (TLS encrypted).
JSON payload includes: Item name, Quantity, Timestamp (ISO format with timezone)

## Cloud Layer (AWS)
AWS IoT Core
Receives MQTT messages securely over TLS.
Routes messages to AWS Lambda.
Lambda Function #1 - Inventory Update
Parses incoming JSON payload.
Updates corresponding record in DynamoDB.
Handles quantity increments.
DynamoDB
Stores real-time inventory state.
Maintains item quantity and timestamps.
Lambda Function #2 - Inventory API
Triggered via AWS API Gateway.
Returns full inventory and JSON response.
AWS API Gateway
Hosts public HTTP endpoint.
Enables external access to fridge inventory.

## Mobile Layer

MIT App Inventor Application
Sends HTTP requests to API Gateway endpoint.
Retrieves live inventory JSON.
Displays real-time fridge contents.
Supports alert and update notifications.

## Technologies Used

Edge Computing
Python
OpenCV
YOLOv11 (Ultralytics)
Picamera2
NumPy
Secure MQTT (paho-mqtt)
TLS v1.2 encryption

Cloud Services
AWS IoT Core
AWS Lambda (2 functions)
AWS DynamoDB
AWS API Gateway
JSON-based REST APIs

Mobile
MIT App Inventor
HTTP Web Extension
MQTT Extension

## Key Features
Real-time object detection (92% average accuracy)
Secure MQTT communication over TLS
Serverless cloud processing
DynamoDB inventory persistence
Public REST API endpoint
Mobile app integration
End-to-end latency: 5-10 seconds
Continuous frame-rate optimized interference loop

## Engineering Concepts Demonstrated
Edge AI interference on embedded Linux device
Event-driven cloud architecture
Secure IoT communication (TLS certificates)
Serverless backend design
REST API development
Distributed system integration
Mobile-cloud synchronization
