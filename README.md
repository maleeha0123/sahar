# Sahar Lifeline 🎯


## Basic Details
### Team Name: Irish women


### Team Members
- Member 1: Maleeha Nasseer - Mar Athanasius College of Engineering,Kothamangalam
- Member 2: Neeharika Niroup Gupta - Mar Athanasius College of Engineering,Kothamangalam

### Hosted Project Link
https://github.com/maleeha0123/sahar/edit/main/README.md

### Project Description
        Through our project we aim to create a secure, offline-first messaging app optimized for intermittent satellite communication, helping Afghan women stay connected in a highly censored and oppressive regime.Our web page represents a mobile app that can be downloaded in rudimentary phones, it simulates the movement of an emergency message from the user in a remote location , to a 'relay' persons ,through a mesh network ,the message hops from one node to next ,till the message reaches a node that has internet connectivity ,on reaching such a node, message is then transmitted to respective NGO.

### The Problem statement
      Since the Taliban’s takeover of Afghanistan in August 2021, women have faced systematic oppression at an unprecedented level. What were once basic freedoms—education, employment, movement, and even self-expression—have been stripped away in a brutal regression of rights.
         - Over 1.1 million girls are barred from secondary and university education.
         - Women are banned from most jobs, including government, NGOs, and even beauty salons.
         - Women cannot travel without a male guardian (mahram) and are banned from public parks, gyms, and restaurants.
         - The opressive Taliban regime has erased women from public life—including banning female voices from radio and TV.
         -  With no education or financial independence, early marriages have surged, leading to severe health and social consequences.
         - Reports show a rise in domestic abuse, forced marriages, and honor killings, with no legal protection for women.
         - While women elsewhere pursue careers, vote freely, drive, and travel independently, Afghan women are living in a prison without walls, deprived of the most basic human rights. What is normal and trivial for others—texting freely, choosing their future, or attending a university—is an impossible dream for Afghan women today.

### The Solution
In this dire situation,our secure messaging app is not just about technology—it’s a lifeline for Afghan women.
         - Even with restrictions, messaging can help Afghan women connect, share, and seek help.
         - In a country where private messages can be monitored, encryption ensures women can speak safely without fear of retribution.
         - This project highlights the dire reality of Afghan women and serves as a technological resistance against digital suppression.
       ##- NGOs operating in Afghanistan, especially those focused on women’s rights and humanitarian aid, face severe connectivity challenges due to a mix of political restrictions, infrastructure limitations, and security concerns.
         - The Taliban tightly controls internet access and monitors communication channels, making it difficult for NGOs to securely contact women.
         -  NGOs are often unable to receive urgent distress calls from women in danger.
    Our project gives a simulation of a mobile app that can be used in rudimentary phones, to send emergency messages to relays which then transmit the messages to respective NGOs using satellite services from partnered telecommunication companies.We hope to lend a hand to NGOs trying to reach people who are in need of dire necessities and help.  
    We used AES algorithm in code for encryption , to send the messages securely to relay and then to needed NGO.
## Technical Details
### Technologies/Components Used
For Software:
- HTML
- programs where stored with .html extension,and output was seen on default browser

### Implementation

# Run
### Below is the code for simulation of keypad,and sending of alphabetic and numeric values to relay and printing the time when the message was recieved after toggling connectivity ,then the messages are transmitted to needed NGO
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Emergency Communication Simulation</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f0f8ff;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            height: 100vh;
        }
        .keypad-container {
            text-align: center;
            background-color: #ffffff;
            border-radius: 10px;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
            padding: 30px;
            width: 320px;
            margin-bottom: 40px; /* Space between keypad and relay section */
        }
        .keypad-container h1 {
            color: #333;
        }
        .keypad-container button {
            padding: 20px;
            font-size: 20px;
            margin: 5px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            width: 60px;
            height: 60px;
        }
        .keypad-container button:hover {
            background-color: #45a049;
        }
        .output {
            margin-top: 20px;
            font-size: 16px;
            color: #333;
        }

        /* Relay and message queue styling */
        .status {
            margin-top: 20px;
            padding: 10px;
            color: white;
            border-radius: 5px;
            width: 300px;
            margin-left: auto;
            margin-right: auto;
        }
        .status.connected {
            background-color: #4CAF50;
        }
        .status.disconnected {
            background-color: #f44336;
        }
        .message-box {
            background-color: #ffffff;
            border-radius: 10px;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
            padding: 20px;
            margin-top: 20px;
            min-height: 150px;
            max-height: 300px;
            overflow-y: auto;
            width: 300px;
            margin-left: auto;
            margin-right: auto;
        }
        .message {
            background-color: #f9f9f9;
            margin: 5px 0;
            padding: 10px;
            border-radius: 5px;
        }
        .transmitting {
            color: #ff9800;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <!-- Keypad Section (Emergency Message Input) -->
    <div class="keypad-container">
        <h1>Sahar Lifeline</h1>
        <div class="output" id="outputMessage"></div>
        
        <div class="row">
            <button onclick="sendEmergencyMessage(1)">1</button>
            <button onclick="pressKey(2)">2<br>ABC</button>
            <button onclick="pressKey(3)">3<br>DEF</button>
        </div>
        <div class="row">
            <button onclick="pressKey(4)">4<br>GHI</button>
            <button onclick="pressKey(5)">5<br>JKL</button>
            <button onclick="pressKey(6)">6<br>MNO</button>
        </div>
        <div class="row">
            <button onclick="pressKey(7)">7<br>PQRS</button>
            <button onclick="pressKey(8)">8<br>TUV</button>
            <button onclick="pressKey(9)">9<br>WXYZ</button>
        </div>
        <div class="row">
            <button onclick="pressKey(0)">0</button>
        </div>
        
        <div class="row">
            <button onclick="sendMessage()">Send</button>
            <button onclick="clearMessage()">Clear</button>
        </div>
    </div>

    <!-- Relay Section (Message Queue and Connectivity) -->
    <div id="status" class="status disconnected">
        No connectivity
    </div>
    
    <div class="message-box" id="messageBox">
        <!-- Emergency messages will be listed here -->
    </div>
    
    <button onclick="simulateMessage()">Receive Message</button>
    <button onclick="simulateConnectivity()">Toggle Connectivity</button>
    <button onclick="sendMessages()">Send Messages to NGO</button>

    <script>
        let message = "";
        let lastKey = null;
        let keyPressCount = 0;
        let keyPressTimeout;
        const keyMappings = {
            2: "ABC",
            3: "DEF",
            4: "GHI",
            5: "JKL",
            6: "MNO",
            7: "PQRS",
            8: "TUV",
            9: "WXYZ"
        };
        const emergencyMessages = {
            1: "Rescue",
            2: "Medical",
            3: "Amenities"
        };

        // Emergency message functions
        function pressKey(key) {
            clearTimeout(keyPressTimeout);
            
            if (key === lastKey) {
                keyPressCount++;
            } else {
                if (lastKey !== null) {
                    message += keyMappings[lastKey][(keyPressCount - 1) % keyMappings[lastKey].length];
                }
                lastKey = key;
                keyPressCount = 1;
            }

            keyPressTimeout = setTimeout(() => {
                if (keyMappings[lastKey]) {
                    message += keyMappings[lastKey][(keyPressCount - 1) % keyMappings[lastKey].length];
                } else {
                    message += lastKey;
                }
                lastKey = null;
                keyPressCount = 0;
                document.getElementById("outputMessage").innerText = message;
            }, 3000);
        }

        function sendEmergencyMessage(key) {
            let emergencyText = emergencyMessages[key];
            if (emergencyText) {
                let asciiValues = emergencyText.split('').map(char => char.charCodeAt(0)).join(' ');
                document.getElementById("outputMessage").innerText = Emergency Message: ${emergencyText}\nASCII Values: ${asciiValues};
            }
        }

        function sendMessage() {
            if (message.trim() === "") {
                alert("Message cannot be empty");
                return;
            }
            let asciiValues = message.split('').map(char => char.charCodeAt(0)).join(' ');
            document.getElementById("outputMessage").innerText = Message Sent: ${message}\nASCII Values: ${asciiValues};
        }

        function clearMessage() {
            message = "";
            lastKey = null;
            keyPressCount = 0;
            document.getElementById("outputMessage").innerText = "";
        }

        // Relay and Message Queue Section
        let messageQueue = [];
        let isConnected = false;

        function simulateMessage() {
            const emergencyMessage = Emergency Request: ${new Date().toLocaleTimeString()};
            messageQueue.push(emergencyMessage);
            updateMessageBox();
        }

        function simulateConnectivity() {
            isConnected = !isConnected;
            const statusElement = document.getElementById("status");

            if (isConnected) {
                statusElement.innerText = "Connectivity Available";
                statusElement.classList.remove("disconnected");
                statusElement.classList.add("connected");
            } else {
                statusElement.innerText = "No Connectivity";
                statusElement.classList.remove("connected");
                statusElement.classList.add("disconnected");
            }
        }

        function updateMessageBox() {
            const messageBox = document.getElementById("messageBox");
            messageBox.innerHTML = "";

            messageQueue.forEach((msg) => {
                const messageElement = document.createElement("div");
                messageElement.classList.add("message");
                messageElement.innerText = msg;
                messageBox.appendChild(messageElement);
            });
        }

        function sendMessages() {
            if (isConnected && messageQueue.length > 0) {
                const statusElement = document.getElementById("status");
                statusElement.innerHTML = "Transmitting Messages...";
                statusElement.classList.add("transmitting");

                setTimeout(() => {
                    messageQueue = [];
                    updateMessageBox();

                    statusElement.innerHTML = "Messages Sent Successfully";
                    setTimeout(() => {
                        statusElement.classList.remove("transmitting");
                        statusElement.classList.remove("connected");
                        statusElement.classList.add("disconnected");
                        statusElement.innerHTML = "No Connectivity";
                    }, 2000);
                }, 3000);
            } else {
                alert("No connectivity or no messages to send");
            }
        }
    </script>
</body>
</html>
### Below is the code for encryption using AES algorithm and we included the functionality of there being 4 nodes,connected together by mesh network.We intended it to act as extra feature to above program code,so finally it comes as though the input from the keypad goes to a particular relay node in a mesh network of many relays ,there is a message counter for each node, that increments each time a message reaches it.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Emergency Mesh Network</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/crypto-js/4.1.1/crypto-js.min.js"></script>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; }
        .node { display: inline-block; padding: 15px; margin: 10px; border: 2px solid black; }
        .connected { background-color: lightgreen; }
        .disconnected { background-color: lightcoral; }
        .message-box { border: 1px solid black; padding: 10px; min-height: 50px; }
    </style>
</head>
<body>
    <h1>Emergency Mesh Network</h1>
    <div id="nodes"></div>
    <button onclick="toggleConnectivity()">Toggle Connectivity</button>
    <button onclick="sendMessage()">Send Emergency Message</button>
    <button onclick="checkForInternetNode()">Transmit to NGO</button>

    <script>
        const encryptionKey = "SecretPassphrase";
        const nodes = [
            { id: 1, connected: false, queue: [] },
            { id: 2, connected: false, queue: [] },
            { id: 3, connected: false, queue: [] },
            { id: 4, connected: true, queue: [] } // Internet Node
        ];

        function encryptMessage(message) {
            return CryptoJS.AES.encrypt(message, encryptionKey).toString();
        }
        function decryptMessage(encryptedMessage) {
            let bytes = CryptoJS.AES.decrypt(encryptedMessage, encryptionKey);
            return bytes.toString(CryptoJS.enc.Utf8);
        }

        function toggleConnectivity() {
            nodes.forEach(node => { node.connected = Math.random() > 0.5; });
            updateNodes();
        }

        function updateNodes() {
            let nodesDiv = document.getElementById("nodes");
            nodesDiv.innerHTML = "";
            nodes.forEach(node => {
                let nodeDiv = document.createElement("div");
                nodeDiv.className = node ${node.connected ? 'connected' : 'disconnected'};
                nodeDiv.innerHTML = <strong>Node ${node.id}</strong><br>Messages: ${node.queue.length};
                nodesDiv.appendChild(nodeDiv);
            });
        }

        function sendMessage() {
            let message = "Emergency Request";
            let encryptedMsg = encryptMessage(message);
            nodes[0].queue.push(encryptedMsg);
            passMessage(0);
        }

        function passMessage(index) {
            if (index >= nodes.length - 1) return;
            let nextNode = nodes[index + 1];
            if (nextNode.connected) {
                nextNode.queue.push(...nodes[index].queue);
                nodes[index].queue = [];
                updateNodes();
                passMessage(index + 1);
            }
        }

        function checkForInternetNode() {
            let internetNode = nodes.find(node => node.connected);
            if (internetNode) {
                let decryptedMessages = internetNode.queue.map(encryptMsg => decryptMessage(encryptMsg));
                alert(Internet found at Node ${internetNode.id}. Messages sent: \n${decryptedMessages.join("\n")});
                internetNode.queue = [];
                updateNodes();
            } else {
                alert("No internet nodes available. Messages will keep hopping.");
            }
        }

        updateNodes();
    </script>
</body>
</html>
Both the above codes when used together, will allow user to give a message, the message will be encrypted , then sent to a mesh network of relay nodes,one of the nodes will get the message and as per the connectivity available(here we toggled connectivity manually),the messages will reach intended NGOs,partnered telecommunication companies will aid relays in having connectivity ,as per the connectivity ,the message will hop nodes till it reaches a connected node.
### Project Documentation
For Software:

# Screenshots (Add at least 3)
![Screenshot1](Add screenshot 1 here with proper name)
*Add caption explaining what this shows*

![Screenshot2](Add screenshot 2 here with proper name)
*Add caption explaining what this shows*

![Screenshot3](Add screenshot 3 here with proper name)
*Add caption explaining what this shows*

# Build Photos
![Team](Add photo of your team here)


![Components](Add photo of your components here)
*List out all components shown*

![Build](Add photos of build process here)
*Explain the build steps*

![Final](Add photo of final product here)
*Explain the final build*

### Project Demo
# Video
Included in repository

# Additional Demos
[Add any extra demo materials/links]


---
Made with ❤️ at TinkerHub
