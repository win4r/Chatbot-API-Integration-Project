# Chatbot API Integration Project

This project demonstrates how to transition a traditional chatbot, initially interacted with through Selenium, to a more scalable and robust API-driven model. By leveraging Flask-SocketIO, this transformation enhances the chatbot's responsiveness and allows for real-time interaction without the overhead of a browser interface.

## Project Overview

Originally, the chatbot was controlled via a Selenium-driven script that simulated user interactions directly in a web browser. This approach, while straightforward, does not scale well and is limited by the performance of the web browser and the visibility of the web elements. To address these limitations, this project introduces an API layer, enabling direct communication with the chatbot backend without the need for a graphical interface.

## Technology Stack

- **Flask**: A lightweight WSGI web application framework in Python, used to create the API.
- **Flask-SocketIO**: Facilitates real-time bi-directional communications between the clients and the server.
- **Selenium**: Previously used for automating web browsers, now phased out from direct chatbot interaction but still useful for certain automated tasks in the project.
- **JavaScript (with Socket.IO client)**: Handles real-time communication on the client side, allowing users to interact with the chatbot through a web interface.

## Getting Started

### Prerequisites

Before you can run this project, you will need:

- Python 3.6+
- pip (Python package installer)

### Installation

1. **Clone the Repository:**

   ```
   git clone https://github.com/yourusername/chatbot-api-integration.git
   cd chatbot-api-integration
   ```

2. **Set up a Virtual Environment (optional but recommended):**

   ```
   python -m venv venv
   source venv/bin/activate  # On Windows use `venv\Scripts\activate`
   ```

3. **Install Required Python Packages:**

   ```
   pip install flask flask-socketio
   ```

4. **Run the Application:**

   ```
   python app.py
   ```

   This command starts the Flask server with Socket.IO integration.

### Usage

Once the server is running, you can open a web browser and visit `http://localhost:5000` to interact with the chatbot via the provided user interface. The UI allows you to send messages to the chatbot and receive responses in real-time.

## Features

- **Real-Time Interaction**: Users can communicate with the chatbot without delay, as messages are transmitted over WebSockets using Flask-SocketIO.
- **API-Driven**: Removes the dependency on a physical or simulated browser, enhancing performance and reliability.
- **Scalability**: Easier to scale the backend for handling multiple simultaneous user sessions.

## Contributing

Contributions are what make the open-source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

Distributed under the MIT License. See `LICENSE` for more information.

## Buy Me a Coffee
[!["Buy Me A Coffee"](https://storage.ko-fi.com/cdn/kofi2.png?v=3)](https://ko-fi.com/aila)
