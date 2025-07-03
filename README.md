# Spring Boot WebSocket Real-Time Application

A Spring Boot application demonstrating real-time communication using WebSockets. The application broadcasts timed messages to all connected clients using Java WebSocket API and displays them in a React-based web interface.

## 🚀 Features

- **Real-time WebSocket Communication**: Server broadcasts messages to all connected clients
- **Scheduled Broadcasting**: Automatic message broadcasting every 5 seconds using Spring's `@Scheduled` annotation
- **React Frontend**: Interactive web interface using React with JSX
- **RESTful API**: Status endpoint for server health checks
- **Connection Management**: Automatic handling of WebSocket connections, disconnections, and errors

## 📋 Prerequisites

Before running this application, make sure you have the following installed:

- **Java 8** or higher
- **Maven 3.6+**
- **Modern web browser** with WebSocket support

## 🛠️ Technologies Used

- **Spring Boot 2.3.1** - Main framework
- **Spring WebSocket** - WebSocket support
- **Java WebSocket API** - Server-side WebSocket endpoints
- **React 16** - Frontend framework
- **Babel** - JSX transpilation
- **Maven** - Build and dependency management

## 📦 Dependencies Fixed

The project required an additional dependency to compile successfully:

```xml
<dependency>
    <groupId>javax.websocket</groupId>
    <artifactId>javax.websocket-api</artifactId>
    <version>1.1</version>
    <scope>provided</scope>
</dependency>
```

This dependency provides the `ServerEndpointExporter` class needed for WebSocket configuration.

## 📦 Project Structure

```
spring-sockets-rt/
├── src/
│   ├── main/
│   │   ├── java/edu/eci/arsw/spring_sockets_rt/
│   │   │   ├── App.java                    # Simple main class
│   │   │   ├── WSStartApp.java             # Spring Boot main application
│   │   │   ├── WebController.java          # REST controller
│   │   │   ├── components/
│   │   │   │   └── TimedMessageBroker.java # Scheduled message broadcaster
│   │   │   ├── configuration/
│   │   │   │   └── WSConfigurator.java     # WebSocket configuration
│   │   │   └── endpoints/
│   │   │       └── TimerEndpoint.java      # WebSocket endpoint
│   │   └── resources/
│   │       ├── application.properties       # Application configuration
│   │       └── static/
│   │           ├── index.html              # Main HTML page
│   │           └── js/
│   │               └── WsComponent.jsx     # React WebSocket client
│   └── test/
│       └── java/edu/eci/arsw/spring_sockets_rt/
│           └── AppTest.java                # Unit tests
├── pom.xml                                 # Maven configuration
└── README.md                              # This file
```

## 🔧 Installation & Setup

### 1. Clone the repository

```bash
git clone https://github.com/AnderssonProgramming/spring-sockets-rt.git
cd spring-sockets-rt
```

### 2. Install dependencies

The project uses Maven for dependency management. All required dependencies will be downloaded automatically during the build process.

### 3. Build the project

```bash
mvn clean compile
```

### 4. Run the application

```bash
mvn spring-boot:run
```

Alternative method using the main class:

```bash
mvn exec:java -Dexec.mainClass="edu.eci.arsw.spring_sockets_rt.WSStartApp"
```

The application will start on **port 8081** (configured in `application.properties`).

## 🚀 Usage

### Starting the Server

1. Run the application using one of the methods above
2. The server will start on `http://localhost:8081`
3. You should see logs indicating successful startup and scheduled broadcasting

### Accessing the Web Interface

1. Open your web browser
2. Navigate to `http://localhost:8081`
3. The page will automatically connect to the WebSocket endpoint
4. You should see real-time messages being received from the server

### API Endpoints

#### REST Endpoints

- **GET** `/status` - Returns server status with current date and time

#### WebSocket Endpoints

- **WS** `/timer` - WebSocket endpoint for real-time message broadcasting

## ✅ Verification Checklist

After following the setup instructions, verify your application is working correctly:

### 1. Compilation Success
- [x] **Fixed Dependencies**: Added `javax.websocket-api` dependency to resolve compilation errors
- [x] **Clean Build**: `mvn clean compile` executes without errors
- [x] **Tests Pass**: `mvn test` runs successfully

### 2. Application Startup
- [x] **Server Starts**: Application starts on port 8081
- [x] **Scheduled Tasks**: Broadcasting logs appear every 5 seconds
- [x] **WebSocket Endpoint**: `/timer` endpoint is available

### 3. REST API Functionality
- [x] **Status Endpoint**: `GET /status` returns JSON with server information
- [x] **Response Format**: `{"status":"Greetings from Spring Boot [timestamp]. The server is Running!"}`

### 4. WebSocket Real-time Communication
- [x] **Frontend Connection**: React component connects to `ws://localhost:8081/timer`
- [x] **Message Reception**: Real-time messages display in the browser
- [x] **Multiple Clients**: All connected clients receive the same messages simultaneously

### 5. React Frontend
- [x] **Page Loading**: `http://localhost:8081` loads the HTML page
- [x] **React Mounting**: Component displays "Loading..." then switches to real-time messages
- [x] **Error Handling**: Proper error states for connection failures

## 🔍 How It Works

### Server-Side Components

1. **WSConfigurator**: Configures WebSocket support and enables scheduling
2. **TimerEndpoint**: Handles WebSocket connections and manages client sessions
3. **TimedMessageBroker**: Broadcasts messages every 5 seconds to all connected clients
4. **WebController**: Provides REST API endpoints

### Client-Side Components

1. **React Component**: Connects to WebSocket and displays received messages
2. **Connection Management**: Handles connection states and errors

### Message Flow

1. Server starts and begins scheduled broadcasting every 5 seconds
2. Client connects to WebSocket endpoint `/timer`
3. Server adds client session to the connection queue
4. Server broadcasts time messages to all connected clients
5. Client receives and displays messages in real-time

## 🛡️ Error Handling

The application includes comprehensive error handling:

- **Connection Errors**: Automatic cleanup of failed connections
- **Session Management**: Proper addition and removal of client sessions
- **Frontend Error States**: React component handles loading and error states

## 📝 Configuration

### Application Properties

The application uses default Spring Boot configuration. You can customize settings in `src/main/resources/application.properties`:

```properties
# Server port (default: 8081)
server.port=8081

# Application name
spring.application.name=spring-sockets-rt

# Logging levels
logging.level.edu.eci.arsw.spring_sockets_rt=INFO
```

### Message Broadcasting Frequency

To change the message broadcasting interval, modify the `@Scheduled` annotation in `TimedMessageBroker.java`:

```java
@Scheduled(fixedRate = 5000) // Current: 5 seconds
```

## 🧪 Testing

### Run Unit Tests

```bash
mvn test
```

## 🧪 Testing

### Run Unit Tests

```bash
mvn test
```

### Verify Application is Running

After starting the application with `mvn spring-boot:run`, you should see:

1. **Successful Startup Messages**:
   ```
   Started WSStartApp in X.XXX seconds
   Tomcat started on port(s): 8081 (http)
   ```

2. **Scheduled Broadcasting Logs** (every 5 seconds):
   ```
   INFO --- [scheduling-1] e.e.a.s.components.TimedMessageBroker : broadcastingMessages
   ```

### Test WebSocket Functionality

1. **Open the Web Interface**:
   - Navigate to `http://localhost:8081` in your browser
   - You should see "Loading..." initially, then real-time messages

2. **Check Browser Console**:
   - Open Developer Tools (F12)
   - Check Console for WebSocket connection messages
   - Should see "In onMessage" logs every 5 seconds

3. **Test Multiple Connections**:
   - Open multiple browser tabs to `http://localhost:8081`
   - All tabs should receive the same messages simultaneously
   - Messages should display: "The time is now HH:mm:ss"

### REST API Testing

Test the status endpoint:

```bash
curl http://localhost:8081/status
```

Should return current date and time information.

### Manual Testing

1. Open multiple browser tabs/windows to `http://localhost:8081`
2. Verify all clients receive the same messages simultaneously
3. Close some tabs and verify remaining clients continue receiving messages
4. Check the browser console for WebSocket connection logs

## 🚨 Troubleshooting

### Common Issues

1. **Compilation Errors**: 
   - Ensure all dependencies are properly downloaded: `mvn clean install`
   - Check Java version compatibility

2. **WebSocket Connection Failed**:
   - Verify server is running on port 8081
   - Check firewall settings
   - Ensure WebSocket URL is correct: `ws://localhost:8081/timer`

3. **No Messages Received**:
   - Check server logs for scheduled task execution
   - Verify WebSocket connection is established
   - Check browser console for JavaScript errors

### Logs

The application provides detailed logging. Check the console output for:
- Connection establishment/closure messages
- Scheduled broadcasting logs
- Error messages and stack traces

## 🔮 Future Enhancements

Potential improvements for this application:

- [ ] Add user authentication and session management
- [ ] Implement custom message types and routing
- [ ] Add database persistence for message history
- [ ] Include unit and integration tests for WebSocket functionality
- [ ] Add Docker containerization
- [ ] Implement message queuing for better scalability
- [ ] Add WebSocket connection monitoring and metrics

## 🤝 Contributing

1. Fork the project
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📞 Support

If you encounter any issues or have questions, please:

1. Check the troubleshooting section above
2. Review the server logs for error messages
3. Create an issue in the project repository

---

**Happy coding! 🎉**