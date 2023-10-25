# Environmental-Monitoring

# IoT Project: Environmental Monitoring

## Abstract Idea

The field of environmental monitoring has become increasingly critical in the face of escalating climate change and resource depletion. Leveraging the capabilities of the Internet of Things (IoT) offers a promising solution to address environmental challenges effectively.

## Understanding of the Problem

The problem in IoT-based environmental monitoring is the lack of real-time data, connectivity in remote areas, data analysis capabilities, and tools for sustainability planning. Addressing these issues is crucial for effective environmental monitoring, decision-making, and regulatory compliance while involving and educating communities.

## Problem Definition

The problem at hand revolves around the urgent need to monitor, manage, and mitigate environmental issues such as air and water pollution, deforestation, wildlife conservation, and climate change. Traditional methods of data collection and management are often inadequate, expensive, and inefficient. This leads to delayed responses to environmental crises, hindering sustainability efforts.

## Design Thinking Approach

To tackle these challenges, a design thinking approach can be adopted. This involves empathizing with stakeholders, defining the problem, ideating solutions, prototyping, and testing. In the context of IoT-based environmental monitoring:

1. **Empathize:**
   - Understand the needs and concerns of environmental organizations, regulatory bodies, scientists, and communities affected by environmental issues. Identify their pain points and requirements for data and information.

2. **Define:**
   - Clearly articulate the problems, such as insufficient real-time environmental data, limited connectivity in remote areas, and the lack of actionable insights. Prioritize these problems based on impact and feasibility.

3. **Ideate:**
   - Generate creative ideas for IoT solutions, including sensor networks, data analytics, and communication technologies. Consider how these solutions can enhance data collection, improve decision-making, and promote sustainability.

4. **Prototype:**
   - Develop prototypes or proof-of-concept systems that demonstrate the feasibility of IoT solutions. Test these prototypes in real-world scenarios to refine their functionality and reliability.

5. **Test:**
   - Gather feedback from users, environmental experts, and stakeholders to refine the prototypes further. Ensure that the solutions align with the identified problems and address the specific needs of the environmental monitoring context.





# Phase 2: Innovation - Transforming Design into Reality

## Introduction

The Innovation phase is the pivotal step in converting our design thinking ideas into a tangible IoT-based environmental management solution. This document outlines the comprehensive steps that will be taken to bring our design concept into practice.

## Step 1: Refine Problem Definition

- **Review Problem Statement:**
  - Revisit the problem statement to ensure clarity and relevance.
- **Gather Additional Insights:**
  - Consult with stakeholders, environmental experts, and target communities to gather more insights.

## Step 2: Define Technical Requirements

- **Sensor Selection:**
  - Determine the types of sensors required for data collection (e.g., air quality, water quality, temperature, humidity, etc.).
- **Data Storage:**
  - Decide on the data storage solutions (local or cloud-based databases) and data management tools.
- **Communication Protocols:**
  - Choose the appropriate communication protocols for data transmission (e.g., LoRa, NB-IoT, or cellular networks).
- **Data Analysis Tools:**
  - Identify the data analysis tools and algorithms to be used for deriving actionable insights.

## Step 3: Develop Hardware and Software

**Hardware Development:**

- Identify IoT hardware components (sensors, microcontrollers, communication modules).
- Create a detailed hardware architecture diagram.
- Source the required hardware components.
- Assemble and test the hardware components.

**Software Development:**

- Develop firmware for microcontrollers to collect and transmit data.
- Develop server-side software for data reception, storage, and analysis.
- Create a user interface (UI) for data visualization and user interaction.
- Ensure data security and privacy measures are implemented.

## Step 4: Prototyping

- **Create Prototypes:**
  - Build a prototype system with a limited set of sensors.
  - Test the prototype in controlled environments.
  - Refine the hardware and software based on initial testing.

## Step 5: Real-world Testing

- **Deploy Prototypes in Real Environments:**
  - Install prototypes in target environmental monitoring locations.
  - Monitor and collect real-time data over an extended period.
  - Address technical issues and refine the system based on field testing results.

## Step 6: User Feedback

- **Gather User Feedback:**
  - Engage with stakeholders and user groups for feedback.
  - Identify areas for improvement and additional features.
  - Iteratively refine the system based on feedback.

## Step 7: Data Analysis and Insights

- **Data Analysis:**
  - Use collected data to analyze environmental conditions and trends.
  - Apply machine learning and AI algorithms for predictive analysis.
  - Generate actionable insights and reports for decision-makers.

## Step 8: Sustainability and Community Engagement

- **Community Involvement:**
  - Implement community engagement programs, educational initiatives, and awareness campaigns.
  - Enable community members to access and interpret environmental data.
  - Promote sustainable practices based on insights.

## Step 9: Regulatory Compliance

- **Ensure Regulatory Compliance:**
  - Implement features to facilitate compliance reporting.
  - Collaborate with regulatory bodies to ensure data accuracy and alignment with regulations.

## Step 10: Documentation and Reporting

- **Document the Entire Process:**
  - Create detailed documentation for hardware and software components.
  - Prepare reports on field testing, user feedback, and data analysis.
  - Share findings and progress with stakeholders and project sponsors.

## Conclusion

The Innovation phase is a crucial step in turning our design thinking concept into a practical solution for IoT-based environmental management. By following these structured steps, we aim to address environmental challenges effectively and make a positive impact on sustainability efforts.

# IOT-PHASE 3
# Development Part 1
## CODE:
#include <WiFi.h>
#include <HTTPClient.h>
#include <DHT.h>
const char* ssid = "Your_SSID";
const char* password = "Your_Password";
const char* serverUrl = "https://smartenviron.free.beeceptor.com/smartenviron/";
#define DHTPIN 4
#define DHTTYPE DHT22
DHT dht(DHTPIN, DHTTYPE);
const unsigned long INTERVAL = 60000; // Send data every 1 minute
unsigned long previousMillis = 0;
float temperature = 0.0;
float humidity = 0.0;
void setup() {
  Serial.begin(9600);
  Serial.print("Connecting to WiFi");
 // Attempt to connect to WiFi
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    Serial.print(".");
    delay(1000); // Wait for 1 second before retrying
  }
if (WiFi.status() == WL_CONNECTED) {
    Serial.println(" Connected!");
    dht.begin();
  } else {
    Serial.println(" WiFi not connected.") }
}void loop() {
  if (WiFi.status() != WL_CONNECTED) {
    // WiFi is not connected, you can handle this scenario as needed
    Serial.println("WiFi not connected. Reconnecting...");
    connectToWiFi();
  } else {
    unsigned long currentMillis = millis();
    if (currentMillis - previousMillis >= INTERVAL) {
      previousMillis = currentMillis;
    float newTemperature = dht.readTemperature();
      float newHumidity = dht.readHumidity();
     if (!isnan(newTemperature) && !isnan(newHumidity)) {
        // Only send data if there's a significant change
        if (abs(newTemperature - temperature) >= 0.5 || abs(newHumidity - humidity) >= 1.0) {
          temperature = newTemperature;
          humidity = newHumidity;
          sendSensorData();
        }
      } else {
        Serial.println("Failed to read from DHT sensor!");
      } }}}
void connectToWiFi() {
  WiFi.begin(ssid, password);
 while (WiFi.status() != WL_CONNECTED) {
    Serial.print(".");
    delay(1000); // Wait for 1 second before retrying
  }
if (WiFi.status() == WL_CONNECTED) {
    Serial.println("WiFi reconnected!");
  }}
void sendSensorData() {
  // The rest of your sendSensorData function remains the same}
 
## OUTPUT:

 

## CODE DISCRIPTION:
This Arduino sketch is designed to create a robust environment monitoring system. It utilizes a DHT22 sensor to capture temperature and humidity data and wirelessly transmits this data to a designated server via Wi-Fi. The core functionalities encompass Wi-Fi network connectivity, sensor data acquisition, and periodic data transmission.
## Initialization and Wi-Fi Connection:
The sketch starts by initializing the Serial communication for debugging purposes with a baud rate of 9600.It then attempts to connect to a Wi-Fi network using the provided SSID (Service Set Identifier) and password.During the connection process, the sketch displays a series of dots to indicate the connection status. If a connection is established, it informs the user with a "Connected!" message. If not, it signals that Wi-Fi is not connected.
## Main Loop:
The primary loop continually checks the Wi-Fi connection status. If the connection is lost, it enters a reconnection phase, calling the connectToWiFi() function.When the Wi-Fi connection is stable, the sketch monitors the time elapsed since the last data transmission. It waits for a specified interval (in this case, one minute) before checking the sensor for new temperature and humidity readings.If fresh data is available and is significantly different from the previous readings (with predefined thresholds of 0.5°C for temperature and 1.0% for humidity), it proceeds to send the updated data to the server.

## Wi-Fi Reconnection Function (connectToWiFi):
This function is responsible for reconnecting to the Wi-Fi network in case of a connection loss.
It employs a loop to repeatedly attempt connection and displays progress dots.
When a successful reconnection occurs, it prints "WiFi reconnected!".
Data Transmission Function (sendSensorData):
This function constructs a URL to the designated server, incorporating the temperature and humidity data as query parameters.
It initiates an HTTP GET request to the server using the HTTPClient library.The function then evaluates the HTTP response code to confirm the success of the transmission.In the event of success, it prints the server's response.If the HTTP request fails, it reports an error code.

# ADDITIONAL  FEATURES:
## Error Handling: Improve error handling to handle network or server issues gracefully.
## Modularize Code: Break the code into smaller functions for better organization and readability.
## Minimize String Usage: Avoid using the String class, as it can cause memory fragmentation on microcontrollers. Use character arrays (char[]) for data instead.
## Reduce HTTP Requests: Instead of sending data in every loop iteration, consider sending data at longer intervals or only when there's a significant change in sensor values.


