# 🚦 Traffic Light Simulation with ASP.NET Core + C# Clients

This project simulates traffic light control logic with multiple car clients interacting in real-time via HTTP. It is built using ASP.NET Core Web API for the server and C# console clients for the drivers. Each car client can queue, wait for green lights, and attempt to pass through intersections with random crashes if traffic rules are violated.

---

## 🧩 Project Structure

```
├── Server.cs                   # Starts ASP.NET Core server (WebAPI)
├── TrafficLightController.cs   # HTTP API endpoints
├── TrafficLightLogic.cs        # Thread-safe traffic light and queue logic
├── Client.cs                   # Car simulator (driver loop with randomization)
├── TrafficLightClient.cs       # Auto-generated API client (NSwag)
```

---

## 🧠 Features

- 🚗 Multiple concurrent car clients
- 🟢🟥 Traffic light toggling (red/green) in a background thread
- 🧠 Thread-safe shared state using locks
- 📝 Client identity: car number, driver name, and unique car ID
- 🛑 Queuing logic based on red lights
- 🚦 Passing logic with crash simulation (if out-of-turn or red)
- 📜 Swagger docs enabled for testing API endpoints
- 🔁 Auto-recovery on client disconnection
- 📊 Logging with `NLog` for both server and clients

---

## 🖥️ How It Works

### 🧩 Server (`ASP.NET Core`)
- Hosts `/trafficLight` API with endpoints:
  - `GET /getUniqueId` — Assigns a unique car ID
  - `GET /getLightState` — Returns the current light color
  - `POST /queue` — Queues a car if light is red
  - `GET /isFirstInLine?carId=x` — Checks if a car is first in queue
  - `POST /pass` — Attempts to pass the light and returns success/failure

### 🚗 Client
- Randomly selects a name, surname, and car number
- Connects to the server, receives a unique ID
- Simulates driving, stopping at lights, queuing, or passing
- Waits for green and position in queue before attempting to pass
- Handles crashes due to red lights or queue jumping

---

## 🖼 Console Sample

```
13:00:01|INFO| I am car 5, RegNr. BVX 834, Driver Steve Jackson.
13:00:04|INFO| I am driving on the road.
13:00:07|INFO| I see a traffic light.
13:00:08|INFO| Light is red, trying to queue.
13:00:09|INFO| I'm in queue now. Waiting for light.
13:00:13|INFO| Light is green and I am ready, trying to pass.
13:00:13|INFO| Passed, life is good.
```

---

## 🚀 Getting Started

### ▶️ Server
1. Open the solution in Visual Studio or use CLI
2. Run `Server.cs`
3. Visit Swagger UI at: [http://localhost:5000/swagger](http://localhost:5000/swagger)

### 🚗 Client
1. Build and run `Client.cs` (can run multiple instances)
2. Each client connects to the server and participates as a car

---

## 🔧 Technologies

- C#
- ASP.NET Core Web API
- NSwag (for auto-generating API client)
- NLog (for logging)
- Threading and concurrency handling
